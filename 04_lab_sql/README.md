本周通过Postgresql软件实践基本的SQL，并学习了集合操作等知识。

# 本周作业（第3次作业）
本周作业**需要**使用Postgresql及DataGrip软件操作，并对操作页面及结果进行截图。

## 题目一（2分）

完成第2次作业的题目一。
CREATE TABLE users (
    name VARCHAR(50) PRIMARY KEY,
    pswd VARCHAR(50) NOT NULL,
    gender CHAR(1)
);
![image](https://github.com/user-attachments/assets/7e01ed1c-e1cd-46fd-97d1-16a54c84f539)

## 题目二（3分+1分）
1. 新建一个`university`数据库，并执行`largeRelationsInsertFile.sql`，导入数据。
![5636762415f7d00f32152a6258f27f8](https://github.com/user-attachments/assets/be24dab3-9817-4bb3-84f1-a6ef6cb12dc1)
![8b5749d8ef8260f2fa0a9d1a7182ac3](https://github.com/user-attachments/assets/8765d453-4ca6-40b0-9cb0-300882dc95db)
![e6a90e875f777bab162b3547b82c279](https://github.com/user-attachments/assets/ec7deb1a-3016-419b-9170-3d69b7951532)
3. 运行第2次作业的题目三代码。注意：把原题目中的`会计`改成`History`。
SELECT DISTINCT T.name
FROM instructor AS T, instructor AS S
WHERE T.salary > S.salary AND S.dept_name = 'History';
![43d4cb685abee7dbd07414f1627725a](https://github.com/user-attachments/assets/e63ab40b-e792-4394-883b-43f37ad182f1)

## 题目三（2分+2分）
1. 通过实验验证PG中`like`是大小写敏感的。
 ![image](https://github.com/user-attachments/assets/f2369ee6-d385-499d-a1b8-574a91263c8f)
SELECT * FROM test_case_sensitive WHERE text_field LIKE 'S%';
SELECT * FROM test_case_sensitive WHERE text_field LIKE 's%';
3. 在`university`数据库中查询所有包含名字`sci`的学院名称（`dept_name`），而不区分大小写。
![Uploading image.png…]()
SELECT dept_name
FROM department
WHERE dept_name ~* 'sci';
