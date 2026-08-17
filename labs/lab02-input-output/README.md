# Lab 02：输入输出与基本数据类型

## 一、实训目的

通过本次实训进一步掌握 Python 程序中变量、基本数据类型、输入输出和类型转换的使用方法，能够根据实际需求接收用户输入、保存不同类型的数据，并采用规范的格式输出程序运行结果。

结合人工智能专业的简单应用场景，逐步建立“**输入数据 → 保存数据 → 转换数据 → 规范输出**”的基本程序设计思维，为后续学习表达式、条件判断、循环以及数据处理奠定基础。

---

## 二、实训内容

本次实训主要包括以下内容：

1. 认识变量和 Python 基本数据类型；
2. 使用 `input()` 接收用户输入；
3. 掌握字符串、整数和浮点数之间的基本类型转换；
4. 使用 `print()` 和 f-string 进行规范化输出；
5. 综合完成一个简单的 AI 实验参数记录程序。

本次实训共设置 **5 个必做任务** 和 **1 个拓展任务**。

---

## 三、任务1：认识变量与基本数据类型

### 1. 任务目标

认识 Python 中常见的基本数据类型，并学会使用 `type()` 查看变量的数据类型。

主要包括：

* 字符串 `str`
* 整数 `int`
* 浮点数 `float`
* 布尔值 `bool`

### 2. 创建程序

创建文件：

```text
task01_data_types.py
```

输入以下程序：

```python
name = "Python"
version = 3
accuracy = 0.95
is_ai_course = True

print(name)
print(version)
print(accuracy)
print(is_ai_course)

print(type(name))
print(type(version))
print(type(accuracy))
print(type(is_ai_course))
```

运行程序并观察结果。

### 3. 修改程序

将变量修改为与自己学习情况相关的数据，例如：

```python
student_name = "张三"
grade = 2024
study_hours = 1.5
like_python = True
```

分别输出变量的：

* 值；
* 数据类型。

### 4. 思考

观察下面几个数据：

```text
100
100.0
"100"
```

思考：

1. 它们的数据类型是否相同？
2. `"100"` 和 `100` 有什么区别？
3. 为什么程序需要区分不同的数据类型？

---

## 四、任务2：使用 input() 接收用户输入

### 1. 任务目标

掌握 `input()` 函数的基本使用方法，并理解通过 `input()` 获得的数据默认是什么类型。

### 2. 创建程序

创建文件：

```text
task02_student_input.py
```

编写程序，依次输入：

* 姓名；
* 学号；
* 专业；
* 年级；
* Python 学习目标。

参考程序：

```python
name = input("请输入姓名：")
student_id = input("请输入学号：")
major = input("请输入专业：")
grade = input("请输入年级：")
goal = input("请输入本学期Python学习目标：")

print(name)
print(student_id)
print(major)
print(grade)
print(goal)
```

### 3. 查看数据类型

在程序最后增加：

```python
print(type(name))
print(type(student_id))
print(type(major))
print(type(grade))
print(type(goal))
```

运行程序并观察结果。

### 4. 思考

即使输入：

```text
2024
```

为什么：

```python
type(grade)
```

得到的仍然是：

```text
str
```

尝试说明 `input()` 函数返回数据的特点。

---

## 五、任务3：基本数据类型转换

### 1. 任务目标

掌握：

```python
int()
float()
str()
```

等常用类型转换方法。

### 2. 创建程序

创建文件：

```text
task03_type_conversion.py
```

首先运行：

```python
age = input("请输入年龄：")

print(age)
print(type(age))
```

观察 `age` 的数据类型。

然后修改为：

```python
age = int(input("请输入年龄："))

print(age)
print(type(age))
```

再次运行并观察变化。

---

### 3. 完成数据输入

继续完善程序，输入：

* 年龄：整数；
* 每天学习 Python 的时间：浮点数；
* Python 学习天数：整数；
* 当前课程名称：字符串。

参考：

```python
age = int(input("请输入年龄："))
hours = float(input("每天计划学习Python多少小时："))
days = int(input("计划学习多少天："))
course = input("请输入课程名称：")

print(age)
print(hours)
print(days)
print(course)
```

然后分别输出四个变量的数据类型。

---

### 4. 类型转换实验

观察下面程序：

```python
number1 = "100"
number2 = int(number1)
number3 = float(number1)

print(number1, type(number1))
print(number2, type(number2))
print(number3, type(number3))
```

运行程序，并比较：

```text
"100"
100
100.0
```

在 Python 中的区别。

---

## 六、任务4：格式化输出

### 1. 任务目标

掌握使用 f-string 对输出结果进行组织和格式化的方法，使程序输出更加清晰、规范。

创建文件：

```text
task04_formatted_output.py
```

---

### 2. 完成学生学习信息卡

输入：

```python
name = input("请输入姓名：")
major = input("请输入专业：")
grade = input("请输入年级：")
hours = float(input("请输入每天计划学习Python的时间："))
```

使用 f-string 输出：

```python
print(f"姓名：{name}")
print(f"专业：{major}")
print(f"年级：{grade}")
print(f"每日Python学习时间：{hours}小时")
```

---

### 3. 完善输出格式

将程序输出设计为：

```text
========== Python学习信息卡 ==========

姓名：张三
专业：人工智能
年级：2024级
每日Python学习时间：1.50小时

=====================================
```

其中学习时间保留两位小数。

提示：

```python
print(f"每日Python学习时间：{hours:.2f}小时")
```

---

### 4. 进一步观察

尝试：

```python
number = 3.1415926

print(f"{number}")
print(f"{number:.2f}")
print(f"{number:.3f}")
```

观察三种输出形式的区别。

---

## 七、任务5：AI实验参数记录器

### 1. 任务背景

在人工智能实验中，通常需要记录模型名称、数据集、训练轮数、批大小、学习率以及实验结果等信息。

本任务要求综合使用本次实验学习的：

* 变量；
* 数据类型；
* `input()`；
* 类型转换；
* f-string；
* 格式化输出。

完成一个简单的 **AI 实验参数记录器**。

---

### 2. 创建程序

创建文件：

```text
task05_ai_experiment.py
```

程序需要输入以下信息：

```text
学生姓名
模型名称
数据集名称
Epoch数量
Batch Size
Learning Rate
实验准确率
```

其中建议的数据类型为：

| 数据            | 类型    |
| ------------- | ----- |
| 学生姓名          | str   |
| 模型名称          | str   |
| 数据集名称         | str   |
| Epoch         | int   |
| Batch Size    | int   |
| Learning Rate | float |
| Accuracy      | float |

---

### 3. 程序要求

程序运行效果可以设计为：

```text
请输入姓名：张三
请输入模型名称：SimpleCNN
请输入数据集名称：MNIST
请输入Epoch数量：20
请输入Batch Size：32
请输入Learning Rate：0.001
请输入实验准确率：0.9568
```

程序输出：

```text
========================================
          AI实验参数记录
========================================

实验人员：张三
模型名称：SimpleCNN
数据集：MNIST

Epoch：20
Batch Size：32
Learning Rate：0.001000

Accuracy：0.9568

========================================
```

---

### 4. 参考程序框架

```python
name = input("请输入姓名：")
model = input("请输入模型名称：")
dataset = input("请输入数据集名称：")

epochs = int(input("请输入Epoch数量："))
batch_size = int(input("请输入Batch Size："))
learning_rate = float(input("请输入Learning Rate："))
accuracy = float(input("请输入实验准确率："))

print()
print("=" * 40)
print("AI实验参数记录")
print("=" * 40)

print(f"实验人员：{name}")
print(f"模型名称：{model}")
print(f"数据集：{dataset}")

print()
print(f"Epoch：{epochs}")
print(f"Batch Size：{batch_size}")
print(f"Learning Rate：{learning_rate:.6f}")

print()
print(f"Accuracy：{accuracy:.4f}")

print("=" * 40)
```

运行程序并尝试使用不同参数进行测试。

---

## 八、拓展任务：设计自己的数据记录卡

在任务5的基础上，自主设计一个简单的数据记录程序。

可以从下面任选一个主题：

* AI模型训练记录卡；
* 学生课程信息记录卡；
* 计算机硬件配置记录卡；
* 数据集信息记录卡；
* 自己感兴趣的其他主题。

要求至少包含：

* 2 个字符串变量；
* 2 个整数变量；
* 2 个浮点数变量；
* 用户输入；
* 类型转换；
* f-string 格式化输出。

输出结果应具有较清晰的版式。

> 拓展任务鼓励独立设计，不要求与其他同学完全相同。

---

## 九、本次实训提交内容

本次实训应至少完成以下程序：

```text
lab02/
├── task01_data_types.py
├── task02_student_input.py
├── task03_type_conversion.py
├── task04_formatted_output.py
└── task05_ai_experiment.py
```

其中：

* Task 01：变量与数据类型；
* Task 02：用户输入；
* Task 03：类型转换；
* Task 04：格式化输出；
* Task 05：AI实验参数记录器。

拓展任务可另外创建：

```text
extension.py
```

---

## 十、实训检查

完成本次实训后，应能够独立回答和完成以下内容：

* [ ] 能够正确创建和使用变量；
* [ ] 能够区分 `str`、`int`、`float` 和 `bool`；
* [ ] 能够使用 `type()` 查看变量的数据类型；
* [ ] 能够使用 `input()` 获取用户输入；
* [ ] 理解 `input()` 返回的数据默认属于字符串类型；
* [ ] 能够使用 `int()`、`float()` 和 `str()` 进行基本类型转换；
* [ ] 能够使用 `print()` 输出程序运行结果；
* [ ] 能够使用 f-string 组织输出内容；
* [ ] 能够控制浮点数的基本显示格式；
* [ ] 能够完成一个简单的信息输入和输出程序。

---

## 十一、本次实训知识路线

```text
变量
  ↓
基本数据类型
  ↓
input()
  ↓
类型转换
  ↓
print()
  ↓
f-string
  ↓
结构化信息输出
  ↓
AI实验参数记录器
```

完成本次实验后，下一阶段将进一步学习 **运算符与表达式**，使程序不仅能够接收和显示数据，还能够对数据进行计算和处理。
