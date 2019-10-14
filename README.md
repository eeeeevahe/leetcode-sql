# Leetcode-sql
## TOOLS: MS SQL SERVER
## Author: Eva He

175. combine the 2 tables and return all person info

```SQL Server

SELECT FirstName, LastName, City, State

FROM Person p

LEFT JOIN Address a

ON p.PersonId = a. PersonId
```

176. select the secound highest salary

mySQL TIPS: <br>
      limit x,y: skip the x row and return y (number of) value<br>
      limit x, offset y: skip the y row and return x (number of) value

```MySQL
SELECT (
    SELECT DISTINCT Salary 
    FROM Emplpyee e
    ORDER BY Salary Desc
    LIMIT 1,1
)AS SecondHighestSalary
```
SQL Server TIPS:<br>
TOP: select top (n-m+1) [columnNames..] from [tablename]<br>
where [columnNames..] not in (<br>
    select top (m-1) [columnNames..] from [tablename])<br>
```SQL server
SELECT TOP 1 Salary AS SecondHighestSalary
FROM Employee e
WHERE Salary not in(Select Top 1 Salary 
From Employee e)
```
