# ON
- Визначає умову об'єднання.
- Вона обчислюється перед самим об'єднанням.
# WHERE
- Визначає умову фільтрації.
- Вона обчислюється після створення результату об'єднання.
- Вибір правильного речення для умови може вплинути на продуктивність, а також на значення SELECT.

# Приклад
Об'єднання відділів з їхніми співробітниками та фільтрація лише тих відділів, у яких немає співробітника.
```SQL
SELECT * FROM employee e
RIGHT JOIN department d
ON e.DepartmentID = d.DepartmentID
WHERE e.lastName IS NULL;
```

```SQL
SELECT * FROM employee e
RIGHT JOIN department d
ON e.DepartmentID = d.DepartmentID
AND e.lastName IS NULL;
```