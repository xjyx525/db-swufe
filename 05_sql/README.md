本周学习了SQL中对空值的处理，聚集函数的使用。

# 本周作业（第4次作业）
不需要操作截图。

## 题目一（2分）
请问下面的SQL语句是否合法？用实验验证你的想法。你从实验结果能得到什么结论？

SELECT dept_name, min(salary)
FROM instructor;
不合法，
语句目标为选择部门名称和最低工资，没有使用GROUP BY子句，
当SELECT子句同时包含聚合函数和非聚合列时，必须使用GROUP BY子句
可以修改为
SELECT dept_name, min(salary)
FROM instructor
GROUP BY dept_name;

SELECT dept_name, min(salary)
FROM instructor
GROUP BY dept_name
HAVING name LIKE '%at%';

不合法，
语句按部门分组并计算最低工资，但HAVING子句中引用了"name"列，而"name"既不是分组列(dept_name)也不是聚合函数
HAVING子句只能引用GROUP BY子句中的列或聚合函数
假设筛选部门名称，可以修改为
SELECT dept_name, min(salary)
FROM instructor
GROUP BY dept_name
HAVING dept_name LIKE '%at%';

SELECT dept_name
FROM instructor
WHERE AVG(salary) > 20000;

不合法，
语句尝试在WHERE子句中使用聚合函数AVG(salary)
不能在WHERE子句中直接使用聚合函数，应该在HAVING子句中使用聚合函数条件。
可以修改为：
SELECT dept_name
FROM instructor
GROUP BY dept_name
HAVING AVG(salary) > 20000;

结论：
1.当SELECT子句同时包含聚合函数和非聚合列时，必须使用GROUP BY子句
2.HAVING子句只能引用GROUP BY子句中的列或聚合函数，不能引用其他列
3.聚合函数不能直接用在WHERE子句中，应该在HAVING子句中使用聚合函数条件

## 题目二（3分+3分+5分）
1. 找到课程总学分最高的系的名字。
SELECT dept_name
FROM course
GROUP BY dept_name
ORDER BY SUM(credits) DESC
LIMIT 1;

3. 有人认为下面的查询结果总是0，你是否认同她的看法？为什么？

```sql
SELECT AVG(salary) - (SUM(salary) / COUNT(*))
FROM instructor;
```
不认同这个查询结果总是0的看法。
有例外情况：
如果salary列包含NULL值，COUNT(*)会计算所有行数，AVG(salary)会忽略NULL值，只计算非NULL值的行数，此时结果可能不为0

3. 用**两种方法**分别找到工资最高的员工的名字（可能不唯一）。
#方法一：使用子查询和等值匹配
SELECT name
FROM instructor
WHERE salary = (SELECT MAX(salary) FROM instructor);

#方法二：使用窗口函数和排名
WITH RankedInstructors AS (
    SELECT 
        name,
        salary,
        DENSE_RANK() OVER (ORDER BY salary DESC) as salary_rank
    FROM instructor
)
SELECT name
FROM RankedInstructors
WHERE salary_rank = 1;
