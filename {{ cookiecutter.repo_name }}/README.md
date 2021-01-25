{{cookiecutter.project_name}}
==============================

{{cookiecutter.description}}

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make build` or `make clean`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── environment.yml    <- The environment file for building the conda environment
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://github.com/bramathon/cookiecutter-data-science">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>

# Initializing the project:

## Initialize git

```bash
git init
```

## Initialize dvc

```bash
dvc init
git commit -m 'Initialized DVC'
```

## Add your data

The first thing to do is add the raw data. Put it in data/raw and use the dvc add command eg.

```bash
cp raw_data.csv to data/raw/
docker-compose run --rm dvc add 
```

## Downloading data

Use the DVC pull and push commands to pull the data files from the cache. The DVC docker container can be used for this:

```bash
docker-compose run --rm dvc pull
docker-compose run --rm dvc push
```

## Train the model (example)

To build the project, run

```bash
docker-compose run dvc repro
```

# Built-in Infrastructure

## CircleCI config

The `.circleci/config.yml` file provides automated build and test.

## Pre-commit hooks

For more info: https://pre-commit.com/

The pre-commit hooks automatically runs the linter and checks that large files are not commited to the repo on each commit.

To enable it, run the command (in the pipenv or docker):

```bash
pre-commit install
```

It's a good idea to actually run the checks on the current repo once enabled

```bash
pre-commit run --all-files
```

To add new hooks, edit the file `.pre-commit-config.yaml`
