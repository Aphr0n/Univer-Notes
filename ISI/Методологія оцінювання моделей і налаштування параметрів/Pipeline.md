Pipeline — це послідовність декількох кроків обробки даних, об'єднаних в одну систему.

Уявімо, що ми хочемо створити модель, яка визначає, чи є пухлина злоякісною або доброякісною.

Для цього потрібно:
1. Отримати дані.
2. Підготувати дані.
3. Нормалізувати значення.
4. Навчити алгоритм.
5. Отримати модель, яка робить передбачення.
Замість того щоб виконувати всі ці дії окремо, ми можемо об'єднати їх у Pipeline.

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.svm import SVC

pipe = Pipeline([
    ('scaler', StandardScaler()),
    ('classifier', SVC())
])

pipe.fit(X_train, y_train)

y_pred = pipe.predict(X_test)
```

