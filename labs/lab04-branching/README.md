# Lab 04：条件分支程序设计

## 一、实训目的

通过本次实训掌握 Python 条件分支结构的基本使用方法，能够根据不同条件控制程序执行不同操作，理解单分支、双分支、多分支以及嵌套条件结构的基本特点。

在 Lab 03 已掌握比较表达式和逻辑表达式的基础上，进一步建立：

**输入数据 → 构造条件 → 判断条件 → 选择程序执行路径 → 输出结果**

的程序设计思维，使程序开始具备基本的“判断能力”。

---

## 二、实训内容

本次实训主要包括以下内容：

1. 掌握 `if` 单分支结构；
2. 掌握 `if-else` 双分支结构；
3. 掌握 `if-elif-else` 多分支结构；
4. 使用比较运算和逻辑运算构造复合条件；
5. 掌握嵌套条件判断的基本方法；
6. 综合完成一个 AI 模型性能评价程序。

本次实训共设置 **5 个必做任务** 和 **1 个拓展任务**。

---

# 三、任务1：单分支条件判断

## 1. 任务目标

掌握最基本的 `if` 条件结构。

基本语法：

```python
if 条件:
    条件成立时执行的代码
```

注意：

* `if` 后面的条件最终应得到 `True` 或 `False`；
* 条件后面必须使用英文冒号 `:`；
* `if` 内部代码必须正确缩进。

---

## 2. 创建程序

创建：

```text
task01_single_if.py
```

编写程序：

```python
score = float(input("请输入Python课程成绩："))

if score >= 60:
    print("成绩合格")

print("程序运行结束")
```

分别输入：

```text
85
```

和：

```text
50
```

观察程序执行结果。

---

## 3. 修改程序

增加一个优秀成绩提示：

```python
score = float(input("请输入Python课程成绩："))

if score >= 60:
    print("成绩合格")

if score >= 90:
    print("成绩优秀")

print("成绩查询结束")
```

分别测试：

```text
55
75
95
```

观察两个 `if` 语句是否相互独立。

---

## 4. 人工智能场景练习

假设某模型准确率为用户输入值：

```python
accuracy = float(input("请输入模型Accuracy："))

if accuracy >= 0.90:
    print("模型准确率达到预期目标")
```

测试：

```text
0.86
0.91
0.95
```

---

## 5. 思考

1. 当 `if` 条件不成立时，`if` 内的代码是否执行？
2. 为什么 Python 中缩进非常重要？
3. 两个独立的 `if` 是否可能同时执行？

---

# 四、任务2：双分支程序设计

## 1. 任务目标

掌握 `if-else` 结构，使程序能够在两种情况之间进行选择。

基本形式：

```python
if 条件:
    条件成立时执行
else:
    条件不成立时执行
```

---

## 2. 创建程序

创建：

```text
task02_if_else.py
```

完成成绩合格判断：

```python
score = float(input("请输入成绩："))

if score >= 60:
    print("成绩合格")
else:
    print("成绩不合格")
```

分别输入：

```text
59
60
85
```

观察结果。

---

## 3. 奇偶数判断

输入一个整数：

```python
number = int(input("请输入一个整数："))

if number % 2 == 0:
    print("这是一个偶数")
else:
    print("这是一个奇数")
```

思考 `%` 运算为什么可以用于判断奇偶数。

---

## 4. 模型结果判断

输入模型准确率：

```python
accuracy = float(input("请输入模型Accuracy："))

if accuracy >= 0.90:
    print("模型达到目标")
else:
    print("模型暂未达到目标")
```

尝试不同 Accuracy。

---

## 5. 思考

比较：

```python
if 条件:
    ...
else:
    ...
```

与两个独立：

```python
if 条件1:
    ...

if 条件2:
    ...
```

在程序执行逻辑上的区别。

---

# 五、任务3：多分支程序设计

## 1. 任务目标

掌握 `if-elif-else` 多分支结构。

基本形式：

```python
if 条件1:
    ...
elif 条件2:
    ...
elif 条件3:
    ...
else:
    ...
```

程序会从上到下依次判断条件。

---

## 2. 创建程序

创建：

```text
task03_multi_branch.py
```

完成成绩等级判断：

```python
score = float(input("请输入成绩："))

if score >= 90:
    level = "优秀"
elif score >= 80:
    level = "良好"
elif score >= 70:
    level = "中等"
elif score >= 60:
    level = "及格"
else:
    level = "不及格"

print(f"成绩等级：{level}")
```

分别测试：

```text
95
85
76
65
50
```

---

## 3. 观察判断顺序

尝试将：

```python
if score >= 90:
```

和：

```python
elif score >= 60:
```

的位置进行不合理调整。

观察结果是否仍然正确。

思考：

> 为什么多分支条件通常需要按照一定顺序排列？

---

## 4. AI模型准确率等级评价

输入模型 Accuracy：

```python
accuracy = float(input("请输入模型Accuracy："))

if accuracy >= 0.95:
    level = "Excellent"
elif accuracy >= 0.90:
    level = "Good"
elif accuracy >= 0.80:
    level = "Acceptable"
else:
    level = "Needs Improvement"

print(f"模型评价等级：{level}")
```

尝试：

```text
0.97
0.92
0.86
0.72
```

---

# 六、任务4：复合条件判断

## 1. 任务目标

掌握：

```text
and
or
not
```

在条件判断中的应用。

---

## 2. 创建程序

创建：

```text
task04_compound_conditions.py
```

假设一个模型需要同时满足：

```text
Accuracy ≥ 0.90
Loss < 0.20
```

才能认为达到基本要求。

编写：

```python
accuracy = float(input("请输入Accuracy："))
loss = float(input("请输入Loss："))

if accuracy >= 0.90 and loss < 0.20:
    print("模型达到综合要求")
else:
    print("模型暂未达到综合要求")
```

---

## 3. 使用 or

假设学生满足以下任意一个条件即可获得拓展任务推荐：

```text
Python成绩 ≥ 90
或者
AI基础成绩 ≥ 90
```

程序：

```python
python_score = float(input("请输入Python成绩："))
ai_score = float(input("请输入AI基础成绩："))

if python_score >= 90 or ai_score >= 90:
    print("推荐完成提高型拓展任务")
else:
    print("建议先完成基础任务")
```

---

## 4. 使用 not

观察：

```python
is_finished = False

if not is_finished:
    print("实验尚未完成")
```

理解：

```python
not False
```

为什么会得到：

```text
True
```

---

## 5. 区间判断

Python 可以直接写：

```python
score = float(input("请输入成绩："))

if 0 <= score <= 100:
    print("成绩输入有效")
else:
    print("成绩输入无效")
```

测试：

```text
85
0
100
-5
120
```

---

# 七、任务5：AI模型性能评价助手

## 1. 任务背景

一个人工智能模型不能只根据单一指标判断性能。

本任务使用：

* Accuracy；
* Loss；
* 训练时间；

三个简单指标，对模型进行初步评价。

本任务综合使用：

* 输入输出；
* 类型转换；
* 比较表达式；
* 逻辑表达式；
* 多分支；
* 嵌套判断；
* f-string。

---

## 2. 创建程序

创建：

```text
task05_ai_model_evaluator.py
```

---

## 3. 输入信息

要求输入：

```text
模型名称
数据集名称
Accuracy
Loss
训练时间（分钟）
```

例如：

```text
模型名称：SimpleCNN
数据集：MNIST
Accuracy：0.952
Loss：0.138
训练时间：18.5
```

---

## 4. 第一步：检查输入范围

对于 Accuracy：

```python
if 0 <= accuracy <= 1:
    print("Accuracy输入有效")
else:
    print("Accuracy输入无效")
```

对于 Loss，应保证：

```text
Loss ≥ 0
```

对于训练时间，应保证：

```text
训练时间 > 0
```

---

## 5. 第二步：评价模型准确率

评价标准：

| Accuracy | 等级                |
| -------- | ----------------- |
| ≥ 0.95   | Excellent         |
| ≥ 0.90   | Good              |
| ≥ 0.80   | Acceptable        |
| < 0.80   | Needs Improvement |

---

## 6. 第三步：综合评价

设定以下简单规则：

### 优秀模型

同时满足：

```text
Accuracy ≥ 0.95
Loss < 0.15
```

### 良好模型

同时满足：

```text
Accuracy ≥ 0.90
Loss < 0.25
```

### 基本可用

满足：

```text
Accuracy ≥ 0.80
```

### 需要改进

其余情况。

---

## 7. 参考程序框架

```python
model = input("请输入模型名称：")
dataset = input("请输入数据集名称：")

accuracy = float(input("请输入Accuracy："))
loss = float(input("请输入Loss："))
training_time = float(input("请输入训练时间（分钟）："))

print()
print("=" * 45)
print("AI模型性能评价")
print("=" * 45)

print(f"模型名称：{model}")
print(f"数据集：{dataset}")
print(f"Accuracy：{accuracy:.4f}")
print(f"Loss：{loss:.4f}")
print(f"训练时间：{training_time:.2f} 分钟")

print()

if not (0 <= accuracy <= 1):
    print("错误：Accuracy应在0～1之间")

elif loss < 0:
    print("错误：Loss不能小于0")

elif training_time <= 0:
    print("错误：训练时间必须大于0")

else:
    if accuracy >= 0.95 and loss < 0.15:
        level = "Excellent"
        suggestion = "模型整体表现优秀"

    elif accuracy >= 0.90 and loss < 0.25:
        level = "Good"
        suggestion = "模型表现良好，可继续优化"

    elif accuracy >= 0.80:
        level = "Acceptable"
        suggestion = "模型基本可用，仍有改进空间"

    else:
        level = "Needs Improvement"
        suggestion = "建议进一步调整模型或训练参数"

    print(f"综合等级：{level}")
    print(f"评价建议：{suggestion}")

print("=" * 45)
```

---

## 8. 测试程序

至少完成以下四组测试。

### 测试1

```text
Accuracy = 0.97
Loss = 0.10
训练时间 = 20
```

### 测试2

```text
Accuracy = 0.92
Loss = 0.20
训练时间 = 30
```

### 测试3

```text
Accuracy = 0.84
Loss = 0.32
训练时间 = 25
```

### 测试4

```text
Accuracy = 1.20
Loss = 0.10
训练时间 = 20
```

观察不同条件下程序执行的分支。

---

## 9. 实验分析

思考：

1. 为什么要先检查输入范围？
2. 为什么 `Accuracy = 1.20` 不应继续参与后续评价？
3. 为什么模型评价通常需要综合多个指标？
4. 改变条件判断顺序是否可能改变程序结果？

---

# 八、拓展任务：智能学习状态评价程序

设计：

```text
extension_learning_advisor.py
```

输入：

```text
学生姓名
每日Python学习时间
已完成实验数量
最近一次实验成绩
```

根据下面规则给出学习建议。

---

## 情况1

如果：

```text
实验成绩 ≥ 90
且
每天学习时间 ≥ 1.5小时
```

输出：

```text
学习状态优秀，可以尝试提高型任务。
```

---

## 情况2

如果：

```text
实验成绩 ≥ 75
且
每天学习时间 ≥ 1小时
```

输出：

```text
学习状态良好，请继续保持。
```

---

## 情况3

如果：

```text
实验成绩 ≥ 60
```

输出：

```text
已掌握基本内容，建议增加练习。
```

---

## 情况4

其他情况输出：

```text
建议重新检查基础知识并完成相关练习。
```

---

## 拓展要求

自行增加至少一个判断因素，例如：

```text
是否按时完成实验
是否完成拓展任务
已完成Lab数量
```

使程序的评价规则更加丰富。

---

# 九、本次实训提交内容

本次实训至少完成：

```text
lab04-branching/
├── task01_single_if.py
├── task02_if_else.py
├── task03_multi_branch.py
├── task04_compound_conditions.py
└── task05_ai_model_evaluator.py
```

拓展任务可以创建：

```text
extension_learning_advisor.py
```

---

# 十、实训检查

完成本次实训后，应能够：

* [ ] 理解条件表达式产生的 `True` 和 `False`；
* [ ] 正确使用 `if` 单分支结构；
* [ ] 正确使用 `if-else` 双分支结构；
* [ ] 使用 `if-elif-else` 完成多分支判断；
* [ ] 正确使用比较运算符构造条件；
* [ ] 使用 `and`、`or`、`not` 构造复合条件；
* [ ] 能够进行简单的区间判断；
* [ ] 理解条件判断的执行顺序；
* [ ] 能够正确使用代码缩进；
* [ ] 能够完成简单的嵌套条件判断；
* [ ] 能够根据实际问题设计基本判断规则；
* [ ] 能够使用条件结构完成简单的 AI 场景评价程序。

---

# 十一、本次实训知识路线

```text
输入数据
   ↓
比较表达式
   ↓
True / False
   ↓
if
   ↓
if-else
   ↓
if-elif-else
   ↓
复合条件
   ↓
嵌套条件
   ↓
多指标判断
   ↓
AI模型性能评价
```

完成本次实训后，将进入 **Lab 05：循环结构程序设计**。

下一阶段程序将从：

```text
根据条件执行一次
```

进一步发展为：

```text
根据规则重复执行多次
```

并正式学习 `for`、`while`、`range()` 以及循环控制。
