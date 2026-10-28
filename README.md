# Imperial BBO Capstone

Black-Box Optimisation capstone project for the Imperial College Professional Certificate in Machine Learning and Artificial Intelligence.

## Project overview

The aim of this project was to maximise the outputs of eight unknown black-box functions using a limited number of sequential queries.

The project began with Bayesian optimisation and Gaussian Process surrogate models. As more observations became available, the optimisation strategy evolved into a function-specific framework using recent model validation, local trust regions, radial basis function interpolation, tree-based models, sparse-coordinate searches and direct numerical refinement.

The main principle developed during the project was that model predictions should guide the search, but returned observations should take priority when the two disagree.

## Optimisation approach

The workflow developed across the project consisted of:

1. Rebuilding the complete observation history after each round.
2. Comparing the latest result with the current best value.
3. Evaluating the recent performance of different surrogate models.
4. Identifying promising local regions or sensitive coordinates.
5. Generating candidate query points.
6. Selecting a query based on model evidence and previous experimental results.
7. Updating the strategy after the returned output was observed.

Early rounds used broader exploration. Later rounds increasingly focused on local exploitation and function-specific strategies.

Examples included:

- micro-stepping around a very sharp optimum for Function 2;
- reducing Function 5 to an almost one-dimensional search;
- sparse or single-coordinate changes for Function 6;
- directional local refinement for Functions 7 and 8;
- response transformation and ranking-based modelling for Function 1.

## Final results

| Function | Best observed output | Round of best result |
|---|---:|---:|
| Function 1 | 1.7124744581327652e-13 | 13 |
| Function 2 | 0.7567071185005707 | 12 |
| Function 3 | -0.02894866193240312 | 11 |
| Function 4 | 0.6097021692966149 | 13 |
| Function 5 | 4441.286859939468 | 13 |
| Function 6 | -0.2355946001700345 | 12 |
| Function 7 | 2.561618942565491 | 13 |
| Function 8 | 9.9971608560546 | 13 |

The strongest performance occurred during the final stages of the project.

Round 12 produced new best results for six of the eight functions. Round 13 produced new best results for five functions.

These results supported the shift from a general Bayesian optimisation strategy toward smaller, function-specific and evidence-driven searches.

## Key observations

Function 2 demonstrated extremely sharp local behaviour. Moving one coordinate by only `0.000001` improved the result substantially in Round 12, while another move of the same size in the same direction produced a much worse result in Round 13.

Function 5 became almost one-dimensional during late-stage optimisation. Three coordinates remained close to the upper boundary while most refinement focused on the second coordinate.

Function 6 showed that surrogate predictions could be unreliable locally. Several model-led moves failed before a simpler single-coordinate change produced a new best result.

Functions 7 and 8 responded well to continued local directional refinement.

Function 1 was difficult to model because its outputs were extremely small and spanned several orders of magnitude. The final round nevertheless produced a new best result after testing the opposite side of a previously unsuccessful local move.

## Key lessons

Several lessons emerged from the project:

- A single optimisation strategy did not work equally well across all functions.
- Recent predictive performance was more useful than assuming a surrogate model was reliable.
- Direct observations were especially important in sharp or irregular local regions.
- High-dimensional functions often became effectively low-dimensional near their best-known regions.
- Smaller local changes were often more effective than broad exploration late in the optimisation process.
- Model disagreement and failed predictions were useful information and influenced later decisions.
- Surrogate models were most useful as decision-support tools rather than authoritative descriptions of the hidden functions.

## Non-technical summary

This project explored how to optimise eight unknown mathematical functions when only a limited number of evaluations were available. I began by using machine-learning models to predict promising inputs. As more results were collected, it became clear that each function behaved differently, so the strategy became more specialised. Some functions required extremely small changes, while others benefited from following successful local directions. The final method combined predictive models with direct evidence from previous evaluations. The strongest improvements occurred in the final two rounds, showing the importance of adapting an optimisation strategy when new results challenge the assumptions of the model.

## Repository contents

- [`Imperial_BBO_Capstone.ipynb`](Imperial_BBO_Capstone.ipynb) — complete optimisation notebook, including the final Round 13 results.
- [`FINAL_RESULTS.md`](FINAL_RESULTS.md) — summary of the final queries, outputs and best observed results.
- [`DATASHEET.md`](DATASHEET.md) — description of the optimisation dataset, collection process, characteristics and limitations.
- [`MODEL_CARD.md`](MODEL_CARD.md) — description of the adaptive surrogate modelling and query-selection framework.

## Project documentation

- [Dataset Datasheet](DATASHEET.md)
- [Optimisation Model Card](MODEL_CARD.md)
- [Final Results](FINAL_RESULTS.md)
- [Final BBO Notebook](Imperial_BBO_Capstone.ipynb)

## Tools and libraries

The project was developed in Google Colab using Python.

Main libraries included:

- NumPy
- pandas
- SciPy
- scikit-learn
- matplotlib

The optimisation workflow used methods including:

- Gaussian Process regression;
- Radial Basis Function interpolation;
- Extra Trees regression;
- local quadratic modelling;
- Bayesian optimisation;
- Sobol candidate generation;
- trust-region refinement;
- sparse-coordinate perturbations;
- directional continuation;
- one-dimensional refinement;
- micro-searches in sharp local regions.

## Reproducibility

The notebook records the optimisation history, returned observations, model diagnostics, candidate-generation methods and query-selection process used throughout the capstone.

The underlying black-box objective functions were accessed through the course portal and are not included in this repository.

The observable optimisation process can nevertheless be reviewed through the stored queries, returned outputs, final notebook and supporting documentation.

Because the data were collected sequentially and adaptively, the observations should not be interpreted as an independent random sample of the full search spaces.

## Limitations

The project had a limited evaluation budget and relatively small datasets for all eight functions.

Later observations were intentionally concentrated around promising regions, creating adaptive sampling bias.

The mathematical form of the objective functions remained hidden, so the project cannot establish that the global optimum of any function was found.

Local model performance also varied substantially between functions, especially in sharp or irregular regions.

For these reasons, the final results should be interpreted as the best observed solutions found during the capstone rather than mathematically proven global optima.
