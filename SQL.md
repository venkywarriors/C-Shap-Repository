### What is Cross Join in SQL?
The SQL CROSS JOIN produces a result set which is the number of rows in the first table multiplied by the number of rows in the second table if no WHERE clause is used along with CROSS JOIN.This kind of result is called as Cartesian Product.
<br>
If WHERE clause is used with CROSS JOIN, it functions like an INNER JOIN
<br>
<a href="https://www.essentialsql.com/cross-join-introduction/">Cross Join</a>
### SQL Self JOIN
A self JOIN is a regular join, but the table is joined with itself.
<br><a href="https://www.w3resource.com/sql/joins/perform-a-self-join.php">Self JOIN Syntax</a><br>
```
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
```
### Compare differences between two tables in mysql
```
SELECT tbl, ID, col
FROM
(
    SELECT
    tbl_a.ID, tbl_a.col, "name_to_display1" as "tbl" FROM tbl_a
    UNION ALL
    SELECT
    tbl_b.ID, tbl_b.col, "name_to_display2" as "tbl" FROM tbl_b
) t
WHERE ID IN (select ID from tbl_a) AND ID IN (select ID from tbl_b)
GROUP BY
ID, col
HAVING COUNT(*) = 1
 ORDER BY ID
```

```
SELECT * FROM T1
WHERE ID NOT IN (SELECT ID FROM T2)

UNION

SELECT * FROM T2
WHERE ID NOT IN (SELECT ID FROM T1)
```
```
select t1.user_id,t2.user_id 
 from t1 left join t2 ON t1.user_id = t2.user_id 
 and t1.username=t2.username 
 and t1.first_name=t2.first_name 
 and t1.last_name=t2.last_name
//This will compare your table and find all matching pairs, if any mismatch return NULL on left.
```
