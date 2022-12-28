# Scikit Learn

## Datasets

``` python
from sklearn.datasets import load_boston
data = load_boston() 								# returns dict with 'data' key containing the dataset
X, y = load_boston(return_X_y=True) # returns np arrays of X and y

```

- sklearn can take dataframes as input but best practice to convert dataframes to numpy arrays for input to sklearn
    - `X = df.drop(columns=['label']).values`
    - `y = df['label'].values`

### Imbalance

- `LogisticRegression(class_weight={0: weight0, 1: weight1})`
    - gives more importance to learning to correctly classify one class over the other



## Pipeline

``` python
from sklearn.linear_model import LinearRegressor
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import Pipeline

...

pipe = Pipeline([
    ("scale", StandardScaler()),
    ("model", LinearRegressor())
])
pipe.fit(X, y)
preds = pipe.predict(X)
```

- Wrap the preprocessing and learning algorithm in a single easy to use object

## Cross Validation

### Grid Search

- Object that wraps a pipeline and all possible hyperparams to test for the learning algorithm and then performs cross validation to find the best hyperparams
- `model,get_params()` returns a dict of the possible params for an algorithm

``` python
from sklearn.model_selection import GridSearchCV

...

clf = GridSearchCV(estimator=pipe,
                    param_grid={'model__n_neighbors': list(range(11))},
                    cv=3
                    )

clf.fit(X,y)
pd.DataFrame(clf.cv_results_) # gives summary stats 

```

## Dummy Baselines

### Classification

``` python
from sklearn.dummy import DummyClassifier

clf = DummyClassifier(strategy="stratified")
clf.fit(X,y)
```

- to get multiple baselines easily:

``` python
pipe = Pipeline([
  ('scale', StandardScaler()),
  ('model', DummyClassifier())
])

grid = GridSearchCV(estimator=pipe,
                    param_grid={'model__strategy': ['stratified', 'most_frequent', 'uniform']},
                    scoring={'acc': make_scorer(accuracy_score)},
                    refit='acc',
                    return_train_score=True)

grid.fit(X, y)
pd.Dataframe(grid.cv_results_)[['param_model__strategy', 'mean_test_acc']]
```

### Regression

``` python
from sklearn.dummy import DummyRegressor

reg = DummyRegressor(strategy="mean")
reg.fit(X,y)
```

