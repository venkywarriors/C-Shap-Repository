
### What is Cross Join in SQL?
The SQL CROSS JOIN produces a result set which is the number of rows in the first table multiplied by the number of rows in the second table if no WHERE clause is used along with CROSS JOIN.This kind of result is called as Cartesian Product.
<br>
If WHERE clause is used with CROSS JOIN, it functions like an INNER JOIN
<br>
<a href="https://www.essentialsql.com/cross-join-introduction/">Cross Join</a>
### SQL Self JOIN
A self JOIN is a regular join, but the table is joined with itself.
<br>
Self JOIN Syntax
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
