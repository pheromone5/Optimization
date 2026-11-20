# Optimization

Genetic algorithm experiments in Python.

## Notebooks

### `Genetic Algorithm for a given function.ipynb`
A from-scratch GA (NumPy only) that minimises

f(x1, x2) = (x1 + x2 - 7)² + (2·x1 + 3·x2 - 6)² - 7

- Population 1,000, top 100 kept each generation (elitism)
- Offspring: a random survivor plus Gaussian noise, with the noise std decaying 0.99 per generation
- Stops on stagnation (50 generations without improvement); 5 random restarts
- Search bounds: [-500, 500]

**Result:** best x1 = 14.93, x2 = -7.94, f = -6.998. The exact minimum is x1 = 15, x2 = -8 with f = -7.

### `Genetic Algorithm.ipynb`
**Feature selection with a GA** for predicting body fat percentage. Uses the [Kaggle body-fat prediction dataset](https://www.kaggle.com/datasets/fedesoriano/body-fat-prediction-dataset), which has 252 men and 14 features: body density, age, weight, height and 10 body circumferences.

Each individual is a subset of features, encoded as a binary mask over the columns. Everything is written from scratch with NumPy and pandas, without scikit-learn:

| Step | Implementation |
|---|---|
| Preprocessing | z-score standardisation of every feature |
| Model | linear regression fitted by batch gradient descent (lr 0.01, 1,000 iterations) |
| Fitness | AIC = 2k + n·ln(RSS/n); lower is better, so it rewards good fit with few features |
| Initial population | random feature masks, never empty |
| Selection | keep the λ lowest-AIC subsets |
| Crossover | uniform: each feature bit is swapped between the two parents with probability 0.5 |
| Mutation | each bit flips when a N(0.5, 0.25) draw falls below the mutation rate |
| Elitism | the best parents are carried into the next generation unchanged |

Run settings: population 50, 10 parents selected, 10 generations, mutation rate 0.2, 5 elites. The notebook plots the best AIC per generation.

Fitted on all 14 features, the baseline model has RSS = 417.0 and AIC = 154.9.

## Run it
```bash
pip install numpy pandas matplotlib seaborn kagglehub jupyter
jupyter notebook
```

## Next steps
- Compare with `scipy.optimize` and a baseline random search.
- Body-fat GA: drop `Density`, since body fat % is computed from it (Siri's equation), so including it leaks the target.
- Body-fat GA: print the selected feature subset and compare its AIC and held-out error with the full model.
