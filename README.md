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

The strongest performance occurred in the final stages of the project.

Round 12 produced new best results for six of the eight functions. Round 13 produced new best results for five functions.

These results supported the shift from a general Bayesian optimisation strategy toward smaller, function-specific and evidence-driven searches.

## Key lessons

Several lessons emerged from the project:

- A single optimisation strategy did not work equally well across all functions.
- Recent predictive performance was more useful than assuming a surrogate model was reliable.
- Direct observations were especially important in sharp or irregular local regions.
- High-dimensional functions often became effectively low-dimensional near their best-known regions.
- Smaller local changes were often more effective than broad exploration late in the optimisation process.
- Model disagreement and failed predictions were useful information and should influence the next decision.

## Non-technical summary

This project explored how to optimise eight unknown mathematical functions when only a limited number of evaluations were available. I began by using machine-learning models to predict promising inputs. As more results were collected, it became clear that each function behaved differently, so the strategy became more specialised. Some functions required extremely small changes, while others benefited from following successful local directions. The final method combined predictive models with direct evidence from previous evaluations. The strongest improvements occurred in the final two rounds, showing the importance of adapting an optimisation strategy when new results challenge the assumptions of the model.

## Repository contents

- `README.md` — project overview, methodology and final results.
- `DATASHEET.md` — description of the optimisation data and its limitations.
- `MODEL_CARD.md` — description of the surrogate modelling and decision framework.
- `notebooks/Imperial_BBO_Capstone_Final.ipynb` — final project notebook.
- `results/` — final queries and result summary.
- `presentation/` — final capstone presentation.

## Project documentation

- [Dataset Datasheet](DATASHEET.md)
- [Optimisation Model Card](MODEL_CARD.md)

## Tools and libraries

The project was developed in Google Colab using Python.

Main libraries included:

- NumPy
- SciPy
- pandas
- scikit-learn
- matplotlib

## Reproducibility

The notebook records the optimisation history, returned observations, model diagnostics and query-generation process used throughout the capstone.

Because the objective functions were accessed through the course portal, the hidden black-box functions themselves are not included in this repository. The recorded inputs and returned outputs document the observable optimisation process.
