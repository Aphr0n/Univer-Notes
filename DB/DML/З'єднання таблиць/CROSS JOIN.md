CROSS JOIN - представляє декартів добуток у SQL, тобто фільтрація не виконується.
# Синтаксис
```SQL
SELECT *
FROM tab1
CROSS JOIN tab2;
Неявна нотація:
SELECT *
FROM tab1,tab2;
```

# Приклад
```SQL
SELECT *
FROM employee
CROSS JOIN department;
```

![[Pasted image 20260426222801.png]]

![[Pasted image 20260426222815.png]]