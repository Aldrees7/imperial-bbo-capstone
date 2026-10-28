# Datasheet for the Black-Box Optimisation Dataset

## Motivation

This dataset was created for the Black-Box Optimisation (BBO) capstone project in the Imperial College Professional Certificate in Machine Learning and Artificial Intelligence.

The objective of the project was to maximise the outputs of eight unknown functions using a limited number of sequential evaluations. The mathematical form of each function was hidden, so optimisation decisions had to be made entirely from previously observed input-output pairs.

The dataset records both the supplied initial observations and the additional observations collected during the optimisation rounds.

## Composition

The dataset contains observations for eight separate black-box functions.

Each observation consists of:

- an input vector with values between 0 and 1;
- the corresponding output returned by the BBO evaluation system.

The functions have different dimensionalities:

- Function 1: 2 input variables
- Function 2: 2 input variables
- Function 3: 3 input variables
- Function 4: 4 input variables
- Function 5: 4 input variables
- Function 6: 5 input variables
- Function 7: 6 input variables
- Function 8: 8 input variables

After the final Round 13 evaluation, the dataset contained:

- Function 1: 23 observations
- Function 2: 23 observations
- Function 3: 28 observations
- Function 4: 43 observations
- Function 5: 33 observations
- Function 6: 33 observations
- Function 7: 43 observations
- Function 8: 53 observations

The different sample sizes reflect the different initial datasets supplied for each function.

## Collection Process

The initial observations were supplied as part of the BBO capstone project.

Additional observations were collected sequentially. During each optimisation round, one new input vector was selected for each of the eight functions and submitted through the capstone project portal.

The portal returned one output value for each query. The new input-output pairs were then appended to the historical data and used to guide the following round.

The later observations are therefore adaptive rather than independent or randomly sampled. Query locations increasingly concentrated around regions that appeared promising based on previous observations and model predictions.

## Final Best Observations

The best observed outputs at the end of the project were:

| Function | Best observed output | Round |
|---|---:|---:|
| Function 1 | 1.7124744581327652e-13 | 13 |
| Function 2 | 0.7567071185005707 | 12 |
| Function 3 | -0.02894866193240312 | 11 |
| Function 4 | 0.6097021692966149 | 13 |
| Function 5 | 4441.286859939468 | 13 |
| Function 6 | -0.2355946001700345 | 12 |
| Function 7 | 2.561618942565491 | 13 |
| Function 8 | 9.9971608560546 | 13 |

The strongest improvements occurred during the final stages of the project. Round 12 produced new best observations for six of the eight functions, while Round 13 produced new best observations for five.

## Preprocessing

All input variables were supplied numerically within the interval from 0 to 1.

No categorical encoding or missing-value imputation was required.

Inputs were generally used directly in the normalised search space.

Outputs differed substantially in scale across functions, so some modelling approaches used internal standardisation or transformations for numerical stability. Function 1 required particular care because its observed outputs were extremely small and spanned several orders of magnitude.

The original returned outputs were always retained as the authoritative observations when comparing optimisation performance.

## Modelling and Optimisation Uses

The dataset was used with several optimisation and surrogate-modelling approaches during the project, including:

- Gaussian Process regression;
- Radial Basis Function interpolation;
- Extra Trees regression;
- local quadratic models;
- Bayesian optimisation and acquisition-based candidate selection;
- Sobol and broader candidate generation in earlier rounds;
- local trust-region searches;
- sparse-coordinate perturbations;
- directional continuation;
- boundary searches;
- one-dimensional refinement;
- six-decimal micro-searches around sharp local regions;
- recent historical validation of surrogate predictions.

The modelling strategy changed as more evidence became available. Early rounds used broader exploration, while later rounds increasingly used function-specific local optimisation.

## Observed Dataset Characteristics

The eight functions displayed substantially different behaviour.

Function 2 showed extreme local sensitivity. A change of only 0.000001 in one coordinate produced a major improvement in Round 12, while another move of the same size in the same direction produced a large decline in Round 13.

Function 5 became effectively low-dimensional near its best region. Three coordinates remained close to the upper boundary while most late-stage refinement focused on the second coordinate.

Functions 7 and 8 developed relatively stable high-performing local regions and responded well to directional refinement.

Function 6 showed that surrogate predictions could be unreliable locally. Several model-led moves failed before a simpler single-coordinate change produced a new best result.

Function 1 contained outputs on an unusually small numerical scale, making direct regression and comparison more difficult.

These behaviours influenced both the modelling methods and the locations of later observations.

## Intended Uses

The dataset is intended to support:

- analysis of sequential black-box optimisation;
- comparison of surrogate models;
- study of exploration and exploitation;
- evaluation of local versus global search strategies;
- investigation of adaptive experimental design;
- reproduction of the optimisation decisions made during the capstone project.

The dataset is not intended to provide a complete representation of the underlying unknown functions.

## Data Quality and Limitations

The primary limitation is the small number of evaluations relative to the size of the continuous search spaces.

The observations are not uniformly distributed. Later queries are deliberately concentrated around regions that appeared promising, so the dataset contains substantial adaptive sampling bias.

Nearby observations are also not necessarily independent because many late-stage queries were small refinements of earlier points.

The underlying mathematical functions remain hidden. It is therefore impossible to determine from the observed dataset alone whether any global optimum was reached.

A coordinate that appears unimportant in the observed data should not automatically be interpreted as globally irrelevant. It may simply have received limited variation in the sampled region.

Similarly, strong local behaviour should not be assumed to generalise across the entire search space.

## Distribution and Maintenance

The final dataset and supporting documentation are maintained in this GitHub repository together with the optimisation notebook and project results.

The BBO evaluation phase is complete, so the repository now represents the final project state rather than an actively expanding weekly dataset.

Changes made after completion should be versioned through Git so that the final capstone results remain reproducible and traceable.

## Privacy and Ethical Considerations

The dataset contains numerical optimisation inputs and outputs generated for an educational capstone project.

It does not contain personal information, sensitive attributes or human-subject data.

The main risks relate to interpretation rather than privacy. Because the observations were collected adaptively and the true functions are hidden, conclusions about global variable importance or global optimality should be made cautiously.
