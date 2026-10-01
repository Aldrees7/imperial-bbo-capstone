# Datasheet for the Black-Box Optimisation Dataset

## Motivation

This dataset was created for the Black-Box Optimisation (BBO) capstone project in the Imperial College Professional Certificate in Machine Learning and Artificial Intelligence.

The purpose of the dataset is to support iterative optimisation of eight unknown functions. For each function, the objective is to identify input values that maximise the returned output while having no direct access to the mathematical form of the function.

The dataset also provides a record of how the optimisation process developed across successive rounds.

## Composition

The dataset contains observations for eight separate black-box functions.

Each observation consists of:

- an input vector containing values between 0 and 1;
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

After Round 9, the dataset contained:

- Function 1: 19 observations
- Function 2: 19 observations
- Function 3: 24 observations
- Function 4: 39 observations
- Function 5: 29 observations
- Function 6: 29 observations
- Function 7: 39 observations
- Function 8: 49 observations

The different sample sizes come from the different initial datasets supplied for each function.

## Collection Process

The initial observations were supplied as part of the BBO capstone project.

Additional observations were collected iteratively. In every round, one new input vector was selected for each of the eight functions and submitted through the capstone project portal.

The portal returned one output value for each submitted query. These input-output pairs were then appended to the existing dataset and used to guide the next round.

Therefore, the data was collected sequentially rather than through a single random sampling process.

The later observations are influenced by the results of earlier rounds because new query points were deliberately selected based on previously observed performance.

## Preprocessing and Uses

All input variables were already represented numerically on the interval from 0 to 1.

No categorical encoding or missing-value imputation was required.

For modelling, the inputs were used directly in the normalised search space.

Some surrogate approaches internally standardised the output values to improve numerical stability. This was particularly useful because the eight functions operate on very different output scales.

The dataset was used for:

- Gaussian Process surrogate modelling;
- Radial Basis Function interpolation;
- Extra Trees regression;
- local search around strong observed solutions;
- global candidate generation using Sobol sampling;
- boundary searches;
- comparison of exploration and exploitation strategies;
- historical validation of surrogate models.

The dataset should not be interpreted as an independent random sample of each function's full search space. Later observations are deliberately concentrated around areas considered promising by the optimisation strategy.

## Distribution and Maintenance

The dataset and supporting project files are maintained in the BBO capstone GitHub repository.

The repository records the optimisation workflow and supporting documentation so that another researcher can understand how the query points were selected.

New observations are added after each round of query evaluation.

The dataset should be versioned alongside the optimisation code because the available information changes after every new round.

## Data Quality and Limitations

The most important limitation is the small number of evaluations relative to the size of the continuous search spaces.

The observations are also not uniformly distributed. Some regions, particularly promising local regions and boundaries, received more samples than others.

This creates sampling bias toward areas favoured by earlier optimisation decisions.

The returned values are treated as the ground-truth observations for the project, but the underlying functions remain unknown.

As a result, it is not possible to determine from the dataset alone whether the global optimum has been found.