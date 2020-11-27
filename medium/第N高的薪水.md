### SQL架构
```
Create table If Not Exists Employee (Id int, Salary int)
Truncate table Employee
insert into Employee (Id, Salary) values ('1', '100')
insert into Employee (Id, Salary) values ('2', '200')
insert into Employee (Id, Salary) values ('3', '300')
```
### 题目
编写一段SQL语句，从`Employee`表查询获得第 n 高的薪水。
```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+
```
例如，在上面的`Employee`表中，n = 2时，第二高的薪水是`200`。如果没不存在第 n 高的薪水，那么查询应返回`null`。
```
+------------------------+
| getNthHighestSalary(2) |
+------------------------+
| 200                    |
+------------------------+
```
### 解答
```
-- 解法一
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
	DECLARE M INT DEFAULT null;
    DECLARE T INT DEFAULT (N - 1);
    SELECT distinct salary INTO M FROM Employee order by salary desc limit T,1;
	RETURN M;
END
```

```
-- 解法二
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
  SET N := N-1;
  RETURN (
      # Write your MySQL query statement below.
      select DISTINCT Salary from Employee
      order by Salary desc
      limit N, 1
  );
END
```
