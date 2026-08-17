# Lab 07：字符串、列表与元组

## 一、实训目的

通过本次实训掌握 Python 中字符串、列表和元组等常用序列类型的基本使用方法，理解序列在批量组织和处理数据中的作用，能够使用索引、切片、遍历、查找、修改、排序和统计等操作完成简单的数据处理任务。

在 Lab 01～Lab 06 中，程序主要通过多个独立变量保存数据，例如：

```python
score1 = 85
score2 = 92
score3 = 78
```

随着数据数量增加，这种方式会越来越不方便。

本次实验开始学习：

```python
scores = [85, 92, 78]
```

从而建立：

```text
单个变量
   ↓
一组数据
   ↓
序列结构
   ↓
批量访问
   ↓
批量处理
   ↓
数据分析
```

的程序设计思维。

---

## 二、实训内容

本次实训主要包括：

1. 字符串的索引、切片、查找和基本处理；
2. 列表的创建、访问、增加、删除和修改；
3. 使用列表完成排序、统计和批量处理；
4. 理解元组及其与列表的区别；
5. 综合完成一个 AI 多轮实验结果序列分析程序。

本次实训设置 **4 个必做任务** 和 **1 个拓展任务**。

---

# 三、任务1：字符串信息处理

## 1. 任务目标

掌握字符串的：

* 索引；
* 切片；
* 长度；
* 查找；
* 大小写转换；
* 分割；
* 去除空白字符。

---

## 2. 创建程序

创建：

```text
task01_string_processing.py
```

首先定义：

```python
text = "Python Programming"
```

完成：

```python
print(text)
print(len(text))

print(text[0])
print(text[-1])

print(text[0:6])
print(text[7:])
```

观察程序运行结果。

---

## 3. 理解索引

对于：

```python
text = "Python"
```

字符位置可以理解为：

```text
 P  y  t  h  o  n
 0  1  2  3  4  5
```

也可以使用负索引：

```text
 P   y   t   h   o   n
-6  -5  -4  -3  -2  -1
```

尝试：

```python
print(text[0])
print(text[2])
print(text[-1])
print(text[-3])
```

---

## 4. 字符串切片

分别运行：

```python
text = "Artificial Intelligence"

print(text[0:10])
print(text[:10])
print(text[11:])
print(text[::2])
print(text[::-1])
```

观察不同切片形式的结果。

---

## 5. 常用字符串操作

创建：

```python
course = "  Python Programming  "
```

尝试：

```python
print(course.strip())
print(course.upper())
print(course.lower())
```

再观察：

```python
text = "Python,AI,Machine Learning"

print(text.split(","))
```

思考：

```python
split()
```

执行以后得到的结果与原来的字符串有什么不同。

---

## 6. 学生信息处理

用户输入：

```python
name = input("请输入姓名：")
major = input("请输入专业：")
email = input("请输入邮箱：")
```

完成：

* 去除姓名前后空格；
* 将邮箱统一转换为小写；
* 判断邮箱中是否包含 `@`；
* 输出格式化后的信息。

例如：

```python
name = name.strip()
email = email.strip().lower()

print(f"姓名：{name}")
print(f"专业：{major}")
print(f"邮箱：{email}")

if "@" in email:
    print("邮箱格式包含@符号")
else:
    print("邮箱格式可能存在问题")
```

---

# 四、任务2：列表的创建与基本操作

## 1. 任务目标

掌握列表的：

```text
创建
访问
修改
增加
删除
遍历
```

---

## 2. 创建程序

创建：

```text
task02_list_operations.py
```

定义：

```python
scores = [85, 92, 78, 96, 88]
```

输出：

```python
print(scores)
print(type(scores))
print(len(scores))
```

---

## 3. 使用索引访问列表

分别输出：

```python
print(scores[0])
print(scores[1])
print(scores[-1])
```

尝试：

```python
print(scores[1:4])
print(scores[:3])
print(scores[2:])
```

观察列表切片与字符串切片有什么相似之处。

---

## 4. 修改列表

执行：

```python
scores[2] = 82
print(scores)
```

观察列表中的数据是否发生变化。

---

## 5. 添加数据

使用：

```python
scores.append(90)
```

然后：

```python
print(scores)
```

继续尝试：

```python
scores.insert(1, 89)
```

观察：

```text
append()
```

和：

```text
insert()
```

的区别。

---

## 6. 删除数据

依次尝试：

```python
scores.remove(92)
print(scores)
```

以及：

```python
removed_score = scores.pop()
print(scores)
print(f"删除的数据：{removed_score}")
```

思考：

```text
remove()
```

与：

```text
pop()
```

有什么区别。

---

## 7. 遍历列表

使用：

```python
scores = [85, 92, 78, 96, 88]

for score in scores:
    print(score)
```

进一步输出：

```python
for score in scores:
    if score >= 90:
        print(f"{score}：优秀")
    elif score >= 60:
        print(f"{score}：合格")
    else:
        print(f"{score}：不合格")
```

---

# 五、任务3：列表统计、排序与元组

## 1. 任务目标

进一步掌握利用列表完成：

* 最大值和最小值；
* 求和；
* 平均值；
* 排序；
* 查找；
* 统计。

同时认识元组。

---

## 2. 创建程序

创建：

```text
task03_sequence_statistics.py
```

定义：

```python
scores = [85, 92, 78, 96, 88, 91]
```

---

## 3. 基本统计

使用：

```python
print(f"学生数量：{len(scores)}")
print(f"最高成绩：{max(scores)}")
print(f"最低成绩：{min(scores)}")
print(f"成绩总和：{sum(scores)}")
```

计算平均成绩：

```python
average = sum(scores) / len(scores)

print(f"平均成绩：{average:.2f}")
```

对比 Lab06：

在没有列表时，我们需要自己编写：

```text
计数器
累加器
最大值变量
最小值变量
```

现在列表已经将所有原始数据保留下来，因此很多统计操作会明显简化。

---

## 4. 列表排序

首先尝试：

```python
scores.sort()
print(scores)
```

再尝试：

```python
scores.sort(reverse=True)
print(scores)
```

观察升序和降序排序。

---

## 5. 使用sorted()

重新定义：

```python
scores = [85, 92, 78, 96, 88, 91]
```

执行：

```python
new_scores = sorted(scores)

print(f"原列表：{scores}")
print(f"排序结果：{new_scores}")
```

观察：

```text
sort()
```

和：

```text
sorted()
```

在是否改变原列表方面有什么区别。

---

## 6. 统计优秀学生数量

要求：

```text
成绩 ≥ 90
```

定义为优秀。

完成：

```python
excellent_count = 0

for score in scores:
    if score >= 90:
        excellent_count += 1

print(f"优秀学生数量：{excellent_count}")
```

---

## 7. 认识元组

定义：

```python
image_size = (224, 224)
```

输出：

```python
print(image_size)
print(type(image_size))

print(image_size[0])
print(image_size[1])
```

---

## 8. 尝试修改元组

尝试：

```python
image_size[0] = 256
```

运行程序。

观察 Python 是否允许修改。

---

## 9. 列表与元组比较

思考：

```python
image_size_list = [224, 224]
```

和：

```python
image_size_tuple = (224, 224)
```

有什么不同。

可以初步理解为：

| 数据结构  | 是否可修改 | 常见用途      |
| ----- | ----- | --------- |
| list  | 可以    | 经常变化的一组数据 |
| tuple | 通常不修改 | 相对固定的一组数据 |

例如人工智能程序中的图像尺寸：

```python
image_size = (224, 224)
```

使用元组就比较自然。

---

# 六、任务4：AI多轮实验结果序列分析

## 1. 任务背景

在 Lab06 中，我们已经完成了 AI 多轮实验结果统计。

当时采用的方法是：

```text
输入一个数据
   ↓
立即统计
   ↓
不保存原始数据
```

因此程序结束循环以后，很难再次查看某一次实验结果。

学习列表以后，可以将所有实验数据保存起来：

```python
accuracies = []
```

每次实验：

```python
accuracies.append(accuracy)
```

最终得到：

```python
[0.91, 0.93, 0.89, 0.95, 0.92]
```

这样就可以进一步完成排序、查询和分析。

---

## 2. 创建程序

创建：

```text
task04_ai_result_analyzer.py
```

---

## 3. 输入实验信息

首先输入：

```text
模型名称
数据集名称
实验次数
```

例如：

```python
model = input("请输入模型名称：")
dataset = input("请输入数据集名称：")
run_count = int(input("请输入实验次数："))
```

---

## 4. 创建实验结果列表

创建：

```python
accuracies = []
losses = []
```

用于分别保存：

```text
Accuracy
Loss
```

---

## 5. 输入实验数据

参考：

```python
for run in range(1, run_count + 1):

    print()
    print(f"---------- Run {run} ----------")

    while True:
        accuracy = float(input("Accuracy："))

        if 0 <= accuracy <= 1:
            break

        print("Accuracy输入无效，请重新输入。")

    while True:
        loss = float(input("Loss："))

        if loss >= 0:
            break

        print("Loss输入无效，请重新输入。")

    accuracies.append(accuracy)
    losses.append(loss)
```

---

## 6. 查看原始实验结果

输出：

```python
print(f"Accuracy记录：{accuracies}")
print(f"Loss记录：{losses}")
```

例如：

```text
Accuracy记录：[0.91, 0.93, 0.89, 0.95, 0.92]
Loss记录：[0.21, 0.18, 0.26, 0.15, 0.19]
```

---

## 7. 完成统计分析

计算：

```python
average_accuracy = sum(accuracies) / len(accuracies)
average_loss = sum(losses) / len(losses)

best_accuracy = max(accuracies)
worst_accuracy = min(accuracies)

best_loss = min(losses)
```

输出：

```text
平均Accuracy
最高Accuracy
最低Accuracy
平均Loss
最低Loss
```

---

## 8. 查找最好实验

可以使用：

```python
best_accuracy = max(accuracies)
best_index = accuracies.index(best_accuracy)
```

由于列表索引从：

```text
0
```

开始，因此实际实验编号为：

```python
best_run = best_index + 1
```

然后输出：

```python
print(f"最佳Accuracy：{best_accuracy:.4f}")
print(f"最佳Accuracy出现在Run {best_run}")
```

---

## 9. Accuracy排序

创建一个新的排序结果：

```python
sorted_accuracies = sorted(accuracies, reverse=True)
```

输出：

```python
print(f"Accuracy降序排列：{sorted_accuracies}")
```

注意不要直接破坏原始数据列表。

---

## 10. 达标实验筛选

用户输入目标：

```python
target_accuracy = float(input("请输入目标Accuracy："))
```

统计达到目标的实验次数：

```python
qualified_count = 0

for accuracy in accuracies:
    if accuracy >= target_accuracy:
        qualified_count += 1
```

计算：

```python
qualified_rate = qualified_count / len(accuracies) * 100
```

---

## 11. 完整实验报告

最终输出可以设计为：

```text
==================================================
             AI实验结果序列分析
==================================================

模型名称：SimpleCNN
数据集：MNIST
实验次数：5

--------------- 原始数据 ----------------

Accuracy：
[0.91, 0.93, 0.89, 0.95, 0.92]

Loss：
[0.21, 0.18, 0.26, 0.15, 0.19]

--------------- Accuracy ----------------

平均Accuracy：0.9200
最高Accuracy：0.9500
最低Accuracy：0.8900
最佳实验：Run 4

Accuracy降序：
[0.95, 0.93, 0.92, 0.91, 0.89]

---------------- Loss --------------------

平均Loss：0.1980
最低Loss：0.1500

--------------- 达标情况 ----------------

目标Accuracy：0.9000
达标次数：4
达标率：80.00%

==================================================
```

---

## 12. 与Lab06进行比较

思考：

### Lab06

使用：

```text
total_accuracy
best_accuracy
worst_accuracy
```

边输入边统计。

优点：

```text
程序简单
占用数据少
```

但实验结束后无法再次查看所有原始结果。

### Lab07

使用：

```python
accuracies = []
```

保存所有实验数据。

因此可以进一步进行：

```text
查询
排序
切片
重新统计
筛选
```

这正是学习数据结构的重要意义。

---

# 七、拓展任务：最近N次实验结果分析

创建：

```text
extension_recent_results.py
```

假设已经获得：

```python
accuracies = [
    0.82,
    0.85,
    0.87,
    0.89,
    0.91,
    0.92,
    0.94,
    0.95
]
```

要求用户输入：

```text
需要分析最近多少次实验：
```

例如：

```text
3
```

利用列表切片获得最近3次实验：

```python
recent_results = accuracies[-3:]
```

然后计算：

```text
最近N次平均Accuracy
最近N次最高Accuracy
最近N次最低Accuracy
```

例如：

```text
========== 最近3次实验分析 ==========

实验结果：
[0.92, 0.94, 0.95]

平均Accuracy：0.9367
最高Accuracy：0.9500
最低Accuracy：0.9200

====================================
```

---

## 提高要求

比较：

```text
前N次实验
```

和：

```text
最近N次实验
```

的平均 Accuracy。

如果最近实验平均结果更高，则输出：

```text
模型近期实验结果有所提升。
```

如果下降，则输出：

```text
模型近期实验结果有所下降。
```

否则输出：

```text
模型近期实验结果基本稳定。
```

---

# 八、本次实训提交内容

本次实训至少完成：

```text
lab07-sequences/
├── task01_string_processing.py
├── task02_list_operations.py
├── task03_sequence_statistics.py
└── task04_ai_result_analyzer.py
```

拓展任务可以创建：

```text
extension_recent_results.py
```

---

# 九、实训检查

完成本次实训后，应能够：

* [ ] 理解字符串属于序列类型；
* [ ] 使用索引访问字符串和列表中的数据；
* [ ] 使用切片获取序列的一部分；
* [ ] 使用 `len()` 获取序列长度；
* [ ] 掌握常见字符串处理方法；
* [ ] 正确创建列表；
* [ ] 使用 `append()` 添加数据；
* [ ] 修改列表中的数据；
* [ ] 删除列表中的数据；
* [ ] 使用循环遍历列表；
* [ ] 使用 `max()`、`min()`、`sum()` 进行基本统计；
* [ ] 对列表进行排序；
* [ ] 理解 `sort()` 与 `sorted()` 的基本区别；
* [ ] 使用 `index()` 查找数据位置；
* [ ] 理解列表和元组的基本区别；
* [ ] 使用列表保存多轮实验数据；
* [ ] 对一组 AI 实验结果进行基本统计和分析。

---

# 十、本次实训知识路线

```text
单个变量
   ↓
字符串
   ↓
索引与切片
   ↓
列表
   ↓
增加 / 删除 / 修改
   ↓
遍历
   ↓
排序与统计
   ↓
元组
   ↓
保存一组实验结果
   ↓
AI实验序列分析
```

---

# 十一、阶段衔接

Lab 01～Lab 06 主要解决：

```text
程序怎样执行
```

从 Lab 07 开始，我们进一步解决：

```text
数据怎样组织
```

程序将从：

```python
score1 = 90
score2 = 85
score3 = 92
```

逐步发展为：

```python
scores = [90, 85, 92]
```

这意味着程序开始具备真正处理：

```text
一组数据
```

的能力。

完成本次实训后，将进入：

# Lab 08：字典与集合

下一阶段将从：

```text
只有数据值的一组数据
```

进一步发展为：

```text
具有名称、属性和对应关系的结构化数据
```

例如：

```python
student = {
    "name": "张三",
    "score": 90
}
```

为后续数据管理程序和人工智能数据集处理奠定基础。
