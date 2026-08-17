# Lab 12：面向对象程序设计综合应用

## 一、实训目的

通过本次实训掌握 Python 面向对象程序设计的基本思想，理解类、对象、属性和方法之间的关系，能够使用类封装数据和相关操作，并将前面基于列表、字典和函数实现的数据管理程序重构为面向对象程序。

在前面的 Lab 中，每名学生通常使用字典表示：

```python
student = {
    "student_id": "20260001",
    "name": "张三",
    "python_score": 88,
    "ai_score": 92
}
```

与学生有关的操作则通过独立函数完成：

```text
show_student()
find_student()
modify_score()
```

这种程序已经可以完成任务，但随着数据和功能越来越多，会出现：

```text
数据分散
   +
相关函数分散
   ↓
程序关系不够直观
```

面向对象程序设计提供了一种新的组织方式：

```text
数据
+
与这些数据相关的操作
        ↓
       对象
```

例如：

```python
class Student:
    ...
```

一个 `Student` 对象既保存：

```text
学号
姓名
成绩
Lab完成情况
AI兴趣
```

也可以提供：

```text
显示信息
修改成绩
判断是否优秀
计算Lab完成数量
```

等操作。

本次实训的整体学习路线为：

```text
类
 ↓
对象
 ↓
属性
 ↓
方法
 ↓
Student
 ↓
多个Student对象
 ↓
StudentManager
 ↓
文件持久化
 ↓
完整面向对象程序
```

---

## 二、实训内容

本次实训主要包括：

1. 类与对象的基本概念；
2. `__init__()` 构造方法；
3. 实例属性与实例方法；
4. 使用 `Student` 类封装学生数据；
5. 使用 `StudentManager` 类管理多个学生对象；
6. 将 Lab11 中的数据管理系统重构为面向对象程序；
7. 保留 CSV 文件读写与异常处理能力。

本次实训设置：

**3 个必做任务 + 1 个拓展任务。**

---

# 三、任务1：类与对象基础

## 1. 任务目标

掌握：

```text
class
对象
__init__()
self
属性
方法
```

等基本概念。

---

## 2. 创建程序

创建：

```text
task01_class_basics.py
```

首先定义一个简单的学生类：

```python
class Student:

    def __init__(self, name, major):
        self.name = name
        self.major = major
```

创建对象：

```python
student1 = Student(
    "张三",
    "人工智能"
)

student2 = Student(
    "李四",
    "人工智能"
)
```

输出：

```python
print(student1.name)
print(student1.major)

print(student2.name)
print(student2.major)
```

观察：

```text
student1
student2
```

是否保存了彼此独立的数据。

---

## 3. 理解类与对象

可以初步理解：

```text
Student
   ↓
类
   ↓
描述“学生应该有哪些数据和行为”
```

而：

```text
student1
student2
```

是根据 `Student` 类创建的：

```text
具体对象
```

例如：

```text
Student
   ↓
模板

张三
李四
王五
   ↓
具体对象
```

---

## 4. 增加方法

修改：

```python
class Student:

    def __init__(self, name, major):
        self.name = name
        self.major = major

    def show_info(self):
        print(f"姓名：{self.name}")
        print(f"专业：{self.major}")
```

调用：

```python
student1.show_info()
student2.show_info()
```

---

## 5. 增加成绩属性

继续修改：

```python
class Student:

    def __init__(
        self,
        name,
        major,
        python_score
    ):

        self.name = name
        self.major = major
        self.python_score = python_score

    def show_info(self):

        print(f"姓名：{self.name}")
        print(f"专业：{self.major}")
        print(
            f"Python成绩："
            f"{self.python_score}"
        )
```

---

## 6. 增加判断方法

定义：

```python
def is_python_excellent(self):

    return self.python_score >= 90
```

调用：

```python
if student1.is_python_excellent():

    print("Python课程成绩优秀")
```

这里：

```text
python_score
```

属于学生对象的数据，

而：

```text
is_python_excellent()
```

属于学生对象能够执行的操作。

---

## 7. 修改对象属性

可以直接：

```python
student1.python_score = 95
```

再输出：

```python
print(student1.python_score)
```

---

## 8. 使用方法修改成绩

更推荐将修改逻辑放入类中：

```python
def update_python_score(self, score):

    if 0 <= score <= 100:

        self.python_score = score
        return True

    return False
```

调用：

```python
success = student1.update_python_score(
    95
)

if success:
    print("成绩修改成功")
else:
    print("成绩无效")
```

---

## 9. 思考

回答：

1. 类和对象有什么区别？
2. `__init__()` 什么时候执行？
3. `self` 表示什么？
4. 属性和普通变量有什么区别？
5. 方法和普通函数有什么联系和区别？
6. 为什么与学生有关的操作可以放到 `Student` 类中？

---

# 四、任务2：设计完整Student类

## 1. 任务目标

将前面一直使用的学生字典：

```python
student = {
    ...
}
```

重构为：

```python
student = Student(...)
```

让学生的数据和基本行为组织在一起。

---

## 2. 创建程序

创建：

```text
task02_student_class.py
```

---

## 3. Student类应包含的数据

每名学生至少保存：

```text
学号
姓名
专业
Python成绩
AI基础成绩
已完成Lab
AI兴趣方向
```

因此可以定义：

```python
class Student:

    def __init__(
        self,
        student_id,
        name,
        major,
        python_score,
        ai_score,
        completed_labs=None,
        ai_interests=None
    ):

        self.student_id = student_id
        self.name = name
        self.major = major

        self.python_score = python_score
        self.ai_score = ai_score

        if completed_labs is None:
            completed_labs = set()

        if ai_interests is None:
            ai_interests = set()

        self.completed_labs = completed_labs
        self.ai_interests = ai_interests
```

---

## 4. 为什么默认值使用None

不建议直接写：

```python
def __init__(
    self,
    completed_labs=set()
):
```

本阶段只需要记住：

> 对于列表、集合、字典等可变对象，默认参数更适合先使用 `None`，再在函数内部创建新对象。

不要求深入讨论 Python 底层机制。

---

# 五、设计Student方法

建议至少设计以下方法。

---

## 1. 显示基本信息

```python
def show_info(self):

    print("=" * 40)

    print(f"学号：{self.student_id}")
    print(f"姓名：{self.name}")
    print(f"专业：{self.major}")

    print(
        f"Python成绩："
        f"{self.python_score}"
    )

    print(
        f"AI基础成绩："
        f"{self.ai_score}"
    )

    print(
        f"完成Lab数量："
        f"{len(self.completed_labs)}"
    )

    print(
        f"AI兴趣："
        f"{self.ai_interests}"
    )

    print("=" * 40)
```

---

## 2. 修改Python成绩

```python
def update_python_score(self, score):

    if 0 <= score <= 100:

        self.python_score = score
        return True

    return False
```

---

## 3. 修改AI成绩

```python
def update_ai_score(self, score):

    if 0 <= score <= 100:

        self.ai_score = score
        return True

    return False
```

---

## 4. 判断是否综合优秀

规定：

```text
Python成绩 ≥ 90
且
AI成绩 ≥ 90
```

定义：

```python
def is_excellent(self):

    return (
        self.python_score >= 90
        and self.ai_score >= 90
    )
```

---

## 5. 返回Lab完成数量

```python
def completed_lab_count(self):

    return len(
        self.completed_labs
    )
```

---

## 6. 添加已完成Lab

```python
def add_completed_lab(self, lab_name):

    self.completed_labs.add(
        lab_name
    )
```

例如：

```python
student.add_completed_lab(
    "Lab12"
)
```

---

## 7. 添加AI兴趣方向

```python
def add_ai_interest(self, interest):

    self.ai_interests.add(
        interest
    )
```

---

# 六、创建Student对象

例如：

```python
student1 = Student(
    student_id="20260001",
    name="张三",
    major="人工智能",
    python_score=88,
    ai_score=92,
    completed_labs={
        "Lab01",
        "Lab02",
        "Lab03"
    },
    ai_interests={
        "Computer Vision",
        "Machine Learning"
    }
)
```

调用：

```python
student1.show_info()
```

---

# 七、比较字典与对象

## 字典方式

原来：

```python
student = {
    "name": "张三",
    "python_score": 88
}
```

访问：

```python
student["name"]
```

---

## 对象方式

现在：

```python
student = Student(...)
```

访问：

```python
student.name
```

并且对象还能够直接：

```python
student.show_info()

student.update_python_score(95)

student.is_excellent()
```

因此对象可以理解为：

```text
数据
+
与这些数据紧密相关的方法
```

---

# 八、任务3：面向对象的AI课程学习数据管理系统

## 1. 任务背景

在 Lab11 中，系统主要采用：

```text
list
+
dict
+
functions
+
CSV
```

结构。

例如：

```python
students = [
    {
        "student_id": "...",
        "name": "...",
        ...
    }
]
```

并通过：

```text
add_student()
find_student()
save_students()
load_students()
```

等函数操作这些数据。

本任务要求将整个系统进一步重构为：

```text
Student
+
StudentManager
```

其中：

```text
Student
```

负责：

> 一名学生的数据和基本行为。

而：

```text
StudentManager
```

负责：

> 多名学生的管理、查询、统计、文件读写等系统功能。

---

## 2. 创建程序

创建：

```text
task03_oop_course_manager.py
```

---

# 九、Student类职责

`Student` 主要负责：

```text
保存个人信息
显示个人信息
修改成绩
Lab完成情况
优秀状态判断
```

不要让 `Student` 负责：

```text
管理全部学生
查找其他学生
读取整个CSV
显示系统菜单
```

这些应由：

```text
StudentManager
```

负责。

---

# 十、StudentManager类

可以首先设计：

```python
class StudentManager:

    def __init__(self, filename):

        self.filename = filename
        self.students = []
```

其中：

```text
filename
```

保存数据文件路径，

而：

```text
students
```

保存：

```text
Student对象列表
```

即：

```python
self.students = [
    Student(...),
    Student(...),
    Student(...)
]
```

---

# 十一、查找学生方法

定义：

```python
def find_student(
    self,
    student_id
):

    for student in self.students:

        if (
            student.student_id
            == student_id
        ):

            return student

    return None
```

注意现在访问方式已经从：

```python
student["student_id"]
```

变成：

```python
student.student_id
```

---

# 十二、添加学生方法

可以设计：

```python
def add_student(self):

    print()
    print("----- 添加学生 -----")

    student_id = input(
        "请输入学号："
    )

    if (
        self.find_student(student_id)
        is not None
    ):

        print(
            "该学号已经存在。"
        )
        return

    name = input(
        "请输入姓名："
    )

    major = input(
        "请输入专业："
    )

    python_score = self.input_valid_score(
        "请输入Python成绩："
    )

    ai_score = self.input_valid_score(
        "请输入AI基础成绩："
    )

    lab_text = input(
        "请输入已完成Lab，"
        "用逗号分隔："
    )

    interest_text = input(
        "请输入AI兴趣方向，"
        "用逗号分隔："
    )

    completed_labs = set()

    if lab_text.strip():

        completed_labs = set(
            lab_text.split(",")
        )

    ai_interests = set()

    if interest_text.strip():

        ai_interests = set(
            interest_text.split(",")
        )

    student = Student(
        student_id=student_id,
        name=name,
        major=major,
        python_score=python_score,
        ai_score=ai_score,
        completed_labs=completed_labs,
        ai_interests=ai_interests
    )

    self.students.append(
        student
    )

    self.save_data()

    print("学生添加成功。")
```

---

# 十三、成绩输入方法

将 Lab11 中的输入检查进一步作为 Manager 的辅助方法：

```python
def input_valid_score(
    self,
    prompt
):

    while True:

        try:

            score = float(
                input(prompt)
            )

            if 0 <= score <= 100:

                return score

            print(
                "成绩必须在0～100之间。"
            )

        except ValueError:

            print(
                "请输入有效数字。"
            )
```

---

# 十四、查看全部学生

设计：

```python
def show_all_students(self):

    if len(self.students) == 0:

        print(
            "当前暂无学生数据。"
        )
        return

    print()
    print("-" * 70)

    for student in self.students:

        print(
            f"{student.student_id} | "
            f"{student.name} | "
            f"Python={student.python_score} | "
            f"AI={student.ai_score} | "
            f"Lab={student.completed_lab_count()}"
        )

    print("-" * 70)
```

---

# 十五、查询学生

```python
def query_student(self):

    student_id = input(
        "请输入查询学号："
    )

    student = self.find_student(
        student_id
    )

    if student is None:

        print(
            "未找到该学生。"
        )
        return

    student.show_info()
```

这里可以看到：

```text
StudentManager
```

负责：

```text
查找对象
```

找到以后：

```text
Student
```

负责：

```text
显示自己的信息
```

这体现了对象之间的协作。

---

# 十六、修改学生成绩

设计：

```python
def modify_score(self):

    student_id = input(
        "请输入学生学号："
    )

    student = self.find_student(
        student_id
    )

    if student is None:

        print(
            "未找到该学生。"
        )
        return

    print("1. 修改Python成绩")
    print("2. 修改AI成绩")
    print("0. 返回")

    choice = input(
        "请选择："
    )

    if choice == "1":

        score = self.input_valid_score(
            "请输入新的Python成绩："
        )

        student.update_python_score(
            score
        )

        self.save_data()

        print("修改成功。")

    elif choice == "2":

        score = self.input_valid_score(
            "请输入新的AI成绩："
        )

        student.update_ai_score(
            score
        )

        self.save_data()

        print("修改成功。")

    elif choice == "0":

        return

    else:

        print("无效选择。")
```

---

# 十七、成绩统计

设计：

```python
def show_statistics(self):

    if len(self.students) == 0:

        print(
            "暂无数据可统计。"
        )
        return

    python_scores = []
    ai_scores = []

    for student in self.students:

        python_scores.append(
            student.python_score
        )

        ai_scores.append(
            student.ai_score
        )

    print()
    print("=" * 45)
    print("课程成绩统计")
    print("=" * 45)

    print(
        f"学生人数："
        f"{len(self.students)}"
    )

    print(
        f"Python平均成绩："
        f"{sum(python_scores) / len(python_scores):.2f}"
    )

    print(
        f"Python最高成绩："
        f"{max(python_scores)}"
    )

    print(
        f"Python最低成绩："
        f"{min(python_scores)}"
    )

    print(
        f"AI平均成绩："
        f"{sum(ai_scores) / len(ai_scores):.2f}"
    )

    print(
        f"AI最高成绩："
        f"{max(ai_scores)}"
    )

    print(
        f"AI最低成绩："
        f"{min(ai_scores)}"
    )

    print("=" * 45)
```

---

# 十八、优秀学生

```python
def show_excellent_students(
    self
):

    excellent_students = []

    for student in self.students:

        if student.is_excellent():

            excellent_students.append(
                student
            )

    if len(excellent_students) == 0:

        print(
            "当前暂无综合优秀学生。"
        )
        return

    print()
    print("综合优秀学生：")

    for student in excellent_students:

        print(
            f"{student.student_id} "
            f"{student.name}"
        )
```

---

# 十九、AI兴趣方向统计

设计：

```python
def show_ai_interests(self):

    all_interests = set()

    for student in self.students:

        all_interests = (
            all_interests
            | student.ai_interests
        )

    if len(all_interests) == 0:

        print(
            "暂无AI兴趣方向数据。"
        )
        return

    print()
    print("AI兴趣方向：")

    for interest in all_interests:

        print(interest)

    print(
        f"共涉及 "
        f"{len(all_interests)} "
        f"个不同方向。"
    )
```

---

# 二十、保存Student对象到CSV

对象不能直接写入 CSV，需要先转换为：

```text
字符串 / 数值
```

定义：

```python
import csv
```

然后：

```python
def save_data(self):

    with open(
        self.filename,
        "w",
        newline="",
        encoding="utf-8-sig"
    ) as file:

        fieldnames = [
            "student_id",
            "name",
            "major",
            "python_score",
            "ai_score",
            "completed_labs",
            "ai_interests"
        ]

        writer = csv.DictWriter(
            file,
            fieldnames=fieldnames
        )

        writer.writeheader()

        for student in self.students:

            writer.writerow(
                {
                    "student_id":
                        student.student_id,

                    "name":
                        student.name,

                    "major":
                        student.major,

                    "python_score":
                        student.python_score,

                    "ai_score":
                        student.ai_score,

                    "completed_labs":
                        "|".join(
                            student.completed_labs
                        ),

                    "ai_interests":
                        "|".join(
                            student.ai_interests
                        )
                }
            )
```

---

# 二十一、从CSV恢复Student对象

这是本次实验中一个非常重要的转换过程：

```text
CSV一行
   ↓
字典
   ↓
Student(...)
   ↓
Student对象
```

定义：

```python
def load_data(self):

    self.students = []

    try:

        with open(
            self.filename,
            "r",
            encoding="utf-8-sig"
        ) as file:

            reader = csv.DictReader(
                file
            )

            for row in reader:

                completed_labs = set()

                if row["completed_labs"]:

                    completed_labs = set(
                        row[
                            "completed_labs"
                        ].split("|")
                    )

                ai_interests = set()

                if row["ai_interests"]:

                    ai_interests = set(
                        row[
                            "ai_interests"
                        ].split("|")
                    )

                student = Student(
                    student_id=
                        row["student_id"],

                    name=
                        row["name"],

                    major=
                        row["major"],

                    python_score=
                        float(
                            row[
                                "python_score"
                            ]
                        ),

                    ai_score=
                        float(
                            row[
                                "ai_score"
                            ]
                        ),

                    completed_labs=
                        completed_labs,

                    ai_interests=
                        ai_interests
                )

                self.students.append(
                    student
                )

    except FileNotFoundError:

        print(
            "未找到数据文件，"
            "将从空数据开始。"
        )
```

---

# 二十二、显示菜单

可以作为 Manager 的方法：

```python
def show_menu(self):

    print()
    print("=" * 50)
    print(
        "AI课程学习数据管理系统"
    )
    print("=" * 50)

    print("1. 添加学生")
    print("2. 查看全部学生")
    print("3. 查询学生")
    print("4. 修改学生成绩")
    print("5. 查看成绩统计")
    print("6. 查看优秀学生")
    print("7. 查看AI兴趣方向")
    print("0. 保存并退出")
```

---

# 二十三、run()方法

进一步可以把整个菜单循环也放入：

```python
def run(self):

    self.load_data()

    while True:

        self.show_menu()

        choice = input(
            "请选择功能："
        )

        if choice == "1":

            self.add_student()

        elif choice == "2":

            self.show_all_students()

        elif choice == "3":

            self.query_student()

        elif choice == "4":

            self.modify_score()

        elif choice == "5":

            self.show_statistics()

        elif choice == "6":

            self.show_excellent_students()

        elif choice == "7":

            self.show_ai_interests()

        elif choice == "0":

            self.save_data()

            print(
                "数据已保存，系统退出。"
            )

            break

        else:

            print(
                "无效选择，请重新输入。"
            )
```

---

# 二十四、最终主程序

完成以上类以后，主程序可以非常简洁：

```python
DATA_FILE = "data/students.csv"

manager = StudentManager(
    DATA_FILE
)

manager.run()
```

这与 Lab09 中的大量菜单逻辑形成明显对比。

---

# 二十五、程序结构对比

## Lab09

```text
students
+
大量菜单代码
+
数据处理代码
```

---

## Lab10

```text
students
+
多个函数
+
main
```

---

## Lab11

```text
students
+
函数
+
CSV
+
异常处理
```

---

## Lab12

进一步变成：

```text
Student
        ↓
描述一名学生

StudentManager
        ↓
管理所有学生

CSV
        ↓
保存对象数据

main
        ↓
启动系统
```

整体关系：

```text
main
 ↓
StudentManager
 ↓
多个Student
 ↓
CSV文件
```

---

# 二十六、面向对象的核心理解

本次实验不要求记忆复杂的面向对象理论。

现阶段重点理解：

## 类

描述：

```text
某一类对象应该有哪些数据和行为
```

---

## 对象

类创建出来的具体实例。

例如：

```text
Student
       ↓
张三
李四
王五
```

---

## 属性

对象保存的数据。

例如：

```text
student.name
student.python_score
```

---

## 方法

对象能够执行的操作。

例如：

```text
student.show_info()

student.update_python_score()

student.is_excellent()
```

---

## 封装

将：

```text
数据
+
与数据相关的操作
```

组织在一起。

---

# 二十七、为什么要使用StudentManager

为什么不把所有方法都放进：

```python
class Student
```

？

因为：

```text
Student
```

表示的是：

> 一名学生。

它适合负责：

```text
自己的信息
自己的成绩
自己的Lab完成情况
```

但：

```text
查找所有学生
统计全班平均成绩
从CSV加载所有学生
```

并不是某一个学生自己的职责。

因此需要：

```text
StudentManager
```

负责：

```text
管理多个Student对象
```

这体现了：

> 不同对象承担不同职责。

---

# 二十八、测试要求

至少完成以下测试。

## 测试1：创建对象

手动创建：

```text
3个Student对象
```

检查：

```text
属性是否独立
方法是否正常
```

---

## 测试2：添加学生

通过 StudentManager 添加至少3名学生。

检查：

```text
students.csv
```

是否正常保存。

---

## 测试3：重新启动程序

关闭程序后重新运行。

确认：

```text
Student对象是否能够从CSV恢复。
```

---

## 测试4：修改成绩

修改一名学生的成绩。

重新启动程序。

确认修改是否保存。

---

## 测试5：优秀学生

测试：

```text
Python ≥ 90
AI ≥ 90
```

的学生能否被正确筛选。

---

## 测试6：非法数据

尝试输入：

```text
abc
-10
120
```

作为成绩。

程序应能够正常处理，而不是直接崩溃。

---

# 二十九、拓展任务：多文件面向对象程序

当：

```text
Student
StudentManager
main
```

全部写在一个文件中时，程序仍然可能比较长。

因此可以进一步拆分为：

```text
extension_oop_project/
│
├── main.py
├── student.py
├── student_manager.py
└── data/
    └── students.csv
```

---

## 1. student.py

保存：

```python
class Student:
    ...
```

---

## 2. student_manager.py

保存：

```python
class StudentManager:
    ...
```

并导入：

```python
from student import Student
```

---

## 3. main.py

只保留：

```python
from student_manager import StudentManager


DATA_FILE = "data/students.csv"

manager = StudentManager(
    DATA_FILE
)

manager.run()
```

---

## 4. 观察程序结构

形成：

```text
main.py
   ↓
StudentManager
   ↓
Student
   ↓
CSV
```

不同文件承担不同职责。

---

## 5. 提高要求

自行增加：

```text
删除学生
修改AI兴趣
添加已完成Lab
按成绩排序
按姓名查询
```

等功能。

但要求：

> 新增功能时，应思考这个功能应该属于 `Student`，还是属于 `StudentManager`。

---

# 三十、本次实训提交内容

本次实训至少完成：

```text
lab12-oop-application/
│
├── task01_class_basics.py
├── task02_student_class.py
├── task03_oop_course_manager.py
│
└── data/
    └── students.csv
```

拓展任务可以完成：

```text
extension_oop_project/
│
├── main.py
├── student.py
├── student_manager.py
│
└── data/
    └── students.csv
```

---

# 三十一、实训检查

完成本次实训后，应能够：

* [ ] 理解类和对象的基本区别；
* [ ] 使用 `class` 定义类；
* [ ] 使用 `__init__()` 初始化对象；
* [ ] 理解 `self` 的基本作用；
* [ ] 创建对象并访问属性；
* [ ] 为类定义实例方法；
* [ ] 通过方法修改对象状态；
* [ ] 通过方法返回对象相关结果；
* [ ] 理解数据和行为可以封装在对象中；
* [ ] 使用 `Student` 类描述学生；
* [ ] 使用列表保存多个 Student 对象；
* [ ] 使用 `StudentManager` 管理多个对象；
* [ ] 理解不同类应承担不同职责；
* [ ] 将字典程序重构为对象程序；
* [ ] 将 CSV 数据恢复为 Student 对象；
* [ ] 将 Student 对象保存到 CSV；
* [ ] 综合使用类、函数、文件和异常处理；
* [ ] 使用多个对象协作完成较完整程序；
* [ ] 初步完成多文件面向对象程序设计。

---

# 三十二、本次实训知识路线

```text
数据
 ↓
字典
 ↓
函数操作数据
 ↓
类
 ↓
对象
 ↓
属性
 ↓
方法
 ↓
封装
 ↓
Student
 ↓
多个Student对象
 ↓
StudentManager
 ↓
CSV持久化
 ↓
完整面向对象应用
```

---

# 三十三、Lab09～Lab12程序演进

整个连续项目已经经历四个阶段：

```text
Lab09
数据结构
   ↓
把系统功能实现出来

Lab10
函数
   ↓
把程序功能组织起来

Lab11
文件与异常
   ↓
让数据能够保存和恢复

Lab12
面向对象
   ↓
重新组织数据和行为
```

可以概括为：

```text
Lab09
能完成任务

   ↓

Lab10
代码结构清晰

   ↓

Lab11
数据能够持久化

   ↓

Lab12
程序对象关系更加清晰
```

---

# 三十四、第二阶段总结

Lab07～Lab12 构成了课程的第二阶段：

# 程序设计与数据组织

学习路径为：

```text
Lab07
字符串 / 列表 / 元组
        ↓
一组数据

Lab08
字典 / 集合
        ↓
结构化数据

Lab09
数据结构综合
        ↓
数据管理系统

Lab10
函数与模块化
        ↓
程序结构重构

Lab11
文件与异常
        ↓
数据持久化

Lab12
面向对象
        ↓
对象化程序设计
```

完成本阶段后，应已经能够使用 Python 独立完成具有：

```text
结构化数据
数据查询
数据修改
统计分析
函数组织
文件存储
异常处理
类与对象
```

等功能的中等规模程序。

---

# 三十五、下一阶段

完成 Lab12 后，课程将结束以“管理系统”为主线的程序设计训练。

下一阶段正式进入：

# 数据处理与人工智能基础

首先学习：

# Lab 13：NumPy科学计算与数据分析

程序的数据处理方式将从：

```text
Python list
+
for循环
```

逐步过渡到：

```text
NumPy ndarray
+
向量化运算
```

例如原来的：

```python
scores = [
    88,
    92,
    85,
    90
]
```

将进一步发展为：

```python
import numpy as np

scores = np.array(
    [88, 92, 85, 90]
)
```

并开始处理：

```text
一维数据
二维数据
矩阵
多维数组
AI样本与特征
```

课程也将由：

```text
通用Python程序设计
```

正式过渡到：

```text
面向数据与人工智能的Python应用
```
