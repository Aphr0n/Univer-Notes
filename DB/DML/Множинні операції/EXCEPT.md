EXCEPT дозволяє вам дізнатися, яких рядків з першої таблиці немає в другій таблиці.
- Асиметрична операція (порядок таблиць важливий):
	- A EXCEPT B
	- B EXCEPT A
- Можливість заміни за допомогою OUTER JOIN.

## Синтаксис
```SQL
SELECT column(s) FROM table1
EXCEPT 
SELECT column(s) FROM table2
```

## Приклад
```SQL
SELECT followee
FROM follows
WHERE follower = ’user’
EXCEPT
SELECT friendWith
FROM friendsWith
WHERE friend = ’user’;
```