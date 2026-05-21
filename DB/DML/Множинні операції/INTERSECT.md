INTERSECT - Створює перетин двох таблиць містить усі рядки, які є ідентичними в обох таблицях. Можна замінити за допомогою INNER JOIN.

## Синтаксис
```SQL
SELECT column(s) FROM table 1
INTERSECT 
SELECT column(s) FORM table 2
```

## Приклад
```SQL
SELECT followee
FROM follows
WHERE follower == 'user'
INTERSECT 
SELECT friend_with
FROM friends_with
WHERE friend == 'user';
```

