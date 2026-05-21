Найпоширеніший JOIN. Об'єднання створюється шляхом об'єднання записів таблиці на основі умови об'єднання. Зазвичай воно об'єднується за допомогою зовнішнього та первинного ключа.
![[Pasted image 20260426223326.png]]
## Синтаксис
Явний:
```SQL
SELECT * FROM tab1
INNER JOIN tab2 ON podmienka;
```
Неявний (CROSS JOIN + WHERE):
```SQL
SELECT * FROM tab1, tab2
WHERE podmienka;
```
## Приклад

```SQL
SELECT * FROM employee e
INNER JOIN department d
ON e.department=d.departmentid;

SELECT * FROM employee e, department d
WHERE e.department= d.departmentid;
```

![[Pasted image 20260426222801.png]]

![[Pasted image 20260426223635.png]]

# Внутрішнє з'єднання на спільних стовпцях INNER JOIN USING
- Явна альтернатива природному об'єднанню.
- Об'єднує записи таблиці на основі рівних значень явно названих стовпців з однаковим ім'ям.
## Синтаксис
``` SQL
SELECT *
FROM tab1 INNER JOIN tab2
USING(departmentid);
```

## Приклад
```SQL
SELECT * FROM employee e INNER JOIN department d
USING(departmentid);
SELECT * FROM employee e INNER JOIN department d
ON e.departmentid=d.departmentid;
```

![[Pasted image 20260426222801.png]]

![[Pasted image 20260426224020.png]]
