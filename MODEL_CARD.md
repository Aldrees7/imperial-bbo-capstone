# Model Card for the BBO Optimisation Approach

## Overview

Name: Multi-Surrogate Black-Box Optimisation Approach

Type: Sequential surrogate-based optimisation

Version: Round 10

The approach was developed for the Black-Box Optimisation capstone project.

Its objective is to select one new query for each of eight unknown functions during every optimisation round.

## Intended Use

The approach is intended for optimisation problems where:

- the objective function is unknown;
- evaluations are expensive or limited;
- the input space is continuous and bounded;
- only a small number of observations are available;
- exploration and exploitation must be balanced.

It should not be used as evidence that a global optimum has been mathematically proven.

It is also not suitable without modification for problems with categorical variables, changing objective functions, very high-dimensional spaces or strong safety constraints.

## Optimisation Strategy

The strategy evolved substantially across the ten rounds.

Earlier rounds relied mainly on Gaussian Process surrogate models and acquisition-based optimisation.

As additional observations became available, local search and boundary refinement were increasingly used when repeated results suggested useful structure.

By Round 9, the optimisation used a Gaussian Process with an expected-improvement-based acquisition strategy. However, several predictions were overly optimistic. For example, some functions were predicted to improve but returned worse observed values.

This motivated a more robust strategy for Round 10.

Three different surrogate families were compared:

- Gaussian Process regression;
- Radial Basis Function interpolation;
- Extra Trees regression.

Their performance was evaluated separately for each function using:

- rolling one-step-ahead historical validation;
- leave-one-out validation;
- normalised RMSE;
- Spearman rank correlation;
- Gaussian Process uncertainty diagnostics.

Different surrogate weights were then assigned to different functions rather than assuming that one model was best for every objective.

Candidate points were generated using a mixture of:

- global Sobol sampling;
- local perturbations around the current best observation;
- boundary searches;
- targeted one-dimensional searches;
- function-specific local refinement.

Candidate predictions were converted into percentile ranks so models operating on different numerical scales could be combined.

Exploration was given more weight for functions where the surrogate models had weak historical predictive performance.

Local exploitation was given more weight where repeated observations showed stable promising regions.

## Function-Specific Round 10 Strategy

### Function 1

Historical model ranking performance was weak, so the strategy emphasised global exploration rather than trusting a single surrogate optimum.

### Function 2

Previous observations showed strong performance close to the upper boundary of the second input variable.

The Round 10 search therefore remained close to this boundary while avoiding an almost identical repeat of a previously evaluated point.

### Function 3

None of the surrogate models demonstrated consistently strong predictive performance.

The strategy therefore continued to favour broad exploration.

### Function 4

Strong observations had appeared in a small local region.

Gaussian Process and RBF models both showed useful local structure, although Gaussian Process uncertainty had previously been poorly calibrated.

The Round 10 query therefore used cautious local refinement.

### Function 5

Previous results indicated strong performance when the first, third and fourth variables were near their upper boundaries.

The optimisation was therefore reduced mainly to a one-dimensional refinement of the second variable.

### Function 6

RBF interpolation performed best in validation.

The final query used a cautious movement from the observed incumbent toward an RBF-supported local candidate rather than taking a larger model-generated jump.

### Function 7

RBF produced the strongest rolling historical validation performance.

The search therefore focused on a local region supported by the RBF model while still checking predictions from the other surrogate models.

### Function 8

The best observed results were already concentrated within a promising local region.

The strategy used fine local refinement rather than broad exploration.

## Performance

Performance was evaluated primarily by the observed objective value returned by each black-box function.

Since each function has a different numerical scale, raw objective values were not used to compare performance across different functions.

Instead, surrogate quality was evaluated separately for each function using:

- normalised RMSE;
- Spearman rank correlation;
- rolling historical prediction;
- leave-one-out prediction;
- Gaussian Process predictive coverage and standardised residuals.

The main optimisation criterion remained whether a newly submitted query improved on the best previously observed value for that function.

Round 9 improved two of the eight functions:

- Function 2
- Function 5

The Round 9 results also provided evidence that high predicted surrogate values do not necessarily translate into real improvement. This directly influenced the design of the Round 10 strategy.

Round 10 queries have been selected using the multi-surrogate strategy, but their returned outputs are not included here until they have been evaluated.

## Assumptions and Limitations

A major assumption is that nearby observations contain useful information about nearby regions of the objective function.

This assumption may fail if a function is highly irregular or contains narrow isolated optima.

Another assumption is that historical predictive performance is informative about which surrogate should receive greater influence in the next round.

The main limitations are:

- very small datasets;
- different numbers of initial observations across functions;
- sampling bias toward previously promising areas;
- limited evaluations;
- uncertainty about the shape of the true objective functions;
- potential surrogate-model misspecification.

Agreement between several surrogate models also does not guarantee correctness because all models are trained on the same limited observations.

## Ethical Considerations and Transparency

The project does not involve personal or sensitive data, so the main ethical consideration is transparency rather than individual privacy.

Documenting the optimisation process is important because model-generated recommendations can appear more reliable than they actually are.

Recording the query history, validation methods, model settings and decision rules allows another researcher to understand why a query was selected and where uncertainty remains.

This also improves reproducibility and makes it easier to adapt the approach to other black-box optimisation problems without presenting model predictions as certain.

## Model Card Reflection

The decision process is intentionally documented at both the overall and function-specific levels.

The main strength of the approach is that it no longer assumes one surrogate model is reliable for every function. Historical validation is used to determine how much influence different models should receive.

Its main weakness is the small amount of available data. Model validation itself is therefore based on relatively few observations and can be unstable.

The current level of detail is sufficient to explain the major optimisation decisions, but full reproducibility also requires the accompanying code, query history and dataset contained in the GitHub repository.