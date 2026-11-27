
**Grid Search** — це метод пошуку оптимальних гіперпараметрів методом повного перебору заданих комбінацій. У презентації він називається **Brute-force approach** (метод грубої сили).

```python
from sklearn.model_selection import GridSearchCV
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier()
param_grid = {
    'max_depth': [2, 4, 6, 8],
    'min_samples_split': [2, 5, 10]
}

grid = GridSearchCV(
    estimator=model,
    param_grid=param_grid,
    cv=5,
    scoring='accuracy'
)
grid.fit(X_train, y_train)

print(grid.best_params_)
print(grid.best_score_)
```

**Що означають параметри?**
- `estimator` — модель, яку налаштовуємо.
- `param_grid` — набір гіперпараметрів.
- `cv=5` — п'ятифолдова крос-валідація.
- `scoring` — метрика, за якою порівнюємо моделі.
- `best_params_` — повертає найкращу знайдену комбінацію.
- `best_score_` — повертає найкращий середній результат крос-валідації.

---