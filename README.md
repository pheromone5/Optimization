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
Loads the Kaggle body-fat prediction dataset (252 rows, 15 columns) via `kagglehub` and explores it with pandas, seaborn and matplotlib.
<!-- TODO: add one line on how the GA is applied to this dataset (e.g. feature selection) and the result. -->

## Run it
```bash
pip install numpy pandas matplotlib seaborn kagglehub jupyter
jupyter notebook
```

## Next steps
- Compare with `scipy.optimize` and a baseline random search.
