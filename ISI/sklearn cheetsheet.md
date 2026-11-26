# 📈 Scikit-learn Regressor — шпаргалка

> [!summary] Що таке Regression?
> **Regression** — задача прогнозування числового значення.
>
> Приклади:
>
> * ціна будинку → `250000`
> * температура → `21.5`
> * зарплата → `45000`
> * продажі → `1234.7`

---

# 1. Типовий workflow

Майже будь-яка задача регресії в `sklearn` виглядає так:

```python
import pandas as pd

from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error
from sklearn.ensemble import RandomForestRegressor


# 1. Load data
data = pd.read_csv("train.csv")

# 2. Target
y = data["SalePrice"]

# 3. Features
features = [
    "LotArea",
    "YearBuilt",
    "1stFlrSF",
    "2ndFlrSF",
    "FullBath",
    "BedroomAbvGr",
    "TotRmsAbvGrd"
]

X = data[features]

# 4. Split
train_X, val_X, train_y, val_y = train_test_split(
    X,
    y,
    random_state=1
)

# 5. Create model
model = RandomForestRegressor(
    random_state=1
)

# 6. Train
model.fit(train_X, train_y)

# 7. Predict
predictions = model.predict(val_X)

# 8. Evaluate
mae = mean_absolute_error(val_y, predictions)

print(f"MAE: {mae:,.0f}")
```

---

# 2. X, y та random state

У supervised learning:

```text
X → features / input
y → target / output
```

Наприклад:

```python
y = home_data["SalePrice"]

features = [
    "LotArea",
    "YearBuilt",
    "FullBath"
]

X = home_data[features]
```

### X

Має містити ознаки:

```python
X = data[features]
```

Зазвичай це `DataFrame`.

### y

Містить те, що ми хочемо передбачити:

```python
y = data["SalePrice"]
```

Зазвичай це `Series`.

### random state

---

# 3. Train / Validation / Test

Модель не можна оцінювати на тих самих даних, на яких вона навчалась.

## Train

Дані для навчання:

```python
train_X
train_y
```

## Validation

Дані для перевірки моделі:

```python
val_X
val_y
```

## Test

Фінальна перевірка моделі на даних, які модель взагалі не бачила.

---

## `train_test_split`

```python
from sklearn.model_selection import train_test_split

train_X, val_X, train_y, val_y = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=1
)
```

### Основні параметри

```python
test_size=0.2
```

20% → validation/test

```python
test_size=0.3
```

30% → validation/test

```python
random_state=1
```

Фіксує випадковість.

Без нього при кожному запуску split може бути іншим.

> [!tip]
> Для навчання/порівняння моделей майже завжди використовуй `random_state`.

---

# 4. Fit → Predict → Evaluate

Це головний патерн `sklearn`.

```python
model.fit(X_train, y_train)

predictions = model.predict(X_val)

metric = mean_absolute_error(
    y_val,
    predictions
)
```

### `fit()`

Навчити модель:

```python
model.fit(X, y)
```

### `predict()`

Отримати прогноз:

```python
predictions = model.predict(X)
```

---

# 5. Regression Metrics

## MAE — Mean Absolute Error

Найпростіша метрика.

```python
from sklearn.metrics import mean_absolute_error

mae = mean_absolute_error(y_true, predictions)
```

Формула:

$$
MAE = \frac{1}{n}\sum |y_i-\hat{y}_i|
$$

Наприклад:

```text
Real:       100  200  300
Prediction: 110  180  330
```

Помилки:

```text
10, 20, 30
```

MAE:

```text
20
```

### Інтерпретація

Якщо:

```text
MAE = 20,000
```

то модель помиляється приблизно на:

```text
$20,000
```

> [!important]
> **MAE → lower is better**

---

# 6. MSE

```python
from sklearn.metrics import mean_squared_error

mse = mean_squared_error(
    y_true,
    predictions
)
```

Формула:

$$
MSE = \frac{1}{n}\sum(y_i-\hat{y}_i)^2
$$

Через квадрат великі помилки отримують більшу вагу.

> MAE більш стійка до outliers.
>
> MSE сильніше карає великі помилки.

---

# 7. RMSE

```python
from sklearn.metrics import root_mean_squared_error

rmse = root_mean_squared_error(
    y_true,
    predictions
)
```

Або в старіших версіях:

```python
import numpy as np
from sklearn.metrics import mean_squared_error

rmse = np.sqrt(
    mean_squared_error(y_true, predictions)
)
```

RMSE:

$$
RMSE = \sqrt{MSE}
$$

Перевага:

```text
RMSE має ті самі одиниці, що і target
```

Наприклад:

```text
RMSE = $25,000
```

---

# 8. R² — coefficient of determination

```python
from sklearn.metrics import r2_score

r2 = r2_score(
    y_true,
    predictions
)
```

Інтерпретація:

```text
R² = 1      → perfect
R² = 0      → приблизно як baseline
R² < 0      → дуже погана модель
```

> [!important]
> Для MAE/MSE/RMSE → **менше краще**
>
> Для R² → **більше краще**

---

# 9. Основні Regression Models

У `sklearn` є багато регресорів.

Найважливіші:

```text
LinearRegression
Ridge
Lasso
ElasticNet

DecisionTreeRegressor

RandomForestRegressor

GradientBoostingRegressor
RandomForestRegressor
HistGradientBoostingRegressor

RandomForestRegressor
ExtraTreesRegressor

KNeighborsRegressor

SVR

MLPRegressor
```

---

# 10. Linear Regression

Найпростіша модель.

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()

model.fit(train_X, train_y)

predictions = model.predict(val_X)
```

Модель приблизно шукає:

$$
y = b_0 + b_1x_1 + b_2x_2 + ... + b_nx_n
$$

### Коли використовувати

* зв'язок приблизно лінійний
* потрібна проста baseline-модель
* важлива інтерпретованість

---

# 11. Ridge Regression

Linear Regression + L2 regularization.

```python
from sklearn.linear_model import Ridge

model = Ridge(alpha=1.0)

model.fit(train_X, train_y)
```

### `alpha`

Контролює силу regularization:

```python
Ridge(alpha=0.1)
Ridge(alpha=1)
Ridge(alpha=10)
Ridge(alpha=100)
```

Більший `alpha`:

```text
↑ regularization
↓ complexity
```

---

# 12. Lasso Regression

Linear Regression + L1 regularization.

```python
from sklearn.linear_model import Lasso

model = Lasso(alpha=1.0)

model.fit(train_X, train_y)
```

Особливість Lasso:

> Може зануляти coefficients → фактично відбирати features.

---

# 13. ElasticNet

Комбінація L1 + L2.

```python
from sklearn.linear_model import ElasticNet

model = ElasticNet(
    alpha=1.0,
    l1_ratio=0.5
)
```

---

# 14. Decision Tree Regressor 🌳

Твоя перша модель:

```python
from sklearn.tree import DecisionTreeRegressor

model = DecisionTreeRegressor(
    random_state=1
)

model.fit(train_X, train_y)

predictions = model.predict(val_X)
```

Дерево розбиває дані на області:

```text
LotArea < 5000?
       |
   ┌───┴───┐
  YES      NO
   |        |
Price A   Price B
```

---

# 15. `max_leaf_nodes`

Один із найважливіших параметрів Decision Tree.

```python
model = DecisionTreeRegressor(
    max_leaf_nodes=100,
    random_state=1
)
```

### Занадто мало

```text
max_leaf_nodes = 5
```

→ модель занадто проста

→ **underfitting**

### Занадто багато

```text
max_leaf_nodes = 1000
```

→ модель дуже складна

→ **overfitting**

Схематично:

```text
Complexity
   ↑
   |
   |       Overfitting
   |          /
   |         /
   |        /
   |   ___/
   |__/ 
   |
   +----------------→
       Complexity
```

---

# 16. Інші параметри Decision Tree

```python
DecisionTreeRegressor(
    max_depth=10,
    min_samples_split=10,
    min_samples_leaf=5,
    max_features=None,
    max_leaf_nodes=100,
    random_state=1
)
```

### `max_depth`

Максимальна глибина дерева:

```python
max_depth=10
```

### `min_samples_split`

Мінімальна кількість samples для розділення node:

```python
min_samples_split=10
```

### `min_samples_leaf`

Мінімальна кількість samples у leaf:

```python
min_samples_leaf=5
```

### `max_features`

Скільки features використовувати при split.

---

# 17. Random Forest 🌲🌲🌲

Random Forest = багато Decision Trees.

```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(
    random_state=1
)

model.fit(train_X, train_y)

predictions = model.predict(val_X)
```

Ідея:

```text
              Random Forest
                    │
       ┌────────────┼────────────┐
       ↓            ↓            ↓
     Tree 1       Tree 2       Tree 3
       ↓            ↓            ↓
    prediction   prediction   prediction
       └────────────┼────────────┘
                    ↓
                average
                    ↓
                final prediction
```

Random Forest зазвичай стабільніший за одне Decision Tree.

---

# 18. Основні параметри Random Forest

```python
RandomForestRegressor(
    n_estimators=100,
    max_depth=None,
    min_samples_split=2,
    min_samples_leaf=1,
    max_features=1.0,
    random_state=1,
    n_jobs=-1
)
```

## `n_estimators`

Кількість дерев:

```python
n_estimators=100
```

або:

```python
n_estimators=500
```

Більше дерев → зазвичай стабільніше, але довше навчання.

---

## `max_depth`

Максимальна глибина кожного дерева:

```python
max_depth=20
```

---

## `min_samples_leaf`

```python
min_samples_leaf=2
```

Допомагає контролювати overfitting.

---

## `n_jobs`

```python
n_jobs=-1
```

Використати всі доступні CPU cores.

> [!tip]
> Для Random Forest часто використовуй:
>
> ```python
> n_jobs=-1
> ```

---

# 19. Gradient Boosting

Ще один дуже важливий клас моделей.

```python
from sklearn.ensemble import GradientBoostingRegressor

model = GradientBoostingRegressor(
    random_state=1
)

model.fit(train_X, train_y)

predictions = model.predict(val_X)
```

Ідея відрізняється від Random Forest.

### Random Forest

```text
Trees → незалежно → average
```

### Gradient Boosting

```text
Tree 1
  ↓
errors
  ↓
Tree 2
  ↓
errors
  ↓
Tree 3
  ↓
...
```

Наступні дерева намагаються виправляти помилки попередніх.

---

# 20. HistGradientBoostingRegressor

Швидша реалізація gradient boosting для великих datasets.

```python
from sklearn.ensemble import HistGradientBoostingRegressor

model = HistGradientBoostingRegressor(
    random_state=1
)
```

Особливо корисна, коли dataset великий.

---

# 21. Extra Trees

```python
from sklearn.ensemble import ExtraTreesRegressor

model = ExtraTreesRegressor(
    n_estimators=100,
    random_state=1,
    n_jobs=-1
)
```

Схожий на Random Forest, але використовує більше randomization під час побудови дерев.

---

# 22. KNN Regression

```python
from sklearn.neighbors import KNeighborsRegressor

model = KNeighborsRegressor(
    n_neighbors=5
)

model.fit(train_X, train_y)
```

Prediction базується на найближчих samples.

```text
new point
   ↓
find nearest neighbors
   ↓
take average target
```

> [!warning]
> KNN чутливий до масштабу features.
>
> Часто потрібен `StandardScaler`.

---

# 23. Support Vector Regression

```python
from sklearn.svm import SVR

model = SVR(
    kernel="rbf",
    C=100
)
```

Також чутливий до масштабу.

Тому часто:

```python
StandardScaler()
+
SVR()
```

---

# 24. MLPRegressor

Нейронна мережа:

```python
from sklearn.neural_network import MLPRegressor

model = MLPRegressor(
    hidden_layer_sizes=(100, 50),
    max_iter=1000,
    random_state=1
)
```

Для MLP зазвичай потрібен scaling.

---

# 25. Scaling

Деякі моделі чутливі до масштабу:

```text
Linear models
KNN
SVM
Neural Networks
```

Наприклад:

```text
Age:       20
Salary:    50000
```

Масштаби дуже різні.

Використовуємо:

```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()

X_train_scaled = scaler.fit_transform(train_X)

X_val_scaled = scaler.transform(val_X)
```

> [!important]
> На validation/test використовуй **тільки `transform()`**.
>
> Не:
>
> ```python
> scaler.fit_transform(val_X)
> ```
>
> Це може призвести до data leakage.

---

# 26. Pipeline ⭐

Найкращий спосіб поєднати preprocessing + model.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import Ridge

model = Pipeline([
    ("scaler", StandardScaler()),
    ("regressor", Ridge(alpha=1))
])

model.fit(train_X, train_y)

predictions = model.predict(val_X)
```

Pipeline:

```text
Raw data
   ↓
Scaler
   ↓
Model
   ↓
Prediction
```

### Перевага

Менше шансів випадково зробити data leakage.

---

# 27. Categorical Features

Якщо є:

```text
Neighborhood
HouseStyle
GarageType
```

модель не може напряму працювати з текстом.

Потрібно encoding.

Найпоширеніший:

```python
OneHotEncoder
```

---

# 28. ColumnTransformer

Для різних типів колонок можна робити різний preprocessing.

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, StandardScaler

numeric_features = [
    "LotArea",
    "YearBuilt"
]

categorical_features = [
    "Neighborhood",
    "HouseStyle"
]

preprocessor = ColumnTransformer([
    (
        "num",
        StandardScaler(),
        numeric_features
    ),
    (
        "cat",
        OneHotEncoder(handle_unknown="ignore"),
        categorical_features
    )
])
```

Потім:

```python
from sklearn.pipeline import Pipeline
from sklearn.ensemble import RandomForestRegressor

model = Pipeline([
    ("preprocessor", preprocessor),
    ("regressor", RandomForestRegressor(
        n_estimators=200,
        random_state=1,
        n_jobs=-1
    ))
])
```

---

# 29. Missing Values

ML-моделі часто не можуть працювати з `NaN`.

Перевірка:

```python
X.isna().sum()
```

Простий варіант:

```python
X = X.fillna(X.median())
```

Але краще через `SimpleImputer`:

```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(
    strategy="median"
)
```

Для categorical:

```python
SimpleImputer(
    strategy="most_frequent"
)
```

---

# 30. Baseline Model

Перед складною моделлю корисно створити baseline.

Наприклад:

```python
from sklearn.dummy import DummyRegressor

baseline = DummyRegressor(
    strategy="mean"
)

baseline.fit(train_X, train_y)

baseline_predictions = baseline.predict(val_X)

baseline_mae = mean_absolute_error(
    val_y,
    baseline_predictions
)
```

Тепер можна порівняти:

```text
Baseline MAE     50,000
Decision Tree    35,000
Random Forest    25,000
```

---

# 31. Cross-validation

Замість одного train/validation split можна використати кілька split.

```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(
    model,
    X,
    y,
    cv=5,
    scoring="neg_mean_absolute_error"
)
```

Чому `neg_mean_absolute_error`?

`sklearn` очікує, що score:

```text
higher = better
```

А MAE:

```text
lower = better
```

Тому sklearn використовує:

```text
-negative MAE
```

Щоб отримати нормальний MAE:

```python
mae_scores = -scores

print(mae_scores)
print(mae_scores.mean())
```

---

# 32. K-Fold Cross Validation

При:

```python
cv=5
```

dataset ділиться на 5 частин:

```text
Fold 1 → validation
Fold 2 → validation
Fold 3 → validation
Fold 4 → validation
Fold 5 → validation
```

Кожна частина один раз стає validation.

---

# 33. Hyperparameter Tuning

Модель має параметри:

```python
RandomForestRegressor(
    n_estimators=100,
    max_depth=10,
    min_samples_leaf=2
)
```

Це називається:

> **hyperparameters**

Їх можна підбирати автоматично.

---

# 34. GridSearchCV

Перебирає всі комбінації.

```python
from sklearn.model_selection import GridSearchCV

model = RandomForestRegressor(
    random_state=1
)

params = {
    "n_estimators": [100, 200],
    "max_depth": [None, 10, 20],
    "min_samples_leaf": [1, 2, 5]
}

grid = GridSearchCV(
    model,
    params,
    cv=5,
    scoring="neg_mean_absolute_error",
    n_jobs=-1
)

grid.fit(X, y)
```

Найкраща модель:

```python
grid.best_estimator_
```

Найкращі параметри:

```python
grid.best_params_
```

Найкращий score:

```python
grid.best_score_
```

---

# 35. RandomizedSearchCV

Замість перебору всіх комбінацій вибирає випадкові.

```python
from sklearn.model_selection import RandomizedSearchCV

search = RandomizedSearchCV(
    model,
    params,
    n_iter=20,
    cv=5,
    scoring="neg_mean_absolute_error",
    random_state=1,
    n_jobs=-1
)

search.fit(X, y)
```

Корисно, коли параметрів багато.

---

# 36. Overfitting vs Underfitting

## Underfitting

Модель занадто проста.

```text
Training error → high
Validation error → high
```

Що робити:

```text
↑ model complexity
↑ features
↓ regularization
```

---

## Overfitting

Модель запам'ятала training data.

```text
Training error → very low
Validation error → high
```

Що робити:

```text
↓ model complexity
↑ regularization
↑ training data
cross-validation
```

Для Decision Tree:

```python
max_depth
min_samples_leaf
max_leaf_nodes
```

Для Random Forest:

```python
max_depth
min_samples_leaf
max_features
```

---

# 37. Feature Importance

Для tree-based моделей:

```python
model.feature_importances_
```

Наприклад:

```python
import pandas as pd

importance = pd.Series(
    model.feature_importances_,
    index=X.columns
)

print(
    importance.sort_values(
        ascending=False
    )
)
```

Можна отримати:

```text
OverallQual    0.35
GrLivArea      0.20
YearBuilt      0.10
LotArea        0.07
...
```

> [!warning]
> `feature_importances_` не означає причинний вплив.
>
> Це оцінка важливості feature для конкретної моделі.

---

# 38. Твій приклад — повністю

```python
import pandas as pd

from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_absolute_error
from sklearn.tree import DecisionTreeRegressor
from sklearn.ensemble import RandomForestRegressor


# =========================
# 1. Load data
# =========================

data = pd.read_csv(
    "../input/home-data-for-ml-course/train.csv"
)


# =========================
# 2. Target
# =========================

y = data["SalePrice"]


# =========================
# 3. Features
# =========================

features = [
    "LotArea",
    "YearBuilt",
    "1stFlrSF",
    "2ndFlrSF",
    "FullBath",
    "BedroomAbvGr",
    "TotRmsAbvGrd"
]

X = data[features]


# =========================
# 4. Train / validation split
# =========================

train_X, val_X, train_y, val_y = train_test_split(
    X,
    y,
    random_state=1
)


# =========================
# 5. Decision Tree
# =========================

tree_model = DecisionTreeRegressor(
    max_leaf_nodes=100,
    random_state=1
)

tree_model.fit(
    train_X,
    train_y
)

tree_predictions = tree_model.predict(
    val_X
)

tree_mae = mean_absolute_error(
    val_y,
    tree_predictions
)

print(
    f"Decision Tree MAE: {tree_mae:,.0f}"
)


# =========================
# 6. Random Forest
# =========================

rf_model = RandomForestRegressor(
    n_estimators=100,
    random_state=1,
    n_jobs=-1
)

rf_model.fit(
    train_X,
    train_y
)

rf_predictions = rf_model.predict(
    val_X
)

rf_mae = mean_absolute_error(
    val_y,
    rf_predictions
)

print(
    f"Random Forest MAE: {rf_mae:,.0f}"
)
```

---

# 39. Найважливіший pattern для запам'ятовування

```python
# 1. Data
X = data[features]
y = data[target]

# 2. Split
X_train, X_valid, y_train, y_valid = train_test_split(
    X,
    y,
    random_state=1
)

# 3. Model
model = RandomForestRegressor(
    random_state=1
)

# 4. Train
model.fit(X_train, y_train)

# 5. Predict
predictions = model.predict(X_valid)

# 6. Evaluate
mae = mean_absolute_error(
    y_valid,
    predictions
)
```

Запам'ятати:

```text
X
↓
train_test_split()
↓
model
↓
fit()
↓
predict()
↓
metric
```

---

# 40. Швидкий вибір моделі

| Model                           | Плюси                      | Мінуси                           |
| ------------------------------- | -------------------------- | -------------------------------- |
| `LinearRegression`              | проста, швидка             | погано ловить nonlinear patterns |
| `Ridge`                         | regularization             | все ще linear                    |
| `Lasso`                         | feature selection          | може занулити важливі features   |
| `DecisionTreeRegressor`         | легко зрозуміти, nonlinear | легко overfit                    |
| `RandomForestRegressor`         | стабільний, powerful       | більший compute                  |
| `GradientBoostingRegressor`     | сильний на tabular data    | tuning важливіший                |
| `HistGradientBoostingRegressor` | швидкий boosting           | складніший                       |
| `KNeighborsRegressor`           | простий                    | sensitive до scaling             |
| `SVR`                           | потужний nonlinear         | повільний на великих datasets    |
| `MLPRegressor`                  | neural network             | потребує tuning/scaling          |

---

# 41. Що потрібно знати в першу чергу ⭐

Якщо ти тільки вивчаєш `sklearn`, спочатку запам'ятай:

### Data

```python
X
y
```

### Split

```python
train_test_split()
```

### Model

```python
DecisionTreeRegressor()
RandomForestRegressor()
```

### Training

```python
model.fit(X_train, y_train)
```

### Prediction

```python
model.predict(X_valid)
```

### Evaluation

```python
mean_absolute_error(y_valid, predictions)
```

### Tuning

```python
max_depth
max_leaf_nodes
n_estimators
min_samples_leaf
```

### Validation

```python
cross_val_score()
```

### Pipelines

```python
Pipeline()
ColumnTransformer()
```

---

# 42. Швидкий Cheat Sheet

```python
# Imports

import pandas as pd

from sklearn.model_selection import (
    train_test_split,
    cross_val_score,
    GridSearchCV,
    RandomizedSearchCV
)

from sklearn.metrics import (
    mean_absolute_error,
    mean_squared_error,
    root_mean_squared_error,
    r2_score
)

from sklearn.tree import DecisionTreeRegressor

from sklearn.ensemble import (
    RandomForestRegressor,
    GradientBoostingRegressor,
    HistGradientBoostingRegressor,
    ExtraTreesRegressor
)

from sklearn.linear_model import (
    LinearRegression,
    Ridge,
    Lasso,
    ElasticNet
)

from sklearn.pipeline import Pipeline

from sklearn.preprocessing import (
    StandardScaler,
    OneHotEncoder
)

from sklearn.compose import ColumnTransformer

from sklearn.impute import SimpleImputer
```

---

## Model

```python
model = RandomForestRegressor(
    n_estimators=200,
    max_depth=None,
    min_samples_leaf=1,
    random_state=1,
    n_jobs=-1
)
```

## Train

```python
model.fit(X_train, y_train)
```

## Predict

```python
predictions = model.predict(X_valid)
```

## MAE

```python
mae = mean_absolute_error(
    y_valid,
    predictions
)
```

## RMSE

```python
rmse = root_mean_squared_error(
    y_valid,
    predictions
)
```

## R²

```python
r2 = r2_score(
    y_valid,
    predictions
)
```

## Cross-validation

```python
scores = cross_val_score(
    model,
    X,
    y,
    cv=5,
    scoring="neg_mean_absolute_error"
)

mae = -scores.mean()
```

## Feature importance

```python
model.feature_importances_
```

---

# 43. Mental Model 🧠

Весь процес можна тримати в голові так:

```text
                DATA
                  │
                  ↓
            ┌───────────┐
            │ X and y   │
            └─────┬─────┘
                  ↓
          train_test_split
                  │
          ┌───────┴───────┐
          ↓               ↓
       TRAIN           VALIDATION
          │               │
          ↓               │
       model.fit()        │
          │               │
          ↓               │
     model.predict() ─────┘
          │
          ↓
       METRIC
          │
          ↓
   MAE / RMSE / R²
          │
          ↓
    Tune model
          │
          ↓
   Cross-validation
          │
          ↓
    Final model
```

---

# 44. Золоте правило

> **Не вибирай модель за training error.**

Правильно:

```text
Train data
    ↓
fit()
    ↓
Validation data
    ↓
predict()
    ↓
MAE / RMSE / R²
    ↓
compare models
```

Мета:

```text
добре працювати на нових даних
```

а не:

```text
запам'ятати training dataset
```
