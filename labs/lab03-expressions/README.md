# Lab 03：运算符与表达式

## 一、实训目的

通过本次实训掌握 Python 中常用运算符及表达式的基本使用方法，能够利用算术运算符完成数值计算，理解运算符优先级和复合赋值的基本规则，并初步认识比较表达式和逻辑表达式。

在 Lab 02 “输入数据与输出数据”的基础上，进一步建立：

**输入数据 → 构造表达式 → 完成计算 → 输出结果**

的基本程序设计思维，为后续条件判断、循环结构和数据处理奠定基础。

---

## 二、实训内容

本次实训主要包括以下内容：

1. 掌握 Python 常用算术运算符；
2. 理解表达式及运算优先级；
3. 掌握赋值运算和复合赋值；
4. 初步认识比较运算符和逻辑运算符；
5. 综合完成一个 AI 模型训练参数与时间估算程序。

本次实训共设置 **5 个必做任务** 和 **1 个拓展任务**。

---

# 三、任务1：算术运算符基础

## 1. 任务目标

掌握 Python 中常用的算术运算符。

| 运算符  | 含义  | 示例       |
| ---- | --- | -------- |
| `+`  | 加法  | `a + b`  |
| `-`  | 减法  | `a - b`  |
| `*`  | 乘法  | `a * b`  |
| `/`  | 除法  | `a / b`  |
| `//` | 整除  | `a // b` |
| `%`  | 取余  | `a % b`  |
| `**` | 幂运算 | `a ** b` |

---

## 2. 创建程序

创建文件：

```text
task01_arithmetic.py
```

输入：

```python
a = 17
b = 5

print(f"a + b = {a + b}")
print(f"a - b = {a - b}")
print(f"a * b = {a * b}")
print(f"a / b = {a / b}")
print(f"a // b = {a // b}")
print(f"a % b = {a % b}")
print(f"a ** b = {a ** b}")
```

运行程序并观察结果。

---

## 3. 重点观察

重点比较：

```python
17 / 5
17 // 5
17 % 5
```

思考这三个表达式之间有什么区别。

---

## 4. 修改程序

分别尝试：

```python
20 / 4
20 // 4
20 % 4
```

以及：

```python
21 / 4
21 // 4
21 % 4
```

记录运行结果并分析 `/`、`//` 和 `%` 的不同作用。

---

## 5. 思考

回答：

1. `/` 和 `//` 有什么区别？
2. `%` 运算可以得到什么？
3. `2 ** 3` 的结果是多少？
4. 为什么数据处理中经常会使用整除和取余运算？

---

# 四、任务2：表达式与运算优先级

## 1. 任务目标

理解表达式的概念和 Python 中基本的运算优先级。

观察：

```python
result = 10 + 5 * 2
print(result)
```

运行后，结果是否为：

```text
30
```

还是：

```text
20
```

分析原因。

---

## 2. 使用括号改变运算顺序

分别运行：

```python
result1 = 10 + 5 * 2
result2 = (10 + 5) * 2

print(result1)
print(result2)
```

比较两个结果。

---

## 3. 创建程序

创建文件：

```text
task02_expressions.py
```

完成以下表达式计算：

```python
a = 10
b = 4
c = 2

result1 = a + b * c
result2 = (a + b) * c
result3 = a ** c + b
result4 = a / c + b
result5 = a / (c + b)

print(result1)
print(result2)
print(result3)
print(result4)
print(result5)
```

---

## 4. 学习建议

当表达式比较复杂时，即使 Python 默认的运算优先级可以得到正确结果，也建议适当使用括号，使程序更加清晰。

例如：

```python
average = (score1 + score2 + score3) / 3
```

通常比依赖读者自行判断优先级更容易理解。

---

## 5. 思考

比较：

```python
2 + 3 * 4
```

和：

```python
(2 + 3) * 4
```

说明括号在表达式中的作用。

---

# 五、任务3：赋值与复合赋值运算

## 1. 任务目标

掌握普通赋值和常用复合赋值运算。

常见形式包括：

```text
=
+=
-=
*=
/=
```

---

## 2. 创建程序

创建：

```text
task03_assignment.py
```

首先运行：

```python
score = 80
print(score)

score = score + 5
print(score)
```

然后修改为：

```python
score = 80
print(score)

score += 5
print(score)
```

观察两个程序的结果是否一致。

---

## 3. 继续练习

运行：

```python
value = 100

value += 20
print(value)

value -= 10
print(value)

value *= 2
print(value)

value /= 5
print(value)
```

观察变量 `value` 每一步的变化。

---

## 4. 模拟训练参数更新

假设一个模型已经训练了：

```python
epoch = 0
```

每完成一轮训练：

```python
epoch += 1
```

例如：

```python
epoch = 0

epoch += 1
print(f"当前Epoch：{epoch}")

epoch += 1
print(f"当前Epoch：{epoch}")

epoch += 1
print(f"当前Epoch：{epoch}")
```

思考：

```python
epoch += 1
```

与：

```python
epoch = epoch + 1
```

是否具有相同作用。

> 这里暂时不使用循环，后续 Lab 将利用循环结构自动完成重复更新。

---

# 六、任务4：比较表达式与逻辑表达式

## 1. 任务目标

初步认识比较运算符和逻辑运算符，并观察表达式最终产生的布尔值。

常见比较运算符：

| 运算符  | 含义   |
| ---- | ---- |
| `>`  | 大于   |
| `<`  | 小于   |
| `>=` | 大于等于 |
| `<=` | 小于等于 |
| `==` | 等于   |
| `!=` | 不等于  |

---

## 2. 创建程序

创建：

```text
task04_comparison_logic.py
```

输入：

```python
accuracy = 0.92

print(accuracy > 0.90)
print(accuracy >= 0.95)
print(accuracy == 0.92)
print(accuracy != 0.80)
```

观察输出。

---

## 3. 查看表达式类型

增加：

```python
result = accuracy > 0.90

print(result)
print(type(result))
```

观察：

```python
accuracy > 0.90
```

最终得到的是什么类型的数据。

---

## 4. 逻辑运算

Python 中常见逻辑运算符包括：

```text
and
or
not
```

例如：

```python
accuracy = 0.92
loss = 0.15

result1 = accuracy >= 0.90 and loss < 0.20
result2 = accuracy >= 0.95 or loss < 0.20
result3 = not accuracy < 0.80

print(result1)
print(result2)
print(result3)
```

观察输出结果。

---

## 5. 人工智能场景表达式

假设一个模型：

```python
accuracy = 0.93
training_time = 45
```

构造表达式：

```python
accuracy_ok = accuracy >= 0.90
time_ok = training_time <= 60
overall_ok = accuracy_ok and time_ok

print(f"准确率达到要求：{accuracy_ok}")
print(f"训练时间达到要求：{time_ok}")
print(f"综合条件满足：{overall_ok}")
```

本次实验只观察表达式结果。

在后续 **Lab 04 条件分支程序设计** 中，将使用这些布尔表达式控制程序执行不同的代码。

---

# 七、任务5：AI模型训练参数与时间估算器

## 1. 任务背景

人工智能模型训练过程中，经常需要根据：

* 数据集样本数量；
* Batch Size；
* Epoch 数量；
* 每个 Batch 的训练时间；

估算模型训练过程中的数据批次数量和总训练时间。

本任务要求综合运用 Lab 02 和 Lab 03 已学习的知识，完成一个简单的：

**AI 模型训练参数与时间估算器。**

---

## 2. 创建程序

创建文件：

```text
task05_training_estimator.py
```

---

## 3. 输入内容

程序需要用户输入：

```text
模型名称
数据集名称
训练样本数量
Batch Size
Epoch数量
每个Batch预计训练时间（秒）
```

建议的数据类型：

| 数据         | 类型    |
| ---------- | ----- |
| 模型名称       | str   |
| 数据集名称      | str   |
| 样本数量       | int   |
| Batch Size | int   |
| Epoch      | int   |
| Batch训练时间  | float |

---

## 4. 需要完成的计算

### （1）完整 Batch 数量

```python
full_batches = samples // batch_size
```

### （2）剩余样本数量

```python
remaining_samples = samples % batch_size
```

### （3）每个 Epoch 预计训练时间

```python
epoch_time = full_batches * batch_time
```

为了简化本次实验，暂时仅根据完整 Batch 估算时间。

### （4）全部 Epoch 预计训练时间

```python
total_time = epoch_time * epochs
```

### （5）转换为分钟

```python
total_minutes = total_time / 60
```

---

## 5. 参考程序框架

```python
model = input("请输入模型名称：")
dataset = input("请输入数据集名称：")

samples = int(input("请输入训练样本数量："))
batch_size = int(input("请输入Batch Size："))
epochs = int(input("请输入Epoch数量："))
batch_time = float(input("请输入每个Batch预计训练时间（秒）："))

full_batches = samples // batch_size
remaining_samples = samples % batch_size

epoch_time = full_batches * batch_time
total_time = epoch_time * epochs
total_minutes = total_time / 60

print()
print("=" * 45)
print("AI模型训练估算结果")
print("=" * 45)

print(f"模型名称：{model}")
print(f"数据集：{dataset}")

print()
print(f"训练样本数量：{samples}")
print(f"Batch Size：{batch_size}")
print(f"Epoch数量：{epochs}")

print()
print(f"每个Epoch完整Batch数量：{full_batches}")
print(f"剩余样本数量：{remaining_samples}")

print()
print(f"每个Epoch预计训练时间：{epoch_time:.2f} 秒")
print(f"总训练时间：{total_time:.2f} 秒")
print(f"总训练时间：{total_minutes:.2f} 分钟")

print("=" * 45)
```

---

## 6. 参考运行效果

例如输入：

```text
请输入模型名称：SimpleCNN
请输入数据集名称：MNIST
请输入训练样本数量：60000
请输入Batch Size：32
请输入Epoch数量：10
请输入每个Batch预计训练时间（秒）：0.05
```

程序可以输出类似：

```text
=============================================
AI模型训练估算结果
=============================================

模型名称：SimpleCNN
数据集：MNIST

训练样本数量：60000
Batch Size：32
Epoch数量：10

每个Epoch完整Batch数量：1875
剩余样本数量：0

每个Epoch预计训练时间：93.75 秒
总训练时间：937.50 秒
总训练时间：15.62 分钟

=============================================
```

---

## 7. 实验分析

分别修改：

```text
Batch Size = 16
Batch Size = 32
Batch Size = 64
Batch Size = 128
```

观察：

* 每个 Epoch 的 Batch 数量；
* 预计训练时间；

发生了怎样的变化。

> 本实验中的训练时间只是为了练习表达式而进行的简化估算，实际深度学习模型训练时间还会受到硬件、数据读取、模型复杂度等多种因素影响。

---

# 八、拓展任务：AI数据集划分计算器

很多人工智能实验需要将数据划分为：

```text
训练集
验证集
测试集
```

设计一个程序：

```text
extension_dataset_split.py
```

用户输入：

```text
数据集名称
样本总数
训练集比例
验证集比例
```

例如：

```text
样本总数：1000
训练集比例：0.7
验证集比例：0.1
```

程序计算：

```python
train_samples = int(total_samples * train_ratio)
val_samples = int(total_samples * val_ratio)
test_samples = total_samples - train_samples - val_samples
```

并输出：

```text
========== 数据集划分结果 ==========

数据集：Demo Dataset
总样本数：1000

训练集：700
验证集：100
测试集：200

====================================
```

### 拓展要求

尝试修改不同划分比例，例如：

```text
6 : 2 : 2
7 : 1 : 2
8 : 1 : 1
```

观察不同划分方案对应的样本数量。

---

# 九、本次实训提交内容

本次实训至少完成：

```text
lab03-expressions/
├── task01_arithmetic.py
├── task02_expressions.py
├── task03_assignment.py
├── task04_comparison_logic.py
└── task05_training_estimator.py
```

拓展任务可创建：

```text
extension_dataset_split.py
```

---

# 十、实训检查

完成本次实训后，应能够：

* [ ] 正确使用 `+`、`-`、`*`、`/`；
* [ ] 理解 `/` 和 `//` 的区别；
* [ ] 能够使用 `%` 完成取余运算；
* [ ] 能够使用 `**` 完成幂运算；
* [ ] 理解表达式和基本运算优先级；
* [ ] 能够使用括号控制运算顺序；
* [ ] 能够使用基本赋值和复合赋值运算；
* [ ] 理解比较表达式产生布尔值；
* [ ] 初步掌握 `and`、`or`、`not`；
* [ ] 能够将输入数据组织成计算表达式；
* [ ] 能够使用表达式解决简单实际计算问题。

---

# 十一、本次实训知识路线

```text
输入数据
   ↓
算术运算符
   ↓
表达式
   ↓
运算优先级
   ↓
赋值运算
   ↓
比较表达式
   ↓
逻辑表达式
   ↓
实际计算问题
   ↓
AI训练参数与时间估算
```

完成本次实验后，下一阶段将进入 **Lab 04：条件分支程序设计**。

届时将进一步学习如何根据本次实验得到的：

```text
True
False
```

控制程序执行不同的操作，实现真正具有“判断能力”的程序。
