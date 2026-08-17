# Lab 09：数据结构综合应用

## 一、实训目的

通过本次实训综合运用字符串、列表、元组、字典和集合等 Python 数据结构，进一步理解不同数据结构的特点及适用场景，能够根据实际问题选择和组合合适的数据结构，并利用条件判断、循环和数据结构完成具有一定规模的数据管理程序。

前面的 Lab 已经分别学习了：

```text
字符串
列表
元组
字典
集合
```

从本次实验开始，不再重点讨论：

```text
“某种数据结构的语法怎么写？”
```

而是重点解决：

```text
“面对一个实际问题，
应该选择什么数据结构，
以及怎样把这些数据结构组合起来？”
```

本次实验的核心学习路线为：

```text
实际问题
   ↓
分析数据特点
   ↓
选择数据结构
   ↓
组织结构化数据
   ↓
查询与统计
   ↓
菜单式管理
   ↓
完整数据管理程序
```

---

## 二、实训内容

本次实训主要包括：

1. 根据实际问题设计合适的数据结构；
2. 综合使用列表、字典、集合和元组组织数据；
3. 对结构化数据进行查询、筛选、统计和排序；
4. 使用菜单式程序完成数据增加、查询、修改和统计；
5. 综合完成一个 AI 课程学习数据管理系统。

本次实训设置：

**3 个必做任务 + 1 个拓展任务。**

---

# 三、任务1：学生学习数据结构设计

## 1. 任务背景

假设需要使用 Python 管理人工智能专业学生的课程学习信息。

每名学生需要保存：

```text
学号
姓名
专业
Python课程成绩
AI基础课程成绩
已经完成的Lab
感兴趣的AI方向
```

如果继续使用独立变量：

```python
name1 = "张三"
score1 = 88

name2 = "李四"
score2 = 92
```

当学生数量越来越多时，程序会非常难管理。

本任务要求根据数据特点选择合适的数据结构。

---

## 2. 创建程序

创建：

```text
task01_structure_design.py
```

---

## 3. 设计课程基本信息

课程名称、学期等信息在程序运行期间通常不会改变，可以使用元组表示：

```python
course_info = (
    "高级语言程序设计实训",
    "人工智能专业",
    "2026"
)
```

输出：

```python
print(f"课程名称：{course_info[0]}")
print(f"面向专业：{course_info[1]}")
print(f"开课年度：{course_info[2]}")
```

思考：

> 为什么这里可以使用元组，而不是必须使用列表？

---

## 4. 使用字典描述一名学生

例如：

```python
student = {
    "student_id": "20260001",
    "name": "张三",
    "major": "人工智能",
    "python_score": 88,
    "ai_score": 92
}
```

访问：

```python
print(student["name"])
print(student["python_score"])
```

---

## 5. 使用集合保存已完成Lab

假设张三已经完成：

```python
completed_labs = {
    "Lab01",
    "Lab02",
    "Lab03",
    "Lab04",
    "Lab05"
}
```

可以将集合放入学生字典：

```python
student["completed_labs"] = completed_labs
```

然后输出：

```python
print(student["completed_labs"])
```

---

## 6. 保存AI兴趣方向

例如：

```python
student["ai_interests"] = {
    "Computer Vision",
    "Machine Learning"
}
```

由于同一个兴趣方向没有必要重复保存，因此集合是一种比较合适的数据结构。

---

## 7. 使用列表保存多名学生

创建：

```python
students = []
```

然后：

```python
students.append(student)
```

继续添加第二名、第三名学生。

最终数据结构可以理解为：

```text
students
   ↓
列表
   ↓
多个学生
   ↓
每个学生是一个字典
   ↓
字典内部还可以包含集合
```

即：

```text
list
 ├── dict
 │    ├── student_id
 │    ├── name
 │    ├── python_score
 │    ├── ai_score
 │    ├── completed_labs → set
 │    └── ai_interests   → set
 │
 ├── dict
 │
 └── dict
```

---

## 8. 数据结构分析

完成下面的分析：

| 数据      | 推荐结构  | 原因          |
| ------- | ----- | ----------- |
| 课程基本信息  | tuple | 数据较固定       |
| 一名学生的信息 | dict  | 多个具有明确含义的属性 |
| 多名学生    | list  | 保存多条记录      |
| 已完成Lab  | set   | 不需要重复       |
| AI兴趣方向  | set   | 不需要重复       |

---

## 9. 思考

回答：

1. 为什么不能只使用一个列表保存所有学生信息？
2. 为什么学生适合使用字典表示？
3. 为什么多个学生适合使用“列表 + 字典”？
4. 集合在学生数据中解决了什么问题？
5. 数据结构选择是否应该根据实际问题决定？

---

# 四、任务2：结构化数据查询与统计

## 1. 任务目标

在已经组织好的学生数据基础上，完成：

```text
遍历
查询
筛选
统计
排序
集合分析
```

---

## 2. 创建程序

创建：

```text
task02_data_analysis.py
```

可以首先准备以下测试数据：

```python
students = [
    {
        "student_id": "20260001",
        "name": "张三",
        "python_score": 88,
        "ai_score": 92,
        "completed_labs": {"Lab01", "Lab02", "Lab03", "Lab04"},
        "ai_interests": {"Computer Vision", "Machine Learning"}
    },
    {
        "student_id": "20260002",
        "name": "李四",
        "python_score": 95,
        "ai_score": 90,
        "completed_labs": {"Lab01", "Lab02", "Lab03", "Lab04", "Lab05"},
        "ai_interests": {"Machine Learning", "NLP"}
    },
    {
        "student_id": "20260003",
        "name": "王五",
        "python_score": 76,
        "ai_score": 82,
        "completed_labs": {"Lab01", "Lab02", "Lab03"},
        "ai_interests": {"Computer Vision"}
    }
]
```

---

## 3. 输出所有学生

使用循环输出：

```text
学号
姓名
Python成绩
AI基础成绩
```

参考形式：

```text
========================================
学生学习信息
========================================

20260001  张三  Python:88  AI:92
20260002  李四  Python:95  AI:90
20260003  王五  Python:76  AI:82

========================================
```

---

## 4. 按学号查询学生

用户输入：

```text
请输入学号：
```

遍历：

```python
found = False

for student in students:

    if student["student_id"] == target_id:

        print(f"姓名：{student['name']}")
        print(f"Python成绩：{student['python_score']}")
        print(f"AI成绩：{student['ai_score']}")

        found = True
        break
```

如果没有找到：

```text
未找到该学生。
```

---

## 5. 筛选优秀学生

规定：

```text
Python成绩 ≥ 90
```

为 Python 课程优秀。

输出所有满足条件的学生。

进一步筛选：

```text
Python成绩 ≥ 90
且
AI基础成绩 ≥ 90
```

的学生。

---

## 6. 计算平均成绩

分别计算：

```text
Python课程平均成绩
AI基础课程平均成绩
```

可以使用：

```python
python_total = 0
ai_total = 0

for student in students:
    python_total += student["python_score"]
    ai_total += student["ai_score"]
```

然后：

```python
python_average = python_total / len(students)
ai_average = ai_total / len(students)
```

---

## 7. 查找Python成绩最高的学生

首先：

```python
best_student = students[0]
```

然后：

```python
for student in students:

    if student["python_score"] > best_student["python_score"]:
        best_student = student
```

输出：

```text
Python课程最高成绩学生：
姓名：李四
成绩：95
```

---

## 8. 按Python成绩排序

可以使用：

```python
sorted_students = sorted(
    students,
    key=lambda student: student["python_score"],
    reverse=True
)
```

> `lambda` 在本次实验中只需要理解为“告诉 `sorted()` 按哪个字段排序”，不要求深入掌握函数原理。函数将在 Lab10 系统学习。

输出排序结果。

---

## 9. 统计所有AI兴趣方向

创建：

```python
all_interests = set()
```

然后：

```python
for student in students:
    all_interests = all_interests | student["ai_interests"]
```

最终输出：

```text
当前学生涉及的AI兴趣方向：

Computer Vision
Machine Learning
NLP
```

---

## 10. 查找共同兴趣

例如前两名学生：

```python
common_interests = (
    students[0]["ai_interests"]
    & students[1]["ai_interests"]
)
```

观察共同兴趣。

---

## 11. Lab完成情况统计

输出每名学生：

```text
姓名
已完成Lab数量
```

例如：

```python
for student in students:

    completed_count = len(student["completed_labs"])

    print(
        f"{student['name']}："
        f"已完成 {completed_count} 个Lab"
    )
```

进一步查找：

```text
完成Lab数量最多的学生
```

---

# 五、任务3：AI课程学习数据管理系统

## 1. 任务背景

前两个任务已经完成：

```text
数据结构设计
+
查询
+
筛选
+
统计
```

本任务进一步将这些功能组合起来，完成一个相对完整的：

# AI课程学习数据管理系统

这是 Lab01～Lab09 中规模最大的综合程序之一。

---

## 2. 创建程序

创建：

```text
task03_ai_course_manager.py
```

---

## 3. 系统数据

创建：

```python
students = []
```

用于保存所有学生。

每名学生至少包含：

```text
student_id
name
python_score
ai_score
completed_labs
ai_interests
```

---

# 六、系统功能设计

程序菜单建议设计为：

```text
==================================================
            AI课程学习数据管理系统
==================================================

1. 添加学生
2. 查看全部学生
3. 查询学生
4. 修改学生成绩
5. 查看成绩统计
6. 查看优秀学生
7. 查看Lab完成情况
8. 查看AI兴趣方向
0. 退出系统

==================================================
```

程序主体使用：

```python
while True:
```

持续显示菜单。

---

# 七、功能1：添加学生

## 1. 输入基本信息

用户输入：

```text
学号
姓名
Python成绩
AI基础成绩
```

必须检查：

```text
0 ≤ 成绩 ≤ 100
```

---

## 2. 检查学号重复

添加之前遍历：

```python
id_exists = False

for student in students:

    if student["student_id"] == student_id:
        id_exists = True
        break
```

如果已经存在：

```text
该学号已经存在，不能重复添加。
```

---

## 3. 输入已完成Lab

可以让用户输入：

```text
Lab01,Lab02,Lab03
```

然后：

```python
lab_text = input("请输入已完成Lab，用逗号分隔：")

completed_labs = set(
    lab_text.split(",")
)
```

---

## 4. 输入AI兴趣方向

例如：

```text
Computer Vision,Machine Learning
```

转换为集合：

```python
interest_text = input(
    "请输入AI兴趣方向，用逗号分隔："
)

ai_interests = set(
    interest_text.split(",")
)
```

---

## 5. 创建学生字典

```python
student = {
    "student_id": student_id,
    "name": name,
    "python_score": python_score,
    "ai_score": ai_score,
    "completed_labs": completed_labs,
    "ai_interests": ai_interests
}
```

加入列表：

```python
students.append(student)
```

---

# 八、功能2：查看全部学生

如果：

```python
len(students) == 0
```

输出：

```text
当前暂无学生数据。
```

否则遍历输出：

```text
学号
姓名
Python成绩
AI成绩
完成Lab数量
```

例如：

```text
------------------------------------------------------------
学号        姓名      Python      AI      完成Lab
------------------------------------------------------------
20260001   张三        88         92         6
20260002   李四        95         90         7
20260003   王五        76         82         5
------------------------------------------------------------
```

---

# 九、功能3：查询学生

输入学号。

如果找到，则显示完整信息：

```text
========================================
学生详细信息
========================================

学号：20260001
姓名：张三

Python成绩：88
AI基础成绩：92

已完成Lab：
Lab01
Lab02
Lab03
...

AI兴趣：
Computer Vision
Machine Learning

========================================
```

如果未找到：

```text
未找到该学生。
```

---

# 十、功能4：修改学生成绩

输入学号。

查找到学生后：

```text
1. 修改Python成绩
2. 修改AI基础成绩
0. 返回
```

修改后的成绩仍需满足：

```text
0 ≤ score ≤ 100
```

---

# 十一、功能5：查看成绩统计

统计：

```text
学生总人数
Python平均成绩
AI平均成绩
Python最高成绩
Python最低成绩
AI最高成绩
AI最低成绩
```

例如：

```text
========================================
课程成绩统计
========================================

学生人数：30

Python平均成绩：82.36
Python最高成绩：97
Python最低成绩：58

AI平均成绩：84.21
AI最高成绩：98
AI最低成绩：61

========================================
```

---

# 十二、功能6：查看优秀学生

规定：

```text
Python成绩 ≥ 90
且
AI基础成绩 ≥ 90
```

为综合优秀。

输出所有综合优秀学生。

例如：

```text
综合优秀学生：

李四
赵六
陈七
```

如果没有：

```text
当前暂无满足条件的学生。
```

---

# 十三、功能7：查看Lab完成情况

输出：

```text
姓名
完成Lab数量
```

并查找：

```text
Lab完成数量最多的学生
```

进一步统计：

```text
完成Lab01的学生数量
完成Lab02的学生数量
...
```

可以先选择统计：

```text
Lab01～Lab08
```

的完成情况。

---

# 十四、功能8：查看AI兴趣方向

利用集合统计当前所有学生涉及的 AI 兴趣方向。

例如：

```text
========================================
AI兴趣方向统计
========================================

Computer Vision
Machine Learning
NLP
Robotics

共涉及4个不同方向。

========================================
```

---

# 十五、程序总体框架

程序可以从下面的结构开始：

```python
students = []

while True:

    print()
    print("=" * 50)
    print("AI课程学习数据管理系统")
    print("=" * 50)

    print("1. 添加学生")
    print("2. 查看全部学生")
    print("3. 查询学生")
    print("4. 修改学生成绩")
    print("5. 查看成绩统计")
    print("6. 查看优秀学生")
    print("7. 查看Lab完成情况")
    print("8. 查看AI兴趣方向")
    print("0. 退出系统")

    choice = input("请选择功能：")

    if choice == "1":

        # TODO：添加学生
        pass

    elif choice == "2":

        # TODO：查看所有学生
        pass

    elif choice == "3":

        # TODO：查询学生
        pass

    elif choice == "4":

        # TODO：修改成绩
        pass

    elif choice == "5":

        # TODO：成绩统计
        pass

    elif choice == "6":

        # TODO：优秀学生筛选
        pass

    elif choice == "7":

        # TODO：Lab完成情况
        pass

    elif choice == "8":

        # TODO：AI兴趣统计
        pass

    elif choice == "0":

        print("系统已退出。")
        break

    else:

        print("无效选择，请重新输入。")
```

---

# 十六、本任务的重点不是“把所有代码写在一起”

完成程序以后，请观察：

```text
添加学生代码
查询学生代码
统计成绩代码
修改成绩代码
```

是否越来越长。

还要观察：

```text
输入成绩并检查合法性
查找学生
显示学生信息
```

这些操作是否在多个位置重复出现。

请暂时不要急着解决这个问题。

因为这正是下一次实验：

# Lab 10：函数与模块化程序设计

要解决的问题。

---

# 十七、拓展任务：AI课程学习画像

创建：

```text
extension_student_profile.py
```

在 Task 3 的学生数据基础上，为每名学生生成简单的学习画像。

例如，根据：

```text
Python成绩
AI基础成绩
Lab完成数量
AI兴趣方向数量
```

给出评价。

---

## 情况1：综合优秀

满足：

```text
Python成绩 ≥ 90
AI成绩 ≥ 90
完成Lab数量 ≥ 8
```

输出：

```text
学习画像：综合表现优秀
```

---

## 情况2：编程能力突出

满足：

```text
Python成绩 ≥ 90
```

但 AI 成绩不足 90：

```text
学习画像：编程基础较强，建议加强AI基础学习
```

---

## 情况3：AI基础较好

满足：

```text
AI成绩 ≥ 90
```

但 Python 不足 90：

```text
学习画像：AI基础较好，建议加强Python编程实践
```

---

## 情况4：实验完成不足

如果：

```text
完成Lab数量 < 6
```

输出：

```text
学习画像：实践任务完成不足，建议增加编程练习
```

---

## 提高要求

自行增加至少一个评价因素，例如：

```text
AI兴趣方向数量
优秀课程数量
Lab完成比例
```

形成更加完整的学习画像。

---

# 十八、本次实训提交内容

本次实训至少完成：

```text
lab09-data-structures/
├── task01_structure_design.py
├── task02_data_analysis.py
└── task03_ai_course_manager.py
```

拓展任务可以创建：

```text
extension_student_profile.py
```

---

# 十九、实训检查

完成本次实训后，应能够：

* [ ] 根据数据特点选择合适的数据结构；
* [ ] 使用列表保存多条记录；
* [ ] 使用字典描述一个结构化对象；
* [ ] 使用集合保存唯一数据；
* [ ] 理解元组适合表示相对固定的数据；
* [ ] 使用列表和字典构成结构化记录集合；
* [ ] 使用嵌套数据结构组织复杂数据；
* [ ] 遍历列表中的字典；
* [ ] 查询指定结构化记录；
* [ ] 对结构化数据进行筛选；
* [ ] 完成最大值、最小值和平均值统计；
* [ ] 使用集合进行去重和汇总；
* [ ] 使用菜单组织多个程序功能；
* [ ] 对输入数据进行合法性检查；
* [ ] 完成数据添加和修改；
* [ ] 根据实际需求设计数据结构；
* [ ] 综合使用字符串、列表、元组、字典和集合；
* [ ] 完成一个具有一定规模的数据管理程序。

---

# 二十、本次实训知识路线

```text
实际问题
   ↓
分析数据
   ↓
选择数据结构
   ↓
list
   +
dict
   +
set
   +
tuple
   ↓
组合数据结构
   ↓
查询
   ↓
筛选
   ↓
排序
   ↓
统计
   ↓
修改
   ↓
菜单管理
   ↓
AI课程学习数据管理系统
```

---

# 二十一、阶段总结

Lab07～Lab09 主要解决了：

# 数据怎样组织和管理

学习路线为：

```text
Lab07
字符串 / 列表 / 元组
        ↓
一组数据
        ↓
Lab08
字典 / 集合
        ↓
结构化数据
        ↓
Lab09
组合数据结构
        ↓
完整数据管理程序
```

到目前为止，我们已经可以完成一个具有：

```text
数据录入
数据保存
数据查询
数据修改
数据筛选
数据统计
菜单交互
```

等功能的程序。

但是 Task 3 也会暴露一个新的问题：

```text
代码越来越长
      ↓
大量重复代码
      ↓
程序结构不清晰
      ↓
修改和维护越来越困难
```

因此下一阶段将进入：

# Lab 10：函数与模块化程序设计

下一次实验将重新设计 Lab09 中的管理系统，把：

```text
一大段程序
```

逐步拆分成：

```text
添加学生函数
查询学生函数
修改成绩函数
统计成绩函数
显示菜单函数
...
```

使程序从：

```text
“能够运行”
```

进一步发展为：

```text
“结构清晰、容易维护和复用”
```
