# Lab 10：函数与模块化程序设计

## 一、实训目的

通过本次实训掌握 Python 函数的定义、调用、参数传递和返回值等基本方法，理解函数在程序分解、代码复用和程序组织中的作用，并能够将前面已经完成的较大程序重新组织为职责明确的多个函数。

在 Lab 09 中，我们已经完成了一个具有多个功能的：

**AI课程学习数据管理系统**

程序中包含：

```text
添加学生
查询学生
修改成绩
成绩统计
优秀学生筛选
Lab完成情况统计
AI兴趣分析
```

如果将所有功能直接写在一个：

```python
while True:
```

中，程序会逐渐出现：

```text
代码过长
   ↓
重复代码增多
   ↓
功能边界不清晰
   ↓
修改困难
   ↓
维护困难
```

本次实验开始学习使用函数解决这些问题。

整体学习路线为：

```text
重复代码
   ↓
定义函数
   ↓
参数传递
   ↓
返回结果
   ↓
功能拆分
   ↓
函数复用
   ↓
主程序简化
   ↓
模块化程序设计
```

---

## 二、实训内容

本次实训主要包括：

1. 函数的定义与调用；
2. 参数和返回值；
3. 局部变量与程序功能分解；
4. 使用函数重构已有综合程序；
5. 初步理解模块化程序设计。

本次实训设置：

**3 个必做任务 + 1 个拓展任务。**

---

# 三、任务1：函数定义、参数与调用

## 1. 任务目标

掌握：

```text
def
函数名
参数
函数调用
return
```

等基本概念。

---

## 2. 创建程序

创建：

```text
task01_function_basics.py
```

首先定义最简单的函数：

```python
def show_welcome():
    print("=" * 40)
    print("欢迎进入Python程序设计实训")
    print("=" * 40)
```

调用：

```python
show_welcome()
```

观察：

> 定义函数本身并不会自动执行其中的代码，只有调用函数时，函数内部代码才会运行。

---

## 3. 带参数的函数

定义：

```python
def greet_student(name):
    print(f"{name}，欢迎开始今天的Python实训！")
```

调用：

```python
greet_student("张三")
greet_student("李四")
```

观察：

同一个函数可以接收不同的数据完成相同类型的任务。

---

## 4. 多个参数

定义：

```python
def show_student(name, python_score):
    print(f"姓名：{name}")
    print(f"Python成绩：{python_score}")
```

调用：

```python
show_student("张三", 88)
show_student("李四", 95)
```

---

## 5. 使用return返回结果

定义：

```python
def calculate_average(score1, score2):
    average = (score1 + score2) / 2
    return average
```

调用：

```python
result = calculate_average(88, 92)

print(f"平均成绩：{result:.2f}")
```

注意：

```text
print()
```

主要负责：

```text
显示结果
```

而：

```text
return
```

负责：

```text
把计算结果返回给函数调用位置
```

---

## 6. 比较print和return

观察：

```python
def add1(a, b):
    print(a + b)
```

和：

```python
def add2(a, b):
    return a + b
```

调用：

```python
result1 = add1(10, 20)
result2 = add2(10, 20)

print(result1)
print(result2)
```

观察两个结果。

思考：

> 为什么用于“计算”的函数通常更适合返回结果，而不是只在函数内部打印结果？

---

## 7. AI场景函数

定义：

```python
def evaluate_accuracy(accuracy):

    if accuracy >= 0.95:
        return "Excellent"

    elif accuracy >= 0.90:
        return "Good"

    elif accuracy >= 0.80:
        return "Acceptable"

    else:
        return "Needs Improvement"
```

调用：

```python
accuracy = float(input("请输入Accuracy："))

level = evaluate_accuracy(accuracy)

print(f"模型评价：{level}")
```

---

## 8. 数据合法性函数

前面多个 Lab 中经常出现：

```python
if 0 <= score <= 100:
```

可以封装为：

```python
def is_valid_score(score):
    return 0 <= score <= 100
```

使用：

```python
score = float(input("请输入成绩："))

if is_valid_score(score):
    print("成绩有效")
else:
    print("成绩无效")
```

---

## 9. 思考

回答：

1. 为什么要使用函数？
2. 参数有什么作用？
3. 一个函数能否有多个参数？
4. `return` 与 `print()` 有什么不同？
5. 同一个函数能否调用多次？

---

# 四、任务2：函数分解与数据处理

## 1. 任务目标

进一步掌握：

```text
参数传递
返回值
列表作为参数
字典作为参数
函数职责划分
局部变量
```

理解：

> 一个函数最好完成一个相对明确的任务。

---

## 2. 创建程序

创建：

```text
task02_function_design.py
```

准备：

```python
students = [
    {
        "student_id": "20260001",
        "name": "张三",
        "python_score": 88,
        "ai_score": 92
    },
    {
        "student_id": "20260002",
        "name": "李四",
        "python_score": 95,
        "ai_score": 90
    },
    {
        "student_id": "20260003",
        "name": "王五",
        "python_score": 76,
        "ai_score": 82
    }
]
```

---

## 3. 函数1：显示学生信息

定义：

```python
def show_student(student):

    print(f"学号：{student['student_id']}")
    print(f"姓名：{student['name']}")
    print(f"Python成绩：{student['python_score']}")
    print(f"AI成绩：{student['ai_score']}")
```

调用：

```python
show_student(students[0])
```

---

## 4. 函数2：查询学生

定义：

```python
def find_student(students, student_id):

    for student in students:

        if student["student_id"] == student_id:
            return student

    return None
```

调用：

```python
target_id = input("请输入查询学号：")

student = find_student(students, target_id)

if student is not None:
    show_student(student)
else:
    print("未找到该学生。")
```

这里出现了一个非常重要的设计：

```text
find_student()
```

只负责：

```text
查找
```

而：

```text
show_student()
```

负责：

```text
显示
```

两个函数职责不同。

---

## 5. 函数3：计算平均成绩

定义：

```python
def calculate_average(students, score_key):

    total = 0

    for student in students:
        total += student[score_key]

    return total / len(students)
```

调用：

```python
python_average = calculate_average(
    students,
    "python_score"
)

ai_average = calculate_average(
    students,
    "ai_score"
)

print(f"Python平均成绩：{python_average:.2f}")
print(f"AI平均成绩：{ai_average:.2f}")
```

思考：

> 为什么同一个函数可以同时用于计算 Python 成绩和 AI 成绩？

---

## 6. 函数4：查找最高成绩学生

定义：

```python
def find_best_student(students, score_key):

    best_student = students[0]

    for student in students:

        if student[score_key] > best_student[score_key]:
            best_student = student

    return best_student
```

调用：

```python
best_python_student = find_best_student(
    students,
    "python_score"
)

print(
    f"Python成绩最高："
    f"{best_python_student['name']} "
    f"{best_python_student['python_score']}"
)
```

---

## 7. 局部变量

观察：

```python
def demo():
    value = 100
    print(value)
```

这里：

```text
value
```

是在函数内部创建的局部变量。

尝试：

```python
demo()

print(value)
```

观察程序运行结果。

理解：

> 函数内部定义的普通变量通常只在函数内部有效。

---

## 8. 不建议过度使用全局变量

例如：

```python
students = []
```

虽然函数可以直接使用外部变量，但为了使函数更加清晰、容易复用，更建议通过参数传入：

```python
def show_all_students(students):
    ...
```

而不是让函数过度依赖外部状态。

---

## 9. 函数设计原则

本课程现阶段建议遵循：

### 一个函数完成一个主要任务

例如：

```text
show_menu()
```

只负责：

```text
显示菜单
```

---

```text
find_student()
```

只负责：

```text
查询学生
```

---

```text
calculate_average()
```

只负责：

```text
计算平均值
```

---

尽量避免一个函数同时承担：

```text
输入
查询
修改
统计
输出
```

所有功能。

---

# 五、任务3：使用函数重构AI课程学习数据管理系统

## 1. 任务背景

在 Lab09 中，我们已经完成：

# AI课程学习数据管理系统

但程序主要采用：

```python
while True:

    if choice == "1":
        # 很多代码

    elif choice == "2":
        # 很多代码

    elif choice == "3":
        # 很多代码
```

随着功能增加，主程序会越来越长。

本任务要求：

> **保持 Lab09 的主要功能基本不变，使用函数重新设计程序结构。**

---

## 2. 创建程序

创建：

```text
task03_ai_course_manager_refactored.py
```

建议不要直接删除 Lab09 原程序。

保留原程序，并创建新的重构版本，以便比较：

```text
Lab09版本
    ↓
无函数的大程序

Lab10版本
    ↓
函数化重构程序
```

---

# 六、第一步：设计函数

建议至少设计以下函数：

```python
show_menu()
add_student()
show_all_students()
find_student()
query_student()
modify_score()
show_statistics()
show_excellent_students()
show_lab_progress()
show_ai_interests()
```

以及辅助函数：

```python
input_valid_score()
```

---

## 1. 显示菜单函数

```python
def show_menu():

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
```

---

# 七、第二步：封装成绩输入

Lab09 中添加学生和修改成绩都会使用：

```text
输入成绩
↓
判断是否合法
↓
错误则重新输入
```

这部分非常适合封装。

定义：

```python
def input_valid_score(prompt):

    while True:

        score = float(input(prompt))

        if 0 <= score <= 100:
            return score

        print("成绩必须在0～100之间，请重新输入。")
```

以后：

```python
python_score = input_valid_score(
    "请输入Python成绩："
)
```

即可完成输入验证。

这就是：

# 代码复用

---

# 八、第三步：封装学生查询

定义：

```python
def find_student(students, student_id):

    for student in students:

        if student["student_id"] == student_id:
            return student

    return None
```

以后：

```text
查询学生
修改学生
检查学号
```

等功能都可以复用这个函数。

---

# 九、第四步：添加学生函数

可以设计：

```python
def add_student(students):

    print()
    print("----- 添加学生 -----")

    student_id = input("请输入学号：")

    if find_student(students, student_id) is not None:
        print("该学号已经存在。")
        return

    name = input("请输入姓名：")

    python_score = input_valid_score(
        "请输入Python成绩："
    )

    ai_score = input_valid_score(
        "请输入AI基础成绩："
    )

    lab_text = input(
        "请输入已完成Lab，用逗号分隔："
    )

    interest_text = input(
        "请输入AI兴趣方向，用逗号分隔："
    )

    completed_labs = set(lab_text.split(","))
    ai_interests = set(interest_text.split(","))

    student = {
        "student_id": student_id,
        "name": name,
        "python_score": python_score,
        "ai_score": ai_score,
        "completed_labs": completed_labs,
        "ai_interests": ai_interests
    }

    students.append(student)

    print("学生添加成功。")
```

---

# 十、第五步：查看全部学生

定义：

```python
def show_all_students(students):

    if len(students) == 0:
        print("当前暂无学生数据。")
        return

    print()
    print("-" * 60)

    for student in students:

        print(
            f"{student['student_id']} | "
            f"{student['name']} | "
            f"Python={student['python_score']} | "
            f"AI={student['ai_score']} | "
            f"Lab={len(student['completed_labs'])}"
        )

    print("-" * 60)
```

---

# 十一、第六步：查询学生

设计：

```python
def query_student(students):

    student_id = input("请输入查询学号：")

    student = find_student(
        students,
        student_id
    )

    if student is None:

        print("未找到该学生。")
        return

    print()
    print("=" * 40)

    print(f"学号：{student['student_id']}")
    print(f"姓名：{student['name']}")
    print(f"Python成绩：{student['python_score']}")
    print(f"AI成绩：{student['ai_score']}")

    print(
        f"已完成Lab："
        f"{student['completed_labs']}"
    )

    print(
        f"AI兴趣："
        f"{student['ai_interests']}"
    )

    print("=" * 40)
```

---

# 十二、第七步：修改学生成绩

设计：

```python
def modify_score(students):

    student_id = input("请输入学号：")

    student = find_student(
        students,
        student_id
    )

    if student is None:
        print("未找到该学生。")
        return

    print("1. 修改Python成绩")
    print("2. 修改AI基础成绩")
    print("0. 返回")

    choice = input("请选择：")

    if choice == "1":

        student["python_score"] = input_valid_score(
            "请输入新的Python成绩："
        )

        print("修改成功。")

    elif choice == "2":

        student["ai_score"] = input_valid_score(
            "请输入新的AI成绩："
        )

        print("修改成功。")

    elif choice == "0":

        return

    else:

        print("无效选择。")
```

---

# 十三、第八步：成绩统计函数

定义：

```python
def show_statistics(students):

    if len(students) == 0:
        print("暂无数据可统计。")
        return

    python_scores = []
    ai_scores = []

    for student in students:

        python_scores.append(
            student["python_score"]
        )

        ai_scores.append(
            student["ai_score"]
        )

    print()
    print("=" * 40)
    print("课程成绩统计")
    print("=" * 40)

    print(
        f"学生人数：{len(students)}"
    )

    print(
        f"Python平均成绩："
        f"{sum(python_scores) / len(python_scores):.2f}"
    )

    print(
        f"Python最高成绩：{max(python_scores)}"
    )

    print(
        f"Python最低成绩：{min(python_scores)}"
    )

    print(
        f"AI平均成绩："
        f"{sum(ai_scores) / len(ai_scores):.2f}"
    )

    print(
        f"AI最高成绩：{max(ai_scores)}"
    )

    print(
        f"AI最低成绩：{min(ai_scores)}"
    )

    print("=" * 40)
```

---

# 十四、第九步：优秀学生函数

规定：

```text
Python成绩 ≥ 90
且
AI成绩 ≥ 90
```

为综合优秀。

定义：

```python
def show_excellent_students(students):

    found = False

    print()
    print("综合优秀学生：")

    for student in students:

        if (
            student["python_score"] >= 90
            and student["ai_score"] >= 90
        ):

            print(
                f"{student['student_id']} "
                f"{student['name']}"
            )

            found = True

    if not found:
        print("当前暂无综合优秀学生。")
```

---

# 十五、第十步：Lab完成情况

定义：

```python
def show_lab_progress(students):

    if len(students) == 0:
        print("暂无学生数据。")
        return

    print()
    print("Lab完成情况：")

    for student in students:

        print(
            f"{student['name']}："
            f"{len(student['completed_labs'])} 个"
        )
```

进一步可以统计：

```text
完成Lab最多的学生
```

---

# 十六、第十一步：AI兴趣方向统计

定义：

```python
def show_ai_interests(students):

    all_interests = set()

    for student in students:

        all_interests = (
            all_interests
            | student["ai_interests"]
        )

    if len(all_interests) == 0:

        print("暂无AI兴趣方向数据。")
        return

    print()
    print("当前AI兴趣方向：")

    for interest in all_interests:
        print(interest)

    print(
        f"共涉及 {len(all_interests)} 个方向。"
    )
```

---

# 十七、重构后的主程序

完成上述函数以后，主程序可以变成：

```python
students = []

while True:

    show_menu()

    choice = input("请选择功能：")

    if choice == "1":

        add_student(students)

    elif choice == "2":

        show_all_students(students)

    elif choice == "3":

        query_student(students)

    elif choice == "4":

        modify_score(students)

    elif choice == "5":

        show_statistics(students)

    elif choice == "6":

        show_excellent_students(students)

    elif choice == "7":

        show_lab_progress(students)

    elif choice == "8":

        show_ai_interests(students)

    elif choice == "0":

        print("系统已退出。")
        break

    else:

        print("无效选择，请重新输入。")
```

观察主程序与 Lab09 相比发生了什么变化。

---

# 十八、Lab09与Lab10程序比较

## Lab09

主程序中存在大量：

```text
输入
判断
遍历
修改
统计
输出
```

具体代码。

整体结构类似：

```text
主程序
├── 添加学生的大段代码
├── 查询学生的大段代码
├── 修改成绩的大段代码
├── 统计的大段代码
└── 其他大量代码
```

---

## Lab10

结构变成：

```text
函数
├── show_menu()
├── add_student()
├── find_student()
├── query_student()
├── modify_score()
├── show_statistics()
├── show_excellent_students()
├── show_lab_progress()
└── show_ai_interests()

主程序
└── 负责调用函数
```

因此形成：

```text
具体功能
    ↓
函数负责

程序流程
    ↓
主程序负责
```

这就是模块化程序设计的基本思想。

---

# 十九、代码复用分析

观察：

```python
find_student()
```

至少可以被：

```text
查询学生
修改学生
检查学号是否重复
```

多个功能调用。

而：

```python
input_valid_score()
```

可以被：

```text
添加学生
修改Python成绩
修改AI成绩
```

反复调用。

这说明：

> 函数不仅能够缩短主程序，更重要的是可以减少重复代码。

---

# 二十、拓展任务：将程序拆分为多个模块

当一个 `.py` 文件中的函数继续增加时，即使已经使用函数，文件仍然可能越来越长。

因此可以进一步将函数保存到不同的 Python 文件中。

创建目录结构：

```text
lab10-functions/
│
├── task03_ai_course_manager_refactored.py
│
└── extension_modules/
    ├── main.py
    ├── student_utils.py
    └── statistics_utils.py
```

---

## 1. student_utils.py

保存与学生管理相关的函数：

```python
def find_student(students, student_id):

    for student in students:

        if student["student_id"] == student_id:
            return student

    return None
```

还可以放入：

```text
add_student()
query_student()
modify_score()
```

---

## 2. statistics_utils.py

保存统计相关函数，例如：

```text
show_statistics()
show_excellent_students()
show_lab_progress()
show_ai_interests()
```

---

## 3. main.py

通过：

```python
from student_utils import find_student
```

或者：

```python
import student_utils
```

使用其他文件中的函数。

例如：

```python
from student_utils import find_student

students = [
    {
        "student_id": "20260001",
        "name": "张三"
    }
]

student = find_student(
    students,
    "20260001"
)

print(student)
```

---

## 4. 拓展目标

将 Task03 中的程序尝试拆分为：

```text
main.py
      ↓
控制系统整体流程

student_utils.py
      ↓
学生数据操作

statistics_utils.py
      ↓
统计分析功能
```

形成：

```text
多个.py文件
      ↓
各自负责不同功能
      ↓
通过import组合
      ↓
完整程序
```

本次只要求初步理解模块化，不要求设计复杂 Python 包。

---

# 二十一、本次实训提交内容

本次实训至少完成：

```text
lab10-functions/
├── task01_function_basics.py
├── task02_function_design.py
└── task03_ai_course_manager_refactored.py
```

拓展任务可以完成：

```text
extension_modules/
├── main.py
├── student_utils.py
└── statistics_utils.py
```

---

# 二十二、实训检查

完成本次实训后，应能够：

* [ ] 使用 `def` 定义函数；
* [ ] 正确调用函数；
* [ ] 理解函数参数的作用；
* [ ] 定义具有多个参数的函数；
* [ ] 使用 `return` 返回结果；
* [ ] 理解 `return` 与 `print()` 的基本区别；
* [ ] 将列表作为函数参数；
* [ ] 将字典作为函数参数；
* [ ] 理解局部变量的基本作用范围；
* [ ] 避免不必要地依赖全局变量；
* [ ] 根据程序功能拆分函数；
* [ ] 让一个函数承担相对明确的职责；
* [ ] 使用函数减少重复代码；
* [ ] 使用函数重构已有程序；
* [ ] 理解主程序与功能函数之间的关系；
* [ ] 初步理解模块化程序设计；
* [ ] 使用 `import` 调用其他 Python 文件中的函数；
* [ ] 比较函数化重构前后的代码结构差异。

---

# 二十三、本次实训知识路线

```text
较大的程序
   ↓
重复代码
   ↓
函数
   ↓
参数
   ↓
返回值
   ↓
函数职责
   ↓
代码复用
   ↓
功能拆分
   ↓
主程序简化
   ↓
多函数协作
   ↓
模块
   ↓
多文件程序
```

---

# 二十四、从Lab09到Lab10

这两个实验形成一个完整的程序设计过程：

```text
Lab09
先解决“程序能不能做出来”
          ↓
完成完整数据管理程序
          ↓
发现代码过长和重复

Lab10
再解决“程序应该怎样组织”
          ↓
提取函数
          ↓
减少重复
          ↓
功能分解
          ↓
程序结构更加清晰
```

因此：

```text
Lab09
更关注功能实现

Lab10
更关注代码组织
```

程序设计能力也开始从：

```text
会写代码
```

发展为：

```text
会设计代码结构
```

---

# 二十五、阶段衔接

完成 Lab10 后，我们已经具备：

```text
控制结构
     +
数据结构
     +
函数
     +
基本模块化
```

程序已经可以比较清晰地组织较复杂的数据管理逻辑。

但目前仍然存在一个重要问题：

```text
程序运行
   ↓
输入学生数据
   ↓
完成查询和统计
   ↓
关闭程序
   ↓
数据全部消失
```

也就是说，目前学生数据仍然只存在于：

```text
内存
```

中。

下一阶段将进入：

# Lab 11：文件、异常与数据处理

届时将在 Lab10 程序基础上进一步解决：

```text
数据如何永久保存？
        ↓
文件

程序遇到错误如何处理？
        ↓
异常

程序重新运行后如何恢复数据？
        ↓
文件读取
```

最终使管理系统从：

```text
只能在一次运行过程中使用
```

发展为：

```text
可以保存和恢复数据
```
