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
or

```SQL server
SELECT Salary as SecondHighestSalary
From employee
order by salary
offset 1 rows
fetch next 1 row only
```

or

```SQL server
SELECT Salary
FROM (
    SELECT row_number() OVER (ORDER BY Salary DESC) as rn, Salary
    FROM Salaries
) as Sn
WHERE rn = 2 --change the number to get different salary
```

181. Employees Earning More Than Their Managers

-self join
-be mindful of you should use managerid = id to get only the employee rows
-if you use id = managerid, you will only get manager rows

```SQL server
select e1.Name as Employee
from Employee e1
join Employee e2
on e1.ManagerId = e2.Id
where e1.Salary>e2.Salary
```

182. Duplicate Emails

```SQL server
select Email
from Person
group by Email
having count(*) > 1
```
183. customers who never buy

```SQL server
select c.Name as Customers
from Customers c
left join Orders o
on c.Id = o.CustomerId
where o.CustomerId is null
```

or

```SQL server
select Name as Customers
from Customers
where Id not in (select CustomerId
                 from Orders)
```
