# Model Card for the BBO Optimisation Approach

## Overview

**Name:** Adaptive Multi-Surrogate Black-Box Optimisation Framework  
**Type:** Sequential surrogate-based optimisation  
**Final version:** Round 13

This approach was developed for the Black-Box Optimisation capstone project in the Imperial College Professional Certificate in Machine Learning and Artificial Intelligence.

Its purpose was to select one new query for each of eight unknown objective functions during each optimisation round.

The final system was not based on a single optimisation model. It evolved into a function-specific framework combining surrogate modelling, historical validation, local search and direct experimental evidence.

## Intended Use

The approach is intended for optimisation problems where:

- the mathematical form of the objective function is unknown;
- evaluations are expensive or limited;
- the input domain is continuous and bounded;
- only a relatively small number of observations are available;
- sequential decisions must balance exploration and exploitation;
- different objective functions may require different search strategies.

The framework is intended to support query selection rather than prove global optimality.

It should not be interpreted as evidence that the true global optimum of any function has been mathematically identified.

The approach would require modification for problems involving categorical variables, non-stationary objectives, very high-dimensional spaces, strict safety constraints or substantially noisy evaluation systems.

## Strategy Evolution

The optimisation strategy changed considerably during the project.

Early rounds relied primarily on Gaussian Process regression and standard Bayesian optimisation ideas. At that stage, broader exploration was useful because relatively little was known about the structure of the eight functions.

As new outputs were returned, it became clear that the functions behaved differently and that one surrogate model could not be assumed to work well for all of them.

Some functions had stable local regions, while others contained sharp response changes or produced surrogate predictions that failed on the next evaluation.

This led to a shift from a common optimisation pipeline toward function-specific decision-making.

By the final rounds, the main principle was:

**Surrogate models generate and rank hypotheses, but returned observations take priority when model predictions and direct evidence disagree.**

## Surrogate Models

Several model families were used during the project:

- Gaussian Process regression;
- Radial Basis Function interpolation;
- Extra Trees regression;
- local quadratic response models.

The models were not treated as equally reliable for every function.

Historical validation was used to determine how much influence each surrogate should receive.

## Model Validation

The project used several forms of validation, including:

- rolling one-step-ahead historical validation;
- leave-one-out validation;
- normalised RMSE;
- Spearman rank correlation;
- improvement-direction accuracy;
- Gaussian Process uncertainty diagnostics;
- comparison of predicted and returned values from recent rounds.

As the project progressed, recent predictive ranking became more important than overall historical fit.

This was because the practical objective was not simply to predict the exact output value. The more important question was whether a model could correctly identify which candidate was more likely to improve the current best observation.

When a model performed poorly on recent observations, its influence on candidate selection was reduced.

## Candidate Generation

Candidate-generation methods changed during the project and included:

- global Sobol sampling;
- local random perturbations;
- boundary searches;
- trust-region refinement;
- sparse-coordinate perturbations;
- directional continuation;
- mirror moves after failed local steps;
- targeted one-dimensional searches;
- six-decimal micro-searches around sharp regions.

Candidate-generation strategy became increasingly local as the evaluation budget decreased.

Late-stage queries were usually based on a small number of experimentally supported directions rather than broad global search.

## Function-Specific Final Strategies

### Function 1

Function 1 was difficult because the observed outputs were extremely small and covered several orders of magnitude.

Raw-value regression was therefore unreliable.

The project used transformed targets and ranking-based comparisons to reduce scale problems.

Broad exploration in Rounds 10 and 11 failed badly. Later queries returned to the best-known region and used smaller local moves.

In Round 12, a positive movement in the first coordinate failed. The final Round 13 query tested the opposite side of the incumbent and produced the final best observation:

`1.7124744581327652e-13`

This was more than two orders of magnitude larger than the previous best.

### Function 2

Function 2 developed an extremely sharp local region.

The best value before Round 12 was approximately:

`0.6301453245`

A change of only `0.000001` in the first coordinate improved the output to:

`0.7567071185`

However, moving another `0.000001` in the same direction in Round 13 reduced the result to:

`0.4368454275`

This function therefore demonstrated the limitations of smooth surrogate models in extremely narrow local peaks.

The final strategy relied more on direct numerical micro-search than surrogate extrapolation.

### Function 3

Function 3 improved in Round 11 to:

`-0.0289486619`

A larger multi-coordinate local move in Round 12 failed.

The final strategy therefore reduced the size and complexity of the move, using a small single-coordinate adjustment instead of another multi-dimensional continuation.

The Round 13 query did not improve the Round 11 incumbent.

### Function 4

Function 4 developed a stable local region.

The optimisation progressively reduced the search radius around this region and used a combination of RBF, GP and direct local evidence.

Round 12 produced a new best of:

`0.6049585587`

Round 13 continued the successful local direction and improved again to:

`0.6097021693`

### Function 5

Function 5 became effectively one-dimensional near its strongest region.

The first, third and fourth coordinates were fixed close to the upper boundary while the second coordinate was progressively refined.

The function improved repeatedly during late-stage optimisation:

- Round 11: approximately `4441.1693`
- Round 12: approximately `4441.2263`
- Round 13: approximately `4441.2869`

This was one of the clearest examples of successful dimensional simplification.

### Function 6

Function 6 produced several unsuccessful model-led local moves.

The best result remained unchanged for several rounds while later proposals returned worse values.

The strategy was therefore simplified to sparse and single-coordinate perturbations around the best observation.

In Round 12, increasing only the second coordinate produced a new best:

`-0.2355946002`

Repeating the same direction in Round 13 did not improve further.

This function showed the value of simplifying the search when surrogate models are unreliable.

### Function 7

Function 7 responded strongly to late-stage directional refinement.

A successful local direction involving mainly the third and fifth coordinates was identified.

The function improved from:

`2.4757340151`

to:

`2.5208541465`

and finally:

`2.5616189426`

The final two rounds confirmed that continuing a direction supported by direct observations could outperform broader candidate search.

### Function 8

Function 8 developed a stable high-performing local region.

The final strategy used small coordinated changes in the third and fifth coordinates.

The best output improved from approximately:

`9.9950507687`

to:

`9.9963337126`

and finally:

`9.9971608561`

This was another example where controlled local continuation worked well once a reliable region had been identified.

## Final Performance

The final best observed values were:

| Function | Best observed output | Best round |
|---|---:|---:|
| Function 1 | 1.7124744581327652e-13 | 13 |
| Function 2 | 0.7567071185005707 | 12 |
| Function 3 | -0.02894866193240312 | 11 |
| Function 4 | 0.6097021692966149 | 13 |
| Function 5 | 4441.286859939468 | 13 |
| Function 6 | -0.2355946001700345 | 12 |
| Function 7 | 2.561618942565491 | 13 |
| Function 8 | 9.9971608560546 | 13 |

Round 12 produced new best values for six of the eight functions.

Round 13 produced new best values for five of the eight functions.

The concentration of improvements in the final rounds supported the move toward function-specific local optimisation.

## Evaluation Criteria

Optimisation performance was evaluated primarily using the returned objective value for each function.

Because the eight functions operate on different numerical scales, raw values were not compared across functions.

Instead, each function was evaluated independently.

The main optimisation criterion was whether a newly evaluated query improved the best observation previously recorded for that function.

Model quality was evaluated using predictive error, ranking quality, recent historical performance and agreement with returned observations.

## Assumptions

The framework assumes that historical observations contain useful information for selecting future queries.

Local search methods also assume that nearby observations may contain information about nearby regions.

These assumptions may fail when a function contains:

- extremely narrow peaks;
- abrupt local changes;
- isolated optima;
- non-smooth behaviour;
- substantial observation noise.

Function 2 demonstrated that even extremely small moves can produce large output changes, so local smoothness should not be assumed without evidence.

## Limitations

The principal limitations are:

- small datasets;
- limited query budget;
- different initial sample sizes across functions;
- adaptive sampling bias;
- concentration of later observations around strong regions;
- possible surrogate-model misspecification;
- uncertain global structure of the hidden functions;
- unstable validation estimates when only a few observations are available.

Agreement between multiple surrogate models does not guarantee correctness because all models are trained on the same limited observations.

High local performance also does not prove global optimality.

## Risk of Overconfidence

One of the main lessons of the project was that model-generated predictions can appear more precise than the evidence supports.

Several candidate points were predicted to improve but returned worse outputs.

For this reason, later rounds reduced reliance on raw predicted magnitude.

Candidate ranking, recent validation and direct experimental results received greater importance.

A model was treated as a decision-support tool rather than an authoritative description of the true function.

## Ethical Considerations

The project does not contain personal or sensitive data.

The principal ethical issue is therefore transparency rather than privacy.

Documenting assumptions, model failures and uncertainty is important because optimisation recommendations can appear more reliable than they are.

The repository records the modelling choices and query history so that another reader can understand how the final decisions were reached.

## Transparency and Reproducibility

The accompanying notebook records the optimisation process, observations, modelling steps and query-generation logic.

The underlying objective functions are hidden by the capstone platform and cannot be reproduced directly.

However, the observable optimisation process can be examined using the stored inputs, returned outputs and decision history.

The accompanying datasheet describes the dataset and its limitations.

## Final Reflection

The main strength of the final approach is its adaptability.

The optimisation system did not assume that one model, acquisition function or search strategy was best for every objective.

Instead, the method evolved as evidence accumulated.

The most important practical lesson was that surrogate models must earn trust through performance on new observations.

The final rounds benefited from simpler local searches, reduced dimensionality and direct use of measured outcomes.

The main weakness remains the limited amount of data. Model validation and local conclusions are necessarily based on a small and adaptively collected sample.

The final framework should therefore be interpreted as an evidence-driven optimisation process rather than a guaranteed solution to the hidden functions.
