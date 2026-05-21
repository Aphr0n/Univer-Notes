OUTER JOIN - використовується для переліку навіть тих записів, які не відповідають критеріям об'єднання (записи, які не мають пари з іншої таблиці).
Типи зовнішніх об'єднань:
- Повне зовнішнє об'єднання:
		`FULL OUTER JOIN`
- Часткове зовнішнє об'єднання:
	- Ліве:
		`LEFT OUTER JOIN`
	- Праве:
		`RIGHT OUTER JOIN`
Також дозволяє використовувати NATURAL та USING як альтернативу умові ON.

# LEFT OUTER JOIN
- Результат завжди містить усі записи з лівої таблиці.
- Кожен рядок з лівої таблиці з'являється принаймні один раз у результаті.
- Відсутні парні записи з правої таблиці замінюються значенням NULL.

![[Pasted image 20260426225204.png]]

## Синтаксис
```SQL
SELECT * FROM tab1
LEFT OUTER JOIN tab2 ON podm;
SELECT * FROM tab1
LEFT JOIN tab2 ON podm;
```

# Приклад
```SQL
SELECT * FROM employee e
LEFT OUTER JOIN department d
ON e.DepartmentID = d.DepartmentID;
```

![[Pasted image 20260426225314.png]]

# RIGHT OUTER JOIN
Результат завжди містить усі записи з правої таблиці. Кожен рядок з правої таблиці з'являється принаймні один раз у результаті. Відсутні парні записи з лівої таблиці замінюються значенням NULL. На практиці ліве зовнішнє об'єднання частіше використовується шляхом заміни таблиць.
![[Pasted image 20260426225713.png]]
## Синтаксис
```SQL
SELECT * FROM tab1
RIGHT OUTER JOIN tab2 ON podm;
SELECT * FROM tab1
RIGHT JOIN tab2 ON podm;
```

## Приклад
```SQL
SELECT * FROM employee e
RIGHT OUTER JOIN department d
ON e.DepartmentID = d.DepartmentID;
```
![[Pasted image 20260426225805.png]]

# FULL OUTER JOIN
Результатом є об'єднання лівого та правого зовнішніх з'єднань. Результат містить усі записи з лівої та всі записи з правої таблиці. Ті, що не мають пари, заповнюються значеннями NULL.

## Синтаксис
```SQL
SELECT * FROM tab1
FULL OUTER JOIN tab2 ON podm;
SELECT * FROM tab1
FULL JOIN tab2 ON podm;
```

## Приклад
```SQL
SELECT * FROM employee e
FULL OUTER JOIN department d
ON e.DepartmentID = d.DepartmentID;
```

![[Pasted image 20260426230157.png]]

