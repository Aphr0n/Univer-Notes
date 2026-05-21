SELECT - найважливіша команда в SQL. Отримує (фільтрує) дані з таблиці. 
- Вибрані рядки (WHERE). 
- Вибрані стовпці (SELECT).

# Синтаксис
```SQL
SELECT co
FROM odkial
WHERE co_nas_zaujima
ORDER BY podla_coho_triedit
DESC;
```

# Приклад
```SQL
SELECT ∗ FROM student;
SELECT meno , priezvisko
FROM student;
SELECT meno , priezvisko
FROM student
ORDER BY priezvisko , meno ;
SELECT meno , priezvisko
FROM student
WHERE meno = ’ Janko ’ ;
```