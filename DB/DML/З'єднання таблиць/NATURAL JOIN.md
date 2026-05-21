NATURAL JOIN - об'єднує записи таблиці на основі ідентичних значень стовпців
з однаковим ім'ям. Не використовується через неявний вираз умови об'єднання.
# Синтаксис
```SQL
SELECT *
FROM tab1 NATURAL JOIN tab2;
```

# Приклад
```SQL
SELECT *
FROM employee e
NATURAL JOIN department d
```

![[Pasted image 20260426222801.png]]

![[Pasted image 20260426223053.png]]


