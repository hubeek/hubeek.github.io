# Join wisely

_Status: Published_
_Created: 2023-11-22 13:15:47_

## Joins

```sql
select distinct users.* from users
left join post users.i = posts.user_id
where views > 90000
```
// 800 ms

## Sub Query1
```sql
select * from users
where id in (
  select user_id from posts where views > 90000
)
```
// 300ms
Never use a sub query? 

Since MySql 8 not true. 

## Sub Query 2
```sql
select * from users where exists ( 
  select user_id from posts where views > 90000 and users.id = user_id 
)  
```
// 200ms
