# Lab 05：循环结构程序设计

## 一、实训目的

通过本次实训掌握 Python 中循环结构的基本使用方法，理解循环在重复执行任务、数据统计和过程控制中的作用，能够根据不同问题选择 `for` 循环或 `while` 循环，并掌握 `range()`、计数、累加、`break`、`continue` 和嵌套循环等基本方法。

在 Lab 04 条件分支程序设计的基础上，进一步建立：

**确定重复任务 → 设置循环条件 → 重复执行 → 控制循环过程 → 得到最终结果**

的程序设计思维。

---

## 二、实训内容

本次实训主要包括以下内容：

1. 使用 `for` 和 `range()` 完成固定次数循环；
2. 使用 `while` 完成条件控制循环；
3. 掌握循环中的计数、累加和简单统计；
4. 掌握 `break` 和 `continue` 的基本使用；
5. 掌握简单嵌套循环，并模拟 AI 模型训练过程。

本次实训共设置 **5 个必做任务** 和 **1 个拓展任务**。

---

# 三、任务1：for循环与range()

## 1. 任务目标

掌握 `for` 循环和 `range()` 的基本使用方法。

基本形式：

```python
for 变量 in range(...):
    循环执行的代码
```

---

## 2. 创建程序

创建：

```text
task01_for_range.py
```

输入：

```python
for i in range(5):
    print(i)
```

运行程序并观察结果。

思考：

```python
range(5)
```

产生的是从哪个数字到哪个数字？

---

## 3. 不同形式的range()

依次运行：

```python
for i in range(1, 6):
    print(i)
```

```python
for i in range(2, 11, 2):
    print(i)
```

```python
for i in range(10, 0, -1):
    print(i)
```

观察：

```text
range(stop)
range(start, stop)
range(start, stop, step)
```

三种形式的区别。

---

## 4. 完成基本练习

使用 `for` 循环分别输出：

```text
1～10
1～20中的偶数
10～1倒序
```

然后输出：

```text
Epoch 1
Epoch 2
Epoch 3
Epoch 4
Epoch 5
```

例如：

```python
for epoch in range(1, 6):
    print(f"Epoch {epoch}")
```

---

## 5. 思考

回答以下问题：

1. `range(1, 6)` 为什么不包含 6？
2. `range(2, 11, 2)` 中的第三个参数有什么作用？
3. 当循环次数已经确定时，为什么通常适合使用 `for`？

---

# 四、任务2：while循环

## 1. 任务目标

掌握 `while` 条件循环的基本使用方法。

基本形式：

```python
while 条件:
    循环执行的代码
```

只要条件为 `True`，循环就会继续执行。

---

## 2. 创建程序

创建：

```text
task02_while.py
```

输入：

```python
count = 1

while count <= 5:
    print(count)
    count += 1
```

运行程序并观察结果。

---

## 3. 修改程序

使用 `while` 输出：

```text
10
9
8
7
...
1
```

参考：

```python
count = 10

while count >= 1:
    print(count)
    count -= 1
```

---

## 4. 模拟模型训练轮次

编写：

```python
epoch = 1
max_epoch = 5

while epoch <= max_epoch:
    print(f"正在进行第 {epoch} 轮训练")
    epoch += 1

print("训练结束")
```

观察循环什么时候停止。

---

## 5. 防止无限循环

观察下面程序：

```python
count = 1

while count <= 5:
    print(count)
```

思考：

为什么这个程序不会正常结束？

> 使用 `while` 时，应特别注意循环条件中的变量是否能够在循环过程中发生变化，否则可能产生无限循环。

---

## 6. for与while的选择

一般情况下：

```text
已知循环次数
        ↓
       for

根据条件决定是否继续
        ↓
      while
```

后续编程中应根据问题特点选择合适的循环结构。

---

# 五、任务3：循环中的计数、累加与统计

## 1. 任务目标

掌握循环中的三个常见程序设计模式：

```text
计数
累加
统计
```

---

## 2. 创建程序

创建：

```text
task03_count_sum.py
```

---

## 3. 计算1～100的和

首先设置：

```python
total = 0
```

然后：

```python
for number in range(1, 101):
    total += number

print(f"1～100的和为：{total}")
```

---

## 4. 统计偶数数量

```python
count = 0

for number in range(1, 101):
    if number % 2 == 0:
        count += 1

print(f"1～100中共有 {count} 个偶数")
```

这里已经将前面学习的：

```text
循环
+
条件判断
```

组合起来使用。

---

## 5. 同时完成统计和累加

编写程序，计算：

```text
1～100中所有偶数的数量
1～100中所有偶数的总和
```

参考框架：

```python
count = 0
total = 0

for number in range(1, 101):
    if number % 2 == 0:
        count += 1
        total += number

print(f"偶数数量：{count}")
print(f"偶数总和：{total}")
```

---

## 6. 模拟多轮实验结果统计

假设连续5次实验的准确率分别通过用户输入：

```python
total_accuracy = 0

for i in range(1, 6):
    accuracy = float(input(f"请输入第{i}次实验Accuracy："))
    total_accuracy += accuracy

average_accuracy = total_accuracy / 5

print(f"平均Accuracy：{average_accuracy:.4f}")
```

尝试输入：

```text
0.91
0.92
0.90
0.94
0.93
```

观察平均值。

---

## 7. 思考

理解下面三个变量在循环中的不同作用：

```python
count += 1
total += value
i += 1
```

它们分别可以用于：

```text
统计次数
累加数据
更新循环状态
```

---

# 六、任务4：break与continue

## 1. 任务目标

掌握循环控制语句：

```text
break
continue
```

其中：

```text
break
```

用于立即结束整个循环；

```text
continue
```

用于跳过当前这一轮，继续下一轮循环。

---

## 2. 创建程序

创建：

```text
task04_loop_control.py
```

---

## 3. break基本使用

运行：

```python
for number in range(1, 11):
    if number == 6:
        break

    print(number)

print("循环结束")
```

观察程序输出。

思考：

为什么：

```text
6
7
8
9
10
```

没有被输出？

---

## 4. continue基本使用

运行：

```python
for number in range(1, 11):
    if number == 6:
        continue

    print(number)
```

观察结果。

比较：

```text
break
```

和：

```text
continue
```

的区别。

---

## 5. 跳过无效实验数据

假设某些实验结果小于0，表示数据无效。

```python
for i in range(1, 6):
    accuracy = float(input(f"请输入第{i}次实验Accuracy："))

    if accuracy < 0:
        print("该数据无效，已跳过")
        continue

    print(f"有效Accuracy：{accuracy:.4f}")
```

输入：

```text
0.91
-1
0.93
0.95
-1
```

观察程序如何跳过无效数据。

---

## 6. 达到目标后提前结束

例如：

```python
for epoch in range(1, 11):
    accuracy = float(input(f"请输入Epoch {epoch}的Accuracy："))

    if accuracy >= 0.95:
        print("模型已达到目标Accuracy")
        break

    print("继续训练")

print("训练过程结束")
```

观察达到：

```text
Accuracy ≥ 0.95
```

后循环如何提前结束。

---

# 七、任务5：AI模型训练过程模拟器

## 1. 任务背景

人工智能模型训练通常包含多个 Epoch，每个 Epoch 又可能包含多个 Batch。

这种结构天然适合使用：

```text
外层循环：Epoch
内层循环：Batch
```

本任务通过一个简化的程序模拟模型训练过程，理解嵌套循环的基本作用。

---

## 2. 创建程序

创建：

```text
task05_training_loop.py
```

---

## 3. 第一阶段：模拟Epoch

输入：

```python
epochs = int(input("请输入Epoch数量："))

for epoch in range(1, epochs + 1):
    print(f"开始Epoch {epoch}")
    print(f"Epoch {epoch}完成")
```

例如：

```text
Epoch = 3
```

观察输出。

---

## 4. 第二阶段：加入Batch

继续输入：

```python
epochs = int(input("请输入Epoch数量："))
batches = int(input("请输入每个Epoch的Batch数量："))

for epoch in range(1, epochs + 1):

    print()
    print(f"===== Epoch {epoch} =====")

    for batch in range(1, batches + 1):
        print(f"正在训练 Batch {batch}")

    print(f"Epoch {epoch} 完成")
```

---

## 5. 观察嵌套循环

如果输入：

```text
Epoch = 3
Batch = 4
```

则内层循环总共执行：

```text
3 × 4 = 12
```

次。

尝试自己计算后，再运行程序验证。

---

## 6. 统计总训练Batch数量

加入：

```python
total_batches = 0
```

每完成一个 Batch：

```python
total_batches += 1
```

最终输出：

```python
print(f"总共完成 {total_batches} 个Batch")
```

完整框架可以写为：

```python
model = input("请输入模型名称：")
epochs = int(input("请输入Epoch数量："))
batches = int(input("请输入每个Epoch的Batch数量："))

total_batches = 0

print()
print("=" * 45)
print(f"{model} 模型训练模拟")
print("=" * 45)

for epoch in range(1, epochs + 1):

    print()
    print(f"Epoch {epoch}/{epochs}")

    for batch in range(1, batches + 1):
        total_batches += 1
        print(f"  Batch {batch}/{batches}")

    print(f"Epoch {epoch} 完成")

print()
print("=" * 45)
print("训练结束")
print(f"总Epoch数量：{epochs}")
print(f"总Batch数量：{total_batches}")
print("=" * 45)
```

---

## 7. 参考运行效果

输入：

```text
模型名称：SimpleCNN
Epoch数量：3
每个Epoch的Batch数量：4
```

输出类似：

```text
=============================================
SimpleCNN 模型训练模拟
=============================================

Epoch 1/3
  Batch 1/4
  Batch 2/4
  Batch 3/4
  Batch 4/4
Epoch 1 完成

Epoch 2/3
  Batch 1/4
  Batch 2/4
  Batch 3/4
  Batch 4/4
Epoch 2 完成

Epoch 3/3
  Batch 1/4
  Batch 2/4
  Batch 3/4
  Batch 4/4
Epoch 3 完成

=============================================
训练结束
总Epoch数量：3
总Batch数量：12
=============================================
```

---

## 8. 实验分析

尝试修改：

```text
Epoch = 2，Batch = 5
Epoch = 5，Batch = 10
Epoch = 10，Batch = 20
```

观察：

```text
总Batch数量
```

如何变化。

思考：

```text
总Batch数量 = Epoch数量 × 每个Epoch的Batch数量
```

与嵌套循环执行次数之间有什么关系。

---

# 八、拓展任务：训练过程早停模拟

在任务5基础上创建：

```text
extension_early_stopping.py
```

模拟一个简化的“提前停止训练”过程。

程序要求：

用户首先输入：

```text
最大Epoch数量
目标Accuracy
```

每个 Epoch 输入一次当前 Accuracy。

例如：

```text
最大Epoch：10
目标Accuracy：0.95
```

运行过程中：

```text
Epoch 1 Accuracy：0.82
继续训练

Epoch 2 Accuracy：0.88
继续训练

Epoch 3 Accuracy：0.92
继续训练

Epoch 4 Accuracy：0.956
目标已达到，停止训练
```

提示：

```python
max_epochs = int(input("请输入最大Epoch数量："))
target_accuracy = float(input("请输入目标Accuracy："))

for epoch in range(1, max_epochs + 1):

    accuracy = float(
        input(f"请输入Epoch {epoch}的Accuracy：")
    )

    if accuracy >= target_accuracy:
        print("目标已达到，停止训练")
        break

    print("继续训练")
```

尝试加入：

```text
Loss
```

作为第二个停止条件。

例如：

```text
Accuracy ≥ 0.95
且
Loss ≤ 0.10
```

时才停止训练。

---

# 九、本次实训提交内容

本次实训至少完成：

```text
lab05-loops/
├── task01_for_range.py
├── task02_while.py
├── task03_count_sum.py
├── task04_loop_control.py
└── task05_training_loop.py
```

拓展任务可以创建：

```text
extension_early_stopping.py
```

---

# 十、实训检查

完成本次实训后，应能够：

* [ ] 正确使用 `for` 循环；
* [ ] 正确使用 `range()`；
* [ ] 理解 `range(start, stop, step)`；
* [ ] 正确使用 `while` 循环；
* [ ] 能够避免简单的无限循环；
* [ ] 能够利用循环完成计数；
* [ ] 能够利用循环完成累加；
* [ ] 能够结合 `if` 和循环完成简单统计；
* [ ] 理解 `break` 的作用；
* [ ] 理解 `continue` 的作用；
* [ ] 能够根据问题选择 `for` 或 `while`；
* [ ] 理解嵌套循环的执行过程；
* [ ] 能够使用循环模拟简单的 Epoch/Batch 训练过程。

---

# 十一、本次实训知识路线

```text
重复任务
   ↓
for
   ↓
range()
   ↓
while
   ↓
计数与累加
   ↓
循环 + 条件判断
   ↓
break / continue
   ↓
嵌套循环
   ↓
Epoch / Batch
   ↓
AI训练过程模拟
```

完成本次实训后，将进入：

**Lab 06：循环结构综合应用**

Lab 06 不再重点学习新的循环语法，而是综合使用：

```text
输入输出
    +
表达式
    +
条件判断
    +
循环结构
    +
计数与统计
```

完成规模更大、功能更完整的程序。
