# Lab 11：文件、异常与数据处理

## 一、实训目的

通过本次实训掌握 Python 文件读写的基本方法，理解程序运行过程中“内存数据”和“文件数据”的区别，能够使用文本文件和 CSV 文件保存、读取和处理结构化数据，并掌握基本异常处理方法。

在 Lab 10 中，我们已经将 AI 课程学习数据管理系统重构为多个函数，例如：

```text
add_student()
find_student()
query_student()
modify_score()
show_statistics()
...
```

程序结构已经更加清晰。

但是目前仍然存在一个明显问题：

```text
运行程序
   ↓
输入学生数据
   ↓
完成查询和统计
   ↓
关闭程序
   ↓
students列表中的数据全部消失
```

这是因为：

```python
students = []
```

中的数据只存在于程序运行时的内存中。

本次实训将进一步解决：

```text
数据如何保存？
      ↓
文件写入

程序重新运行后如何恢复？
      ↓
文件读取

结构化数据如何保存？
      ↓
CSV

文件或输入出现问题怎么办？
      ↓
异常处理
```

最终将 Lab10 的管理系统升级为一个具有基本**数据持久化能力**的程序。

---

## 二、实训内容

本次实训主要包括：

1. 文本文件的打开、读取和写入；
2. 使用 `with open()` 管理文件；
3. CSV 结构化数据的读取与写入；
4. 使用 `try-except` 处理常见异常；
5. 将内存中的学生数据保存到文件；
6. 程序启动时自动恢复已有数据；
7. 综合升级 AI 课程学习数据管理系统。

本次实训设置：

**3 个必做任务 + 1 个拓展任务。**

---

# 三、任务1：文本文件读写基础

## 1. 任务目标

掌握 Python 文件操作的基本流程：

```text
打开文件
   ↓
读取 / 写入
   ↓
关闭文件
```

并掌握推荐的：

```python
with open(...)
```

文件操作方式。

---

## 2. 创建程序

创建：

```text
task01_text_file.py
```

---

## 3. 写入文本文件

首先运行：

```python
with open(
    "learning_record.txt",
    "w",
    encoding="utf-8"
) as file:

    file.write("Python程序设计实训\n")
    file.write("Lab11：文件、异常与数据处理\n")
    file.write("开始学习文件操作\n")
```

运行程序后观察当前目录中是否生成：

```text
learning_record.txt
```

打开文件查看内容。

---

## 4. 理解文件打开模式

常见模式包括：

| 模式    | 含义          |
| ----- | ----------- |
| `"r"` | 读取文件        |
| `"w"` | 写入文件，会覆盖原内容 |
| `"a"` | 追加内容        |
| `"x"` | 创建新文件       |

本次实验重点使用：

```text
r
w
a
```

---

## 5. 追加内容

继续运行：

```python
with open(
    "learning_record.txt",
    "a",
    encoding="utf-8"
) as file:

    file.write("已完成文本文件写入实验\n")
```

再次查看文件。

思考：

```text
"w"
```

和：

```text
"a"
```

有什么区别？

---

## 6. 读取整个文件

使用：

```python
with open(
    "learning_record.txt",
    "r",
    encoding="utf-8"
) as file:

    content = file.read()

print(content)
```

观察：

```python
read()
```

返回的数据类型。

---

## 7. 按行读取

尝试：

```python
with open(
    "learning_record.txt",
    "r",
    encoding="utf-8"
) as file:

    for line in file:
        print(line.strip())
```

这里：

```python
strip()
```

可以去除每行末尾的换行符以及前后多余空白。

---

## 8. 保存简单AI实验记录

将下面实验信息写入文本文件：

```python
model = "SimpleCNN"
dataset = "MNIST"
accuracy = 0.9521
loss = 0.1386
```

文件内容设计为：

```text
AI实验记录
-------------------------
模型：SimpleCNN
数据集：MNIST
Accuracy：0.9521
Loss：0.1386
-------------------------
```

---

## 9. 连续追加实验记录

允许用户输入：

```text
模型名称
数据集名称
Accuracy
Loss
```

每运行一次程序，就追加一条新的实验记录，而不是覆盖原文件。

例如：

```python
with open(
    "ai_experiments.txt",
    "a",
    encoding="utf-8"
) as file:

    file.write(f"模型：{model}\n")
    file.write(f"数据集：{dataset}\n")
    file.write(f"Accuracy：{accuracy:.4f}\n")
    file.write(f"Loss：{loss:.4f}\n")
    file.write("-" * 30 + "\n")
```

---

## 10. 思考

1. 为什么文件可以解决程序关闭后数据消失的问题？
2. `"w"` 和 `"a"` 的区别是什么？
3. 为什么推荐使用 `with open()`？
4. 文本文件适合保存什么类型的信息？
5. 如果需要保存几十名学生的多项属性，仅使用普通文本是否方便？

最后一个问题将引出 Task 2。

---

# 四、任务2：CSV数据处理与异常处理

## 1. 任务背景

如果需要保存：

```text
学号
姓名
Python成绩
AI成绩
```

等结构化数据，普通文本文件虽然可以完成，但程序读取和处理会比较麻烦。

例如：

```text
20260001,张三,88,92
20260002,李四,95,90
20260003,王五,76,82
```

这种按“行”和“列”组织的数据非常适合使用：

# CSV

CSV 即：

```text
Comma-Separated Values
```

常用于保存表格型数据。

---

## 2. 创建程序

创建：

```text
task02_csv_processing.py
```

并创建目录：

```text
data/
```

本任务使用：

```text
data/students.csv
```

---

# 五、使用csv模块写入数据

首先：

```python
import csv
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

## 1. 使用writer写入CSV

```python
import csv

with open(
    "data/students.csv",
    "w",
    newline="",
    encoding="utf-8-sig"
) as file:

    writer = csv.writer(file)

    writer.writerow(
        [
            "student_id",
            "name",
            "python_score",
            "ai_score"
        ]
    )

    for student in students:

        writer.writerow(
            [
                student["student_id"],
                student["name"],
                student["python_score"],
                student["ai_score"]
            ]
        )
```

运行后打开：

```text
data/students.csv
```

观察数据结构。

---

# 六、使用csv模块读取数据

读取：

```python
import csv

with open(
    "data/students.csv",
    "r",
    encoding="utf-8-sig"
) as file:

    reader = csv.reader(file)

    for row in reader:
        print(row)
```

观察：

```text
每一行
```

被读取后是什么类型。

---

# 七、使用DictReader读取结构化数据

对于包含表头的 CSV，更推荐：

```python
csv.DictReader
```

例如：

```python
import csv

with open(
    "data/students.csv",
    "r",
    encoding="utf-8-sig"
) as file:

    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

观察每一行是否变成类似：

```python
{
    "student_id": "20260001",
    "name": "张三",
    "python_score": "88",
    "ai_score": "92"
}
```

---

## 1. 注意数据类型

CSV 中读取出来的数据默认通常是：

```text
字符串
```

因此需要：

```python
row["python_score"] = float(
    row["python_score"]
)

row["ai_score"] = float(
    row["ai_score"]
)
```

再参与数值计算。

---

# 八、读取CSV后完成成绩统计

读取全部学生后：

```python
students = []
```

每读取一行：

```python
student = {
    "student_id": row["student_id"],
    "name": row["name"],
    "python_score": float(
        row["python_score"]
    ),
    "ai_score": float(
        row["ai_score"]
    )
}

students.append(student)
```

然后完成：

```text
学生人数
Python平均成绩
AI平均成绩
Python最高成绩
AI最高成绩
```

---

# 九、认识异常

考虑下面程序：

```python
age = int(
    input("请输入年龄：")
)
```

如果用户输入：

```text
abc
```

程序会发生什么？

再考虑：

```python
with open(
    "not_exist.txt",
    "r",
    encoding="utf-8"
) as file:
    ...
```

如果文件不存在，会发生什么？

这些运行过程中出现的问题通常称为：

# 异常

---

# 十、try-except基础

创建：

```python
try:

    age = int(
        input("请输入年龄：")
    )

    print(f"年龄：{age}")

except ValueError:

    print("输入错误：年龄必须是整数。")
```

尝试分别输入：

```text
20
```

和：

```text
abc
```

观察程序行为。

---

# 十一、处理文件不存在异常

使用：

```python
try:

    with open(
        "data/students.csv",
        "r",
        encoding="utf-8-sig"
    ) as file:

        content = file.read()

    print(content)

except FileNotFoundError:

    print(
        "数据文件不存在，"
        "将使用空数据开始运行。"
    )
```

---

# 十二、输入有效数值

之前我们通常使用：

```python
score = float(input(...))
```

如果输入字母，程序会直接报错。

现在可以设计：

```python
while True:

    try:

        score = float(
            input("请输入成绩：")
        )

        if 0 <= score <= 100:
            break

        print(
            "成绩必须在0～100之间。"
        )

    except ValueError:

        print(
            "输入格式错误，请输入数字。"
        )
```

这样程序可以同时处理：

```text
abc
-10
120
```

等不同问题。

---

# 十三、异常处理原则

本阶段需要理解：

```text
可以预见的错误
       ↓
    try

出现某类异常
       ↓
   except

给用户友好提示
       ↓
程序继续运行
```

但也需要注意：

> 不应该使用异常处理掩盖所有程序错误。

只对能够合理预期并处理的问题进行异常处理。

---

# 十四、任务3：带文件存储的AI课程学习数据管理系统

## 1. 任务背景

Lab10 中：

```python
students = []
```

只存在于内存。

本任务将管理系统升级为：

```text
程序启动
   ↓
读取students.csv
   ↓
恢复students列表
   ↓
正常使用系统
   ↓
添加 / 修改数据
   ↓
写回students.csv
   ↓
程序退出
   ↓
数据仍然保留
```

这就是：

# 数据持久化

---

## 2. 创建程序

创建：

```text
task03_ai_course_manager_file.py
```

同时使用：

```text
data/students.csv
```

保存学生基本信息。

---

# 十五、确定CSV字段

暂时保存：

```text
student_id
name
python_score
ai_score
completed_labs
ai_interests
```

例如：

```text
student_id,name,python_score,ai_score,completed_labs,ai_interests
20260001,张三,88,92,Lab01|Lab02|Lab03,Computer Vision|Machine Learning
```

为什么使用：

```text
|
```

分隔集合？

因为 CSV 本身使用逗号分隔字段，如果集合内部也直接使用逗号，会使文件结构更加复杂。

---

# 十六、保存学生数据函数

定义：

```python
import csv
```

然后：

```python
def save_students(students, filename):

    with open(
        filename,
        "w",
        newline="",
        encoding="utf-8-sig"
    ) as file:

        fieldnames = [
            "student_id",
            "name",
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

        for student in students:

            writer.writerow(
                {
                    "student_id":
                        student["student_id"],

                    "name":
                        student["name"],

                    "python_score":
                        student["python_score"],

                    "ai_score":
                        student["ai_score"],

                    "completed_labs":
                        "|".join(
                            student[
                                "completed_labs"
                            ]
                        ),

                    "ai_interests":
                        "|".join(
                            student[
                                "ai_interests"
                            ]
                        )
                }
            )
```

---

# 十七、读取学生数据函数

定义：

```python
def load_students(filename):

    students = []

    try:

        with open(
            filename,
            "r",
            encoding="utf-8-sig"
        ) as file:

            reader = csv.DictReader(file)

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

                student = {
                    "student_id":
                        row["student_id"],

                    "name":
                        row["name"],

                    "python_score":
                        float(
                            row[
                                "python_score"
                            ]
                        ),

                    "ai_score":
                        float(
                            row[
                                "ai_score"
                            ]
                        ),

                    "completed_labs":
                        completed_labs,

                    "ai_interests":
                        ai_interests
                }

                students.append(student)

    except FileNotFoundError:

        print(
            "未找到学生数据文件，"
            "将创建新的数据集。"
        )

    return students
```

---

# 十八、程序启动时读取数据

原来：

```python
students = []
```

改为：

```python
DATA_FILE = "data/students.csv"

students = load_students(
    DATA_FILE
)
```

然后：

```python
print(
    f"已加载 {len(students)} 条学生数据。"
)
```

---

# 十九、添加学生后保存

在：

```python
add_student()
```

完成学生添加之后：

```python
save_students(
    students,
    DATA_FILE
)
```

例如：

```text
学生添加成功。
数据已保存。
```

---

# 二十、修改成绩后保存

在：

```python
modify_score()
```

完成成绩修改后：

```python
save_students(
    students,
    DATA_FILE
)
```

这样：

```text
添加数据
修改数据
```

以后都会立即持久化。

---

# 二十一、退出程序前保存

即使程序过程中已经保存，也可以在退出时再次：

```python
save_students(
    students,
    DATA_FILE
)

print("数据已保存。")
print("系统已退出。")
```

---

# 二十二、改进成绩输入函数

将 Lab10 中：

```python
def input_valid_score(prompt):
```

升级为：

```python
def input_valid_score(prompt):

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
                "输入格式错误，"
                "请输入有效数字。"
            )
```

这样程序不仅检查：

```text
数值范围
```

还可以处理：

```text
非数字输入
```

---

# 二十三、处理数据文件异常

除了：

```text
FileNotFoundError
```

还可能出现 CSV 内容无法正确转换的问题。

例如：

```python
try:

    score = float(
        row["python_score"]
    )

except ValueError:

    print(
        "发现无法解析的成绩数据。"
    )
```

本次实验只要求初步处理常见异常，不要求覆盖所有可能情况。

---

# 二十四、系统功能

升级后的系统仍然保持 Lab10 的主要功能：

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
0. 保存并退出

==================================================
```

重点不再是增加新的菜单功能，而是解决：

```text
数据保存
+
数据恢复
+
错误处理
```

---

# 二十五、测试要求

完成程序后必须至少进行以下测试。

## 测试1：首次运行

删除或暂时移走：

```text
data/students.csv
```

运行程序。

程序应能够提示：

```text
未找到学生数据文件，
将创建新的数据集。
```

而不是直接崩溃。

---

## 测试2：添加数据

添加至少3名学生。

退出程序。

检查：

```text
data/students.csv
```

是否已经生成。

---

## 测试3：重新启动程序

重新运行程序。

检查：

```text
上一轮添加的学生是否仍然存在。
```

如果数据能够恢复，说明：

```text
文件持久化
```

已经成功。

---

## 测试4：修改数据

修改某名学生的成绩。

退出程序。

重新启动程序。

检查修改后的结果是否仍然存在。

---

## 测试5：非法数值输入

例如：

```text
请输入Python成绩：abc
```

程序应提示：

```text
输入格式错误，请输入有效数字。
```

而不是直接退出。

---

## 测试6：非法成绩范围

输入：

```text
-10
```

或者：

```text
120
```

程序应提示重新输入。

---

# 二十六、Lab10与Lab11比较

## Lab10

数据只存在于：

```text
students列表
```

程序运行过程：

```text
启动
 ↓
students = []
 ↓
输入数据
 ↓
使用数据
 ↓
关闭
 ↓
数据消失
```

---

## Lab11

程序运行过程：

```text
students.csv
      ↓
load_students()
      ↓
students
      ↓
程序操作
      ↓
save_students()
      ↓
students.csv
```

于是形成：

```text
文件
 ↕
内存数据
```

的关系。

---

# 二十七、从内存数据到文件数据

需要理解：

```text
文件中的CSV
      ↓
读取
      ↓
Python字符串
      ↓
类型转换
      ↓
字典
      ↓
列表
```

保存时则反过来：

```text
列表
  ↓
字典
  ↓
字符串化
  ↓
CSV
  ↓
文件
```

这也是后续进行真实数据处理时非常重要的基本思维。

---

# 二十八、拓展任务：AI实验日志管理器

创建：

```text
extension_experiment_log.py
```

以及：

```text
data/experiment_log.csv
```

---

## 1. 实验记录内容

每条 AI 实验至少包含：

```text
实验编号
模型名称
数据集名称
Epoch
Batch Size
Learning Rate
Accuracy
Loss
训练时间
```

---

## 2. 程序功能

设计菜单：

```text
========================================
          AI实验日志管理器
========================================

1. 添加实验记录
2. 查看全部实验
3. 按模型查询实验
4. 查看最佳实验
5. 查看平均Accuracy
0. 保存并退出

========================================
```

---

## 3. 数据保存

所有实验记录保存到：

```text
data/experiment_log.csv
```

程序重新启动后自动加载原来的实验记录。

---

## 4. 输入异常处理

对以下字段进行检查：

### Epoch

必须：

```text
> 0
```

### Batch Size

必须：

```text
> 0
```

### Learning Rate

必须：

```text
> 0
```

### Accuracy

必须：

```text
0 ≤ Accuracy ≤ 1
```

### Loss

必须：

```text
≥ 0
```

### Training Time

必须：

```text
> 0
```

---

## 5. 最佳实验

找出：

```text
Accuracy最高
```

的一次实验，并输出：

```text
模型名称
数据集
参数
Accuracy
Loss
```

---

## 6. 提高要求

在 Accuracy 相同时：

优先选择：

```text
Loss更低
```

的实验。

如果 Accuracy 和 Loss 都相同，可以进一步比较：

```text
训练时间
```

思考：

> “最佳模型”是否一定只能由一个指标决定？

---

# 二十九、本次实训提交内容

本次实训至少完成：

```text
lab11-file-data-processing/
│
├── task01_text_file.py
├── task02_csv_processing.py
├── task03_ai_course_manager_file.py
│
└── data/
    └── students.csv
```

拓展任务可以完成：

```text
extension_experiment_log.py
```

并生成：

```text
data/experiment_log.csv
```

---

# 三十、实训检查

完成本次实训后，应能够：

* [ ] 理解内存数据与文件数据的区别；
* [ ] 使用 `open()` 打开文件；
* [ ] 使用 `with open()` 管理文件；
* [ ] 使用 `"r"` 读取文件；
* [ ] 使用 `"w"` 写入文件；
* [ ] 使用 `"a"` 追加文件；
* [ ] 正确设置文本文件编码；
* [ ] 读取文本文件内容；
* [ ] 按行读取文本文件；
* [ ] 理解 CSV 的基本结构；
* [ ] 使用 `csv.writer` 写入 CSV；
* [ ] 使用 `csv.reader` 读取 CSV；
* [ ] 使用 `csv.DictReader` 读取结构化数据；
* [ ] 使用 `csv.DictWriter` 写入结构化数据；
* [ ] 将 CSV 字符串转换为数值类型；
* [ ] 使用 `try-except` 处理基本异常；
* [ ] 处理 `ValueError`；
* [ ] 处理 `FileNotFoundError`；
* [ ] 对用户输入进行更加健壮的验证；
* [ ] 将 Python 数据结构保存到文件；
* [ ] 从文件恢复 Python 数据结构；
* [ ] 理解基本的数据持久化概念；
* [ ] 为已有程序增加文件读写功能；
* [ ] 完成具有基本持久化能力的数据管理系统。

---

# 三十一、本次实训知识路线

```text
内存中的数据
     ↓
文件
     ↓
文本读写
     ↓
CSV
     ↓
结构化文件
     ↓
读取
     ↓
类型转换
     ↓
Python数据结构
     ↓
程序处理
     ↓
重新写入文件
     ↓
数据持久化
```

同时：

```text
用户输入 / 文件读取
        ↓
可能出现错误
        ↓
try-except
        ↓
异常处理
        ↓
程序更加健壮
```

---

# 三十二、Lab09～Lab11的程序演进

到目前为止，同一个 AI 课程学习数据管理系统已经经历了三次演进：

```text
Lab09
数据结构综合
      ↓
把系统功能做出来
      ↓
但代码较长

Lab10
函数与模块化
      ↓
重新组织程序
      ↓
代码结构更加清晰

Lab11
文件与异常
      ↓
保存和恢复数据
      ↓
程序更加实用、更加健壮
```

可以概括为：

```text
Lab09
“能完成任务”

        ↓

Lab10
“代码组织合理”

        ↓

Lab11
“数据能够保存”
```

---

# 三十三、阶段衔接

虽然 Lab11 已经可以使用：

```text
列表
+
字典
+
函数
+
文件
```

完成一个较完整的数据管理系统，但当前每名学生仍然表示为：

```python
student = {
    "student_id": "20260001",
    "name": "张三",
    "python_score": 88,
    "ai_score": 92
}
```

同时，与学生相关的操作仍然是独立函数，例如：

```text
find_student()
show_student()
modify_score()
```

下一阶段将进入：

# Lab 12：面向对象程序设计综合应用

届时将进一步思考：

```text
学生的数据
+
学生能够执行的操作
```

是否可以组织到一个统一的对象中。

例如：

```python
class Student:
    ...
```

并进一步设计：

```python
class StudentManager:
    ...
```

从而把程序从：

```text
数据
+
操作数据的函数
```

进一步发展为：

```text
对象
=
数据
+
相关行为
```

完成从过程式程序设计到面向对象程序设计的第一次转换。
