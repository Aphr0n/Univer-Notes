```SQL
begin;
create table my_table(n int);
insert into my_table values (1);
savepoint my_savepoint
insert into my_table values(2);
insert into my_table values(3);
select * from my_table;
```

