本周通过Postgresql软件实践基本的SQL，并学习了集合操作等知识。

# 本周作业（第3次作业）

## 题目一（3分+1分）

> **需要**使用PostgreSQL/MySQL及DataGrip软件操作，并对操作页面及结果进行截图。

1. 新建一个`university`数据库，并执行`largeRelationsInsertFile.sql`，导入数据。
![image](https://github.com/user-attachments/assets/5bcc4812-a840-4e78-a378-235a98c3dca8)
![5636762415f7d00f32152a6258f27f8](https://github.com/user-attachments/assets/54cbffd6-d7e8-4fde-992a-ce5803922abc)
![8b5749d8ef8260f2fa0a9d1a7182ac3](https://github.com/user-attachments/assets/8eb3a7dd-dcf8-4822-ae23-0fb3dc600f2d)

3. 运行第2次作业的题目三代码。注意：把原题目中的`会计`改成`History`。
![43d4cb685abee7dbd07414f1627725a](https://github.com/user-attachments/assets/f1717b76-b9bd-4b26-9102-d54e75ac18cf)

## 题目二（3分）

（二选一）

### PostgreSQL

参考[Pattern Matching](https://www.postgresql.org/docs/17/functions-matching.html)，在PG中使用至少三种方法实现找到所有以`S`开头教师的名字。
#使用 LIKE
SELECT name FROM instructor WHERE name LIKE 'S%';
![image](https://github.com/user-attachments/assets/ce2e426a-ed85-48b6-a20a-6a28c47d747d)

#使用正则表达式
SELECT name FROM instructor WHERE name ~ '^S';
![image](https://github.com/user-attachments/assets/ddbec141-6e7b-4276-b093-9e23ec07e3c7)
#使用 LEFT 函数
SELECT name FROM instructor WHERE LEFT(name, 1) = 'S';
![image](https://github.com/user-attachments/assets/a764f411-957e-40c0-b8e8-b4ddcee2888e)


### MySQL

参考[Pattern Matching](https://dev.mysql.com/doc/refman/8.4/en/pattern-matching.html)和[String Functions and Operators](https://dev.mysql.com/doc/refman/8.4/en/string-functions.html) ，在MySQL中使用至少三种方法实现找到所有以`S`开头教师的名字。

## 题目三（3分）

`psql`是PostgreSQL的命令行工具，请使用`psql`命令行工具 (`mysql`是MySQL的命令行工具，请使用`mysql`命令行工具)：

- 实现题目二
方法 1
SELECT name FROM instructor WHERE name LIKE 'S%';

方法 2
SELECT name FROM instructor WHERE name ~ '^S';


方法 3
SELECT name FROM instructor WHERE LEFT(name, 1) = 'S';
- 列出所有的数据库
  \l
  ![image](https://github.com/user-attachments/assets/b8e004b8-46d9-48c7-b325-f49163686e2c)

- 列出当前数据库的所有表
  \dt
- 显示某张表的关系模式
  \d instructor

Hint: [psql](https://www.postgresql.org/docs/current/app-psql.html), [mysql shell](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-commands.html)
