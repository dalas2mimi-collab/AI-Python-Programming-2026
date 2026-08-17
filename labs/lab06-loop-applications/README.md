# Lab 06：循环结构综合应用

## 一、实训目的

通过本次实训综合运用前面已经学习的 Python 基础知识，进一步理解条件判断与循环结构在完整程序设计中的作用，掌握重复输入、数据验证、计数、累加、最大值与最小值统计以及菜单式交互程序的基本设计方法。

本次实验不再重点学习新的 Python 语法，而是综合运用：

* 输入与输出；
* 变量与数据类型；
* 运算符和表达式；
* 条件分支；
* `for` 循环；
* `while` 循环；
* `break` 和 `continue`；
* 计数与累加；
* 嵌套控制结构。

逐步建立：

```text
分析问题
   ↓
设计程序流程
   ↓
接收数据
   ↓
判断与循环
   ↓
数据统计
   ↓
结果输出
```

的基本程序设计思维。

本次实训共设置 **5 个必做任务** 和 **1 个拓展任务**。

---

# 二、任务1：限次身份验证程序

## 1. 任务目标

综合使用：

```text
while
if
计数器
break
```

完成一个具有最大尝试次数限制的简单验证程序。

---

## 2. 创建程序

创建：

```text
task01_login_validation.py
```

假设系统预先设置：

```python
correct_password = "python123"
```

用户最多允许输入密码 3 次。

如果密码正确：

```text
验证成功，欢迎进入系统！
```

并立即结束循环。

如果密码错误：

```text
密码错误，请重新输入。
```

当连续输入错误达到 3 次时：

```text
验证失败次数过多，系统已退出。
```

---

## 3. 参考程序框架

```python
correct_password = "python123"
max_attempts = 3
attempts = 0

while attempts < max_attempts:

    password = input("请输入密码：")
    attempts += 1

    if password == correct_password:
        print("验证成功，欢迎进入系统！")
        break
    else:
        remaining = max_attempts - attempts

        if remaining > 0:
            print(f"密码错误，还可以尝试 {remaining} 次。")
        else:
            print("验证失败次数过多，系统已退出。")
```

---

## 4. 测试程序

至少测试以下情况：

### 情况1

第一次输入正确。

### 情况2

第二次输入正确。

### 情况3

连续三次输入错误。

---

## 5. 思考

1. 为什么需要变量 `attempts`？
2. `break` 在程序中起什么作用？
3. 如果删除 `attempts += 1`，程序可能出现什么问题？
4. 这个程序中的循环为什么更适合使用 `while` 而不是 `for`？

---

# 三、任务2：连续数据输入与统计

## 1. 任务目标

掌握一种常见的循环方式：

> **不断输入数据，直到输入一个特殊值才结束。**

这种特殊值通常称为结束标志或哨兵值。

---

## 2. 创建程序

创建：

```text
task02_number_statistics.py
```

程序要求用户连续输入整数。

当输入：

```text
0
```

时结束输入。

例如：

```text
请输入一个整数（输入0结束）：12
请输入一个整数（输入0结束）：7
请输入一个整数（输入0结束）：20
请输入一个整数（输入0结束）：5
请输入一个整数（输入0结束）：0
```

---

## 3. 统计内容

程序需要统计：

* 输入了多少个有效数字；
* 所有数字之和；
* 偶数数量；
* 奇数数量；
* 最大值；
* 最小值。

---

## 4. 第一阶段：计数与累加

可以首先实现：

```python
count = 0
total = 0

while True:

    number = int(input("请输入一个整数（输入0结束）："))

    if number == 0:
        break

    count += 1
    total += number
```

---

## 5. 第二阶段：统计奇偶数

增加：

```python
even_count = 0
odd_count = 0
```

在循环中：

```python
if number % 2 == 0:
    even_count += 1
else:
    odd_count += 1
```

---

## 6. 第三阶段：统计最大值和最小值

由于本课程目前还没有学习列表，可以使用变量保存当前最大值和最小值。

第一次输入有效数字时：

```python
if count == 1:
    max_value = number
    min_value = number
```

后续输入：

```python
if number > max_value:
    max_value = number

if number < min_value:
    min_value = number
```

---

## 7. 输出结果

例如：

```text
========== 数据统计结果 ==========

有效数据数量：4
数据总和：44
偶数数量：2
奇数数量：2
最大值：20
最小值：5

=================================
```

---

## 8. 注意特殊情况

如果用户第一次就输入：

```text
0
```

意味着没有输入任何有效数据。

程序应输出：

```text
没有可统计的数据。
```

而不是继续计算最大值或最小值。

---

# 四、任务3：学生成绩批量统计程序

## 1. 任务背景

实际程序经常需要连续处理多条数据。

本任务要求输入一个班级中若干名学生的成绩，并完成统计分析。

---

## 2. 创建程序

创建：

```text
task03_score_statistics.py
```

首先输入学生人数：

```text
请输入学生人数：5
```

然后依次输入成绩：

```text
请输入第1名学生成绩：
请输入第2名学生成绩：
...
```

---

## 3. 输入范围验证

成绩必须满足：

```text
0 ≤ score ≤ 100
```

如果输入：

```text
-10
```

或者：

```text
120
```

程序不能直接接受，而应提示：

```text
成绩输入无效，请重新输入。
```

直到输入合法成绩。

可以使用：

```python
while True:

    score = float(input("请输入成绩："))

    if 0 <= score <= 100:
        break

    print("成绩输入无效，请重新输入。")
```

---

## 4. 需要完成的统计

程序至少计算：

* 学生人数；
* 平均成绩；
* 最高成绩；
* 最低成绩；
* 及格人数；
* 优秀人数。

规定：

```text
成绩 ≥ 60   及格
成绩 ≥ 90   优秀
```

---

## 5. 参考变量设计

```python
total_score = 0
pass_count = 0
excellent_count = 0
```

第一次得到合法成绩以后，可以初始化：

```python
max_score = score
min_score = score
```

---

## 6. 参考程序框架

```python
student_count = int(input("请输入学生人数："))

total_score = 0
pass_count = 0
excellent_count = 0

for i in range(1, student_count + 1):

    while True:

        score = float(input(f"请输入第{i}名学生成绩："))

        if 0 <= score <= 100:
            break

        print("成绩输入无效，请重新输入。")

    total_score += score

    if i == 1:
        max_score = score
        min_score = score
    else:
        if score > max_score:
            max_score = score

        if score < min_score:
            min_score = score

    if score >= 60:
        pass_count += 1

    if score >= 90:
        excellent_count += 1

average_score = total_score / student_count
```

---

## 7. 输出统计结果

设计为：

```text
=====================================
          Python课程成绩统计
=====================================

学生人数：5
平均成绩：82.40
最高成绩：96.00
最低成绩：63.00

及格人数：5
优秀人数：2
及格率：100.00%
优秀率：40.00%

=====================================
```

其中：

```python
pass_rate = pass_count / student_count * 100
excellent_rate = excellent_count / student_count * 100
```

---

## 8. 进一步完善

根据平均成绩输出班级整体情况：

```text
平均成绩 ≥ 90    整体表现优秀
平均成绩 ≥ 80    整体表现良好
平均成绩 ≥ 70    整体表现一般
平均成绩 ≥ 60    基本达到要求
其他             需要加强学习
```

---

# 五、任务4：菜单驱动的交互程序

## 1. 任务目标

学习一种非常常见的完整程序结构：

```text
显示菜单
   ↓
用户选择
   ↓
执行功能
   ↓
返回菜单
   ↓
继续选择
   ↓
退出系统
```

这种结构通常使用：

```python
while True:
```

实现。

---

## 2. 创建程序

创建：

```text
task04_menu_program.py
```

设计一个：

# 简易数据计算器

菜单如下：

```text
==============================
        简易数据计算器
==============================

1. 两数相加
2. 两数相减
3. 两数相乘
4. 两数相除
5. 比较两个数大小
0. 退出程序

==============================
```

---

## 3. 程序基本结构

```python
while True:

    print()
    print("=" * 30)
    print("简易数据计算器")
    print("=" * 30)

    print("1. 两数相加")
    print("2. 两数相减")
    print("3. 两数相乘")
    print("4. 两数相除")
    print("5. 比较两个数大小")
    print("0. 退出程序")

    choice = input("请选择功能：")

    if choice == "0":
        print("程序已退出。")
        break

    elif choice == "1":
        pass

    elif choice == "2":
        pass

    elif choice == "3":
        pass

    elif choice == "4":
        pass

    elif choice == "5":
        pass

    else:
        print("无效选择，请重新输入。")
```

将其中的：

```python
pass
```

替换为相应功能。

---

## 4. 除法处理

执行除法时必须考虑：

```text
除数不能为0
```

例如：

```python
if b == 0:
    print("错误：除数不能为0")
else:
    print(f"计算结果：{a / b}")
```

---

## 5. 比较功能

如果用户选择：

```text
5
```

输入两个数，然后输出：

```text
第一个数较大
```

或者：

```text
第二个数较大
```

或者：

```text
两个数相等
```

---

## 6. 思考

这个程序已经具有一个简单应用程序的基本结构：

```text
菜单
+
输入
+
条件判断
+
循环
+
异常情况处理
+
退出机制
```

思考：

> 如果以后程序功能越来越多，所有代码都继续写在一个文件中是否方便？

这个问题将在后续 **函数与模块化程序设计** 中进一步解决。

---

# 六、任务5：AI多轮实验结果分析系统

## 1. 任务背景

在人工智能实验中，同一个模型通常需要运行多次，以观察结果是否稳定。

例如：

```text
Run 1
Run 2
Run 3
Run 4
Run 5
```

每一次实验都可能得到不同的：

```text
Accuracy
Loss
训练时间
```

本任务要求综合使用 Lab01～Lab06 已学习的知识，完成一个简单的：

# AI多轮实验结果分析系统

---

## 2. 创建程序

创建：

```text
task05_ai_experiment_analyzer.py
```

---

## 3. 输入实验基本信息

首先输入：

```text
模型名称
数据集名称
实验次数
目标Accuracy
```

例如：

```text
请输入模型名称：SimpleCNN
请输入数据集名称：MNIST
请输入实验次数：5
请输入目标Accuracy：0.90
```

---

## 4. 输入每轮实验结果

每次实验输入：

```text
Accuracy
Loss
训练时间（分钟）
```

例如：

```text
---------- Run 1 ----------
Accuracy：0.91
Loss：0.18
训练时间：12.5
```

---

## 5. 数据有效性检查

Accuracy 必须满足：

```text
0 ≤ Accuracy ≤ 1
```

Loss 必须满足：

```text
Loss ≥ 0
```

训练时间必须满足：

```text
训练时间 > 0
```

如果输入错误，应要求重新输入当前指标。

例如：

```python
while True:

    accuracy = float(input("Accuracy："))

    if 0 <= accuracy <= 1:
        break

    print("Accuracy输入无效，请重新输入。")
```

---

## 6. 需要完成的统计

### Accuracy

统计：

```text
平均Accuracy
最高Accuracy
最低Accuracy
```

### Loss

统计：

```text
平均Loss
最低Loss
```

### Training Time

统计：

```text
平均训练时间
总训练时间
```

### 达标情况

统计：

```text
达到目标Accuracy的实验次数
达标率
```

---

## 7. 变量初始化

可以设计：

```python
total_accuracy = 0
total_loss = 0
total_time = 0

qualified_count = 0
```

第一次实验时初始化：

```python
best_accuracy = accuracy
worst_accuracy = accuracy
best_loss = loss
```

---

## 8. 循环统计

参考：

```python
for run in range(1, experiment_count + 1):

    print()
    print(f"---------- Run {run} ----------")

    # 输入并检查 Accuracy
    while True:
        accuracy = float(input("Accuracy："))

        if 0 <= accuracy <= 1:
            break

        print("Accuracy输入无效，请重新输入。")

    # 输入并检查 Loss
    while True:
        loss = float(input("Loss："))

        if loss >= 0:
            break

        print("Loss输入无效，请重新输入。")

    # 输入并检查训练时间
    while True:
        training_time = float(input("训练时间（分钟）："))

        if training_time > 0:
            break

        print("训练时间输入无效，请重新输入。")

    total_accuracy += accuracy
    total_loss += loss
    total_time += training_time

    if run == 1:
        best_accuracy = accuracy
        worst_accuracy = accuracy
        best_loss = loss
    else:

        if accuracy > best_accuracy:
            best_accuracy = accuracy

        if accuracy < worst_accuracy:
            worst_accuracy = accuracy

        if loss < best_loss:
            best_loss = loss

    if accuracy >= target_accuracy:
        qualified_count += 1
```

---

## 9. 计算最终结果

```python
average_accuracy = total_accuracy / experiment_count
average_loss = total_loss / experiment_count
average_time = total_time / experiment_count

qualified_rate = qualified_count / experiment_count * 100
```

---

## 10. 输出实验报告

最终可以设计为：

```text
==================================================
              AI多轮实验统计报告
==================================================

模型名称：SimpleCNN
数据集：MNIST
实验次数：5

---------------- Accuracy ----------------

平均Accuracy：0.9264
最高Accuracy：0.9512
最低Accuracy：0.9015

目标Accuracy：0.9000
达到目标次数：5
达标率：100.00%

---------------- Loss --------------------

平均Loss：0.1642
最低Loss：0.1205

------------- Training Time -------------

总训练时间：63.50 分钟
平均训练时间：12.70 分钟

==================================================
```

---

## 11. 增加综合评价

根据平均 Accuracy：

```text
≥ 0.95   Excellent
≥ 0.90   Good
≥ 0.80   Acceptable
其他     Needs Improvement
```

例如：

```python
if average_accuracy >= 0.95:
    level = "Excellent"
elif average_accuracy >= 0.90:
    level = "Good"
elif average_accuracy >= 0.80:
    level = "Acceptable"
else:
    level = "Needs Improvement"
```

输出：

```text
综合评价：Good
```

---

## 12. 实验分析

完成程序后，分别测试：

### 情况1

实验结果比较稳定：

```text
0.91
0.92
0.93
0.91
0.92
```

### 情况2

实验结果波动较大：

```text
0.75
0.95
0.82
0.97
0.88
```

比较两组结果。

思考：

1. 只看最高 Accuracy 能否全面评价模型？
2. 为什么多次实验比单次实验更有参考意义？
3. 平均值和最好结果分别反映了什么信息？

---

# 七、拓展任务：双模型实验对比器

在 Task 5 基础上进一步设计：

```text
extension_model_comparison.py
```

比较两个模型。

例如：

```text
Model A：SimpleCNN
Model B：MLP
```

分别输入两个模型多次实验的 Accuracy。

计算：

```text
Model A平均Accuracy
Model B平均Accuracy
Model A最高Accuracy
Model B最高Accuracy
```

最后输出：

```text
平均Accuracy更高的模型为：XXXX
```

---

## 拓展要求

程序至少完成：

1. 两个模型分别运行相同次数；
2. 分别计算平均 Accuracy；
3. 分别计算最好 Accuracy；
4. 根据平均 Accuracy 给出比较结果；
5. 如果平均 Accuracy 相同，则提示：

```text
两个模型平均表现相同。
```

---

## 更高要求

有能力的同学可以继续加入：

```text
平均Loss
平均训练时间
```

并尝试思考：

> Accuracy 更高但训练时间也明显更长时，哪个模型一定更好吗？

---

# 八、本次实训提交内容

本次实训至少完成：

```text
lab06-loop-applications/
├── task01_login_validation.py
├── task02_number_statistics.py
├── task03_score_statistics.py
├── task04_menu_program.py
└── task05_ai_experiment_analyzer.py
```

拓展任务可以创建：

```text
extension_model_comparison.py
```

本次 Lab 仍建议学生自行从空白 `.py` 文件开始编写程序，不提供完整 Starter Code。

---

# 九、实训检查

完成本次实训后，应能够：

* [ ] 综合使用 `if` 和循环结构；
* [ ] 使用循环完成重复输入；
* [ ] 使用 `while` 完成数据有效性检查；
* [ ] 使用结束标志控制循环停止；
* [ ] 正确使用计数器和累加器；
* [ ] 不依赖列表完成简单最大值和最小值统计；
* [ ] 使用 `break` 控制循环结束；
* [ ] 使用嵌套控制结构解决实际问题；
* [ ] 使用循环批量处理多条数据；
* [ ] 计算平均值、比例等基本统计量；
* [ ] 设计简单的菜单式交互程序；
* [ ] 能够根据实际需求设计基本程序流程；
* [ ] 综合使用 Lab01～Lab05 的知识完成较完整程序；
* [ ] 完成一个简单的 AI 多轮实验数据分析程序。

---

# 十、本次实训知识路线

```text
输入与输出
     +
运算与表达式
     +
条件判断
     +
循环结构
     ↓
重复输入
     ↓
输入验证
     ↓
计数与累加
     ↓
最大值 / 最小值
     ↓
批量统计
     ↓
菜单式交互
     ↓
完整程序流程
     ↓
AI多轮实验分析
```

---

# 十一、阶段总结

Lab 01～Lab 06 构成了本课程的第一个学习阶段：

```text
Lab 01
开发环境与程序运行
        ↓
Lab 02
数据输入与输出
        ↓
Lab 03
运算与表达式
        ↓
Lab 04
条件判断
        ↓
Lab 05
循环结构
        ↓
Lab 06
综合程序设计
```

完成本次 Lab 后，应已经能够利用 Python 基本语法独立完成具有：

```text
输入
计算
判断
重复执行
数据统计
结果输出
```

等功能的小型程序。

下一阶段将进入：

# Lab 07：字符串、列表与元组

程序将从：

```text
利用若干独立变量保存数据
```

进一步发展为：

```text
使用数据结构批量组织和处理数据
```

为后续数据管理、文件处理以及人工智能数据分析奠定基础。
