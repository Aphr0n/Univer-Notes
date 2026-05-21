Прапорець для оператора CREATE VIEW. Умова в реченні WHERE представлення має бути істинною для даних, що вставляються/оновлюються.
```SQL
CREATE VIEW oldusers AS
SELECT * FROM DBUser
WHERE birthday < ’1988-01-01’
WITH CHECK OPTION ;
```