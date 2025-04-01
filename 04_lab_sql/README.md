本周通过Postgresql软件实践基本的SQL，并学习了集合操作等知识。

# 本周作业（第3次作业）

## 题目一（3分+1分）

> **需要**使用PostgreSQL/MySQL及DataGrip软件操作，并对操作页面及结果进行截图。

1. 新建一个`university`数据库，并执行`largeRelationsInsertFile.sql`，导入数据。
![5636762415f7d00f32152a6258f27f8](https://github.com/user-attachments/assets/be24dab3-9817-4bb3-84f1-a6ef6cb12dc1)
![8b5749d8ef8260f2fa0a9d1a7182ac3](https://github.com/user-attachments/assets/8765d453-4ca6-40b0-9cb0-300882dc95db)
![e6a90e875f777bab162b3547b82c279](https://github.com/user-attachments/assets/ec7deb1a-3016-419b-9170-3d69b7951532)

3. 运行第2次作业的题目三代码。注意：把原题目中的`会计`改成`History`。
SELECT DISTINCT T.name
FROM instructor AS T, instructor AS S
WHERE T.salary > S.salary AND S.dept_name = 'History';
![43d4cb685abee7dbd07414f1627725a](https://github.com/user-attachments/assets/e63ab40b-e792-4394-883b-43f37ad182f1)

## 题目二（3分）

（二选一）使用PostgreSQL

### PostgreSQL

参考[Pattern Matching](https://www.postgresql.org/docs/17/functions-matching.html)，在PG中使用至少三种方法实现找到所有以`S`开头教师的名字。
##使用 LIKE
SELECT name FROM instructor WHERE name LIKE 'S%';
![image](https://github.com/user-attachments/assets/cc3f77a9-59f7-4059-b006-ec9e792d1327)

##使用正则表达式 ~
SELECT name FROM instructor WHERE name ~ '^S';
![image](https://github.com/user-attachments/assets/a8bb54a8-0db5-4722-bd7d-84c6d095dce7)

##使用 LEFT 函数
SELECT name FROM instructor WHERE LEFT(name, 1) = 'S';
![image](https://github.com/user-attachments/assets/9cb0b773-cbe0-46e5-b0fe-7b77929b70fa)

### MySQL

参考[Pattern Matching](https://dev.mysql.com/doc/refman/8.4/en/pattern-matching.html)和[String Functions and Operators](https://dev.mysql.com/doc/refman/8.4/en/string-functions.html) ，在MySQL中使用至少三种方法实现找到所有以`S`开头教师的名字。

## 题目三（3分）

`psql`是PostgreSQL的命令行工具，请使用`psql`命令行工具 (`mysql`是MySQL的命令行工具，请使用`mysql`命令行工具)：

- 实现题目二
  \c university
  -- 方法 1：使用 LIKE
SELECT name FROM instructor WHERE name LIKE 'S%';
![image](https://github.com/user-attachments/assets/e4fa8fc3-8bcf-4ddd-a9fb-9773dbade3e6)
-- 方法 2：使用正则表达式 ~
SELECT name FROM instructor WHERE name ~ '^S';
![image](https://github.com/user-attachments/assets/a26f0da0-8ef3-4027-8fd6-f0fe04c26072)
-- 方法 3：使用 LEFT 函数
SELECT name FROM instructor WHERE LEFT(name, 1) = 'S';
![image](https://github.com/user-attachments/assets/c65b9085-5269-4776-b31e-6b557f1c5a1d)

- 列出所有的数据库
  \l
  ![image](https://github.com/user-attachments/assets/ee61deb6-f3b0-4f80-b4f1-047a3c4a86d8)

- 列出当前数据库的所有表
  \dt
- 显示某张表的关系模式
  \d instructor

Hint: [psql](https://www.postgresql.org/docs/current/app-psql.html), [mysql shell](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-commands.html)
