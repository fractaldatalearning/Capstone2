# Katin Lind Springboard Bootcamp Capstone 2 Summary: Instacart Recommendations

In this project I'm working with data used in a kaggle challenge. My goal is to determine which items instacart should recommend to each user next time they log into their account (based on predictions of what they'll reorder from items purchased in the past). 

Dataset originated here: https://www.kaggle.com/competitions/instacart-market-basket-analysis/overview

My [summative project report is available here], or read a summary below to understand what can be found in which notebook:

1. In the [wrangling notebook](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/1-kl-wrangling.ipynb), I load data and merge data about products with that about users and their orders. 

2. Exploratory data analysis begins in [notebook 2](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/2-kl-eda-w-data-direct-from-wrangling.ipynb) but continues all the way through notebook 6, as more insights about the data become possible after some features are engineered. Specifically, in notebooks [3](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/3-kl-eda-w-single-user.ipynb) and [4](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/4-kl-eda-modeling-w-single-user.ipynb), I explore in-depth one single user's purchasing and re-ordering habits in order to deeply understand factors that might support accurate predictions of items they will reorder in the future. 

3. Notebooks [5.1](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/5.1-kl-preprocess-select-users-add-rows.ipynb) and [5.2](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/5.2-kl-preprocess-get-usable-data.ipynb) are dedicated to the most crucial step of adding non-ordered items to each order by each user. This spans two notebooks only because the size of the dataset was slowing down my work in the first. This is such a crucial step because the raw data came with only information about items a user actually purchased in each order. In order to make predictions about what a user will re-order in their 100th order, for example, we need to know, from their 99th order, which items they reordered AND *did not* reorder from among all items they ever ordered. This required creating new rows such that the size of each order grew cumulatively over time for each user, and this resulted in a dataframe with approxiimately 15 times as many rows as the raw set.  

4. I had the most fun with [notebook 6](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/6-kl-preprocess-feature-engineer.ipynb), where I engineered several new features. For example, for each item in each order, I added a column to indicate the percentage of past orders where that item had been purchased. Other new features included "percent of past orders where this product was one of the first 6 items placed in this user's cart" and product kewords such as "organic" or "fresh." These improve modeling because "percent of past orders where this item was purchased," for example, is highly correlated with whether an item will be reordered again in the future, but until the feature was engineered, a model would have had no way to pcik up on this valuable variable. 

5. In [notebook 7](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/7-kl-preprocess-encoding.ipynb), I tried multiple strategies for encoding categorical data and chose a Target Encoder with default hyperparameters in order to encode categorical features such as the user id, product name, and aisle and department in which each product is classified. 

6. Finally, in [notebook 8](https://github.com/fractaldatalearning/Capstone2/blob/main/notebooks/8-kl-modeling.ipynb), I use a random grid search with cross-validation to test multiple classifiers. I selected the Random Forest classifier becaue it performed best overall in a combined evaluation using log loss, roc_auc, and f1 metrics. I tuned the hyperparameters and finalized the model. 

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── processed        <- Intermediate data that has been transformed.
    │   ├── final      <- The final, canonical data sets for modeling.
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
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
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

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
