# Insta Data Science

_A standardized project structure for doing and sharing data science work._

Heavily based on [cookiecutter-data-science](http://drivendata.github.io/cookiecutter-data-science/).


## Project Organization
------------

The directory structure of your new project looks like this: 

```
├── LICENSE
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
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
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── poetry.lock        <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `poetry lock`
│
├── pyproject.toml     <- Pyproject.toml file for poetry
│
├── src                <- Source code for use in this project.
│   ├── __init__.py    <- Makes src a Python module
│   │
│   ├── utils.py       <- Utility functions
│   │
│   ├── features.py    <- Functions for data processing
│   │
│   ├── models.py      <- Functions for model training and prediction
│   │
│   └── plotting.py    <- Functions for plotting
```

### Installing development requirements
------------

    poetry install

### Running the tests
------------

    pytest tests
