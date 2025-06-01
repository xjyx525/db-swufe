# 本周作业（第7次作业）

## 题目一（3分+2分）
考虑一个用于记录学生（student）在不同课程段（section）在不同考试中取得成绩（grade）的数据库，其中课程段属于某个课程（course）。

1. 绘制E-R图，只用二元联系。确保能够表示一个学生在不同考试中获得的成绩，且一个课程段可能有多次考试。（提示：使用多值属性）
![df1b60bf530df18decaec028f28abb3](https://github.com/user-attachments/assets/520fedc0-95c0-44f0-bddd-e45321914043)

2. 写出上面E-R图的关系模式（要求注明主码）。
Student(student_id, name, ...)    主码: student_id
Course(course_id, title, ...)    主码: course_id
Section(section_id, course_id, ...)   主码: section_id; 外码: course_id → Course
Enroll(student_id, section_id)   主码: (student_id, section_id); 
                                 外码: student_id → Student, section_id → Section
ExamGrade(student_id, section_id, exam_id, grade)   主码: (student_id, section_id, exam_id);
                                 外码: (student_id, section_id) → Enroll

## 题目二（3分）
​​#没有非平凡函数依赖​​：
如果 R 中不存在任何非平凡 FD，则没有依赖违反 BCNF 条件，因此 R 属于 BCNF。

​​#存在非平凡函数依赖​​：
在 R(A,B) 中，可能的非平凡 FD 只有以下三种情况：
情况1: A→B​​
A 决定 B，即A决定所有属性（A→AB），所以 A 是候选码。 FD A→B，左边 A 是超码，满足 BCNF。
情况2: B→A​​
B 决定所有属性，B 是候选码。FD B→A 左边 B 是超码，满足 BCNF。
情况3: A→B 和 B→A 同时存在​​
此时 A 和 B 相互决定, A 和 B 都是候选码。对 FD A→B，A 是超码；对 FD B→A，B 是超码，均满足 BCNF。

综上：任何非平凡 FD 的左边都是候选码，所以 R(A,B) 必定属于 BCNF。
## 题目三（2分）
关于关系模式r(A, B, C, D, E)，有如下函数依赖：

- A → BC
- CD → E
- B → D
- E → A

列出该关系模式的的候选码。
A
E
BC（集合 {B,C})
CD（集合 {C,D})
