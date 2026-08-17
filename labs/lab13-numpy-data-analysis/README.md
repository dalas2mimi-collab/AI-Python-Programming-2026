# Lab 13：NumPy科学计算与数据分析

## 一、实训目的

通过本次实训掌握 NumPy 数组的创建、访问、切片、变形、统计和向量化运算方法，理解 NumPy 数组与 Python 列表在数值计算中的区别，能够使用二维数组表示人工智能任务中的“样本—特征”数据，并完成基本的数据统计、筛选、标准化和实验结果分析。

前面的 Python 程序通常使用：

```python
scores = [88, 92, 85, 90]
```

并通过循环完成计算：

```python
total = 0

for score in scores:
    total += score
```

从本次实验开始，将逐步转向：

```python
import numpy as np

scores = np.array(
    [88, 92, 85, 90]
)

average = np.mean(scores)
```

进一步学习：

```text
Python列表
    ↓
NumPy数组
    ↓
一维数据
    ↓
二维数据
    ↓
样本 × 特征
    ↓
向量化计算
    ↓
AI数值数据处理
```

这是从通用 Python 编程进入人工智能数据处理的重要一步。

---

## 二、实训内容

本次实训主要包括：

1. NumPy 数组的创建及基本属性；
2. 数组索引、切片和形状变换；
3. 二维数组与轴 `axis` 的基本概念；
4. 数组统计与向量化计算；
5. 布尔索引和数据筛选；
6. AI 数据的基本数值处理；
7. 多轮模型实验结果统计与分析。

本次实训设置：

**4 个必做任务 + 1 个拓展任务。**

---

## 三、实验准备

本次实验需要使用 NumPy。

首先检查：

```python
import numpy as np

print(np.__version__)
```

如果 NumPy 尚未安装，可以在终端执行：

```bash
pip install numpy
```

能够正常运行：

```python
import numpy as np
```

即可开始实验。

---

# 四、任务1：NumPy数组基础

## 1. 任务目标

掌握：

```text
np.array()
ndim
shape
size
dtype
```

理解 NumPy 数组与 Python 列表的基本区别。

---

## 2. 创建程序

创建：

```text
task01_numpy_basics.py
```

首先导入 NumPy：

```python
import numpy as np
```

---

## 3. 创建一维数组

定义：

```python
scores = np.array(
    [85, 92, 78, 96, 88]
)

print(scores)
print(type(scores))
```

观察：

```text
scores
```

的数据类型。

---

## 4. 查看数组属性

继续：

```python
print(f"维度：{scores.ndim}")
print(f"形状：{scores.shape}")
print(f"元素数量：{scores.size}")
print(f"数据类型：{scores.dtype}")
```

理解：

```text
ndim
```

表示数组维度；

```text
shape
```

表示每个维度的大小；

```text
size
```

表示元素总数量；

```text
dtype
```

表示数组元素的数据类型。

---

## 5. 创建浮点数组

定义：

```python
accuracies = np.array(
    [0.91, 0.93, 0.89, 0.95, 0.92]
)

print(accuracies)
print(accuracies.dtype)
```

观察整数数组与浮点数组的 `dtype` 是否相同。

---

## 6. 使用arange()

创建：

```python
epochs = np.arange(1, 11)

print(epochs)
```

再尝试：

```python
even_numbers = np.arange(
    2,
    21,
    2
)

print(even_numbers)
```

比较：

```python
np.arange()
```

与之前学习的：

```python
range()
```

有什么相似之处。

---

## 7. zeros和ones

创建：

```python
zeros = np.zeros(5)
ones = np.ones(5)

print(zeros)
print(ones)
```

进一步创建二维数组：

```python
matrix1 = np.zeros(
    (3, 4)
)

matrix2 = np.ones(
    (2, 5)
)

print(matrix1)
print(matrix2)
```

---

## 8. 创建二维数组

定义三名学生、四次实验的成绩：

```python
scores = np.array(
    [
        [85, 88, 90, 92],
        [76, 80, 82, 85],
        [91, 93, 95, 96]
    ]
)

print(scores)

print(
    f"维度：{scores.ndim}"
)

print(
    f"形状：{scores.shape}"
)

print(
    f"元素数量：{scores.size}"
)
```

观察：

```text
shape = (3, 4)
```

表示什么。

可以理解为：

```text
3行
×
4列
```

---

## 9. 列表与NumPy数组比较

Python 列表：

```python
values = [1, 2, 3, 4]

print(values * 2)
```

NumPy 数组：

```python
values = np.array(
    [1, 2, 3, 4]
)

print(values * 2)
```

比较两个结果。

思考：

> 为什么 NumPy 数组中的 `* 2` 会直接对每个元素进行数值运算？

---

## 10. 思考

完成 Task 1 后回答：

1. NumPy 数组使用什么类型表示？
2. `shape` 和 `size` 有什么区别？
3. 一维数组和二维数组有什么区别？
4. 为什么人工智能数据处理中经常使用 NumPy 数组？
5. Python 列表的 `* 2` 与 NumPy 数组的 `* 2` 为什么表现不同？

---

# 五、任务2：索引、切片与数组变形

## 1. 任务目标

掌握 NumPy 数组的：

```text
索引
切片
二维索引
reshape()
flatten()
```

并进一步理解数组：

```text
行
列
shape
```

之间的关系。

---

## 2. 创建程序

创建：

```text
task02_indexing_reshape.py
```

---

## 3. 一维数组索引

定义：

```python
import numpy as np

accuracies = np.array(
    [
        0.82,
        0.86,
        0.89,
        0.91,
        0.93,
        0.95
    ]
)
```

访问：

```python
print(accuracies[0])
print(accuracies[2])
print(accuracies[-1])
```

---

## 4. 一维数组切片

尝试：

```python
print(accuracies[0:3])
print(accuracies[:3])
print(accuracies[3:])
print(accuracies[-3:])
print(accuracies[::2])
```

观察与 Python 列表切片有什么相似之处。

---

## 5. 二维数组索引

定义：

```python
data = np.array(
    [
        [0.91, 0.18, 12.5],
        [0.93, 0.16, 13.2],
        [0.89, 0.22, 11.8],
        [0.95, 0.14, 14.1]
    ]
)
```

可以理解为：

```text
每一行
=
一次AI实验

第1列
=
Accuracy

第2列
=
Loss

第3列
=
Training Time
```

访问：

```python
print(data[0, 0])
print(data[0, 1])
print(data[1, 2])
```

---

## 6. 获取整行

```python
print(data[0, :])
print(data[1, :])
```

也可以：

```python
print(data[0])
```

---

## 7. 获取整列

Accuracy：

```python
accuracies = data[:, 0]

print(accuracies)
```

Loss：

```python
losses = data[:, 1]

print(losses)
```

训练时间：

```python
training_times = data[:, 2]

print(training_times)
```

这里非常重要。

二维数据中：

```text
行
→ 一条样本或一次实验

列
→ 一个特征或一个指标
```

---

## 8. reshape()

创建：

```python
values = np.arange(
    1,
    13
)

print(values)
print(values.shape)
```

变成：

```python
matrix = values.reshape(
    3,
    4
)

print(matrix)
print(matrix.shape)
```

观察：

```text
12个元素
```

怎样重新组织为：

```text
3 × 4
```

二维数组。

---

## 9. 尝试其他形状

例如：

```python
print(
    values.reshape(2, 6)
)

print(
    values.reshape(4, 3)
)

print(
    values.reshape(6, 2)
)
```

思考为什么：

```python
values.reshape(5, 3)
```

不能正常执行。

---

## 10. 使用-1自动推断

尝试：

```python
matrix = values.reshape(
    3,
    -1
)

print(matrix)
```

NumPy 会自动推断剩余维度。

---

## 11. 展平数组

定义：

```python
matrix = np.array(
    [
        [1, 2, 3],
        [4, 5, 6]
    ]
)
```

执行：

```python
flat = matrix.flatten()

print(flat)
```

观察：

```text
二维数组
↓
一维数组
```

的变化。

---

## 12. AI数据形状理解

假设：

```python
features = np.zeros(
    (100, 20)
)
```

这里可以理解为：

```text
100个样本
×
20个特征
```

即：

```text
shape = (100, 20)
```

这是一种非常常见的 AI 数据表示方式。

---

# 六、任务3：向量化计算与二维数据分析

## 1. 任务目标

理解 NumPy 最重要的特点之一：

# 向量化计算

即尽量避免使用 Python 循环逐个处理数值，而是直接对整个数组执行运算。

---

## 2. 创建程序

创建：

```text
task03_vectorized_analysis.py
```

---

## 3. Python循环方式

定义：

```python
scores = [
    80,
    85,
    90,
    95
]
```

如果需要每个成绩增加5分，可以：

```python
new_scores = []

for score in scores:

    new_scores.append(
        score + 5
    )

print(new_scores)
```

---

## 4. NumPy向量化方式

使用：

```python
import numpy as np

scores = np.array(
    [80, 85, 90, 95]
)

new_scores = scores + 5

print(new_scores)
```

不需要显式编写：

```python
for
```

即可对整个数组完成运算。

---

## 5. 基本向量化运算

定义：

```python
x = np.array(
    [1, 2, 3, 4]
)
```

尝试：

```python
print(x + 10)
print(x - 1)
print(x * 2)
print(x / 2)
print(x ** 2)
```

观察每一个操作是否应用到了所有元素。

---

## 6. 数组之间的运算

定义：

```python
a = np.array(
    [1, 2, 3]
)

b = np.array(
    [10, 20, 30]
)
```

运行：

```python
print(a + b)
print(a - b)
print(a * b)
print(a / b)
```

观察两个相同形状数组如何逐元素计算。

---

# 七、NumPy统计函数

准备：

```python
accuracies = np.array(
    [
        0.91,
        0.93,
        0.89,
        0.95,
        0.92
    ]
)
```

计算：

```python
print(
    np.mean(accuracies)
)

print(
    np.max(accuracies)
)

print(
    np.min(accuracies)
)

print(
    np.sum(accuracies)
)

print(
    np.std(accuracies)
)
```

分别理解：

```text
mean
最大值
最小值
总和
标准差
```

标准差可以用于粗略描述数据波动程度。

---

# 八、二维数组与axis

这是本次实训的重点之一。

定义：

```python
results = np.array(
    [
        [0.91, 0.18, 12.5],
        [0.93, 0.16, 13.2],
        [0.89, 0.22, 11.8],
        [0.95, 0.14, 14.1]
    ]
)
```

其中：

```text
列0：Accuracy
列1：Loss
列2：Training Time
```

---

## 1. 全部数据平均值

```python
print(
    np.mean(results)
)
```

但这个结果通常实际意义不强，因为三列表示不同指标。

---

## 2. 按列统计

执行：

```python
column_means = np.mean(
    results,
    axis=0
)

print(column_means)
```

得到：

```text
平均Accuracy
平均Loss
平均Training Time
```

即：

```text
沿着行方向聚合
↓
每一列得到一个统计值
```

---

## 3. 按行统计

尝试：

```python
row_means = np.mean(
    results,
    axis=1
)

print(row_means)
```

观察：

```text
axis=0
```

和：

```text
axis=1
```

有什么区别。

> 本阶段不要求机械背诵 axis，而应结合数组形状观察计算结果。

---

# 九、布尔索引

NumPy 可以直接构造：

```python
accuracies >= 0.90
```

例如：

```python
accuracies = np.array(
    [
        0.82,
        0.91,
        0.88,
        0.95,
        0.93
    ]
)

mask = accuracies >= 0.90

print(mask)
```

结果类似：

```text
False
True
False
True
True
```

进一步：

```python
qualified = accuracies[
    accuracies >= 0.90
]

print(qualified)
```

直接筛选所有：

```text
Accuracy ≥ 0.90
```

的实验结果。

---

## 1. 多条件筛选

定义：

```python
accuracy = np.array(
    [0.91, 0.95, 0.88, 0.93]
)

loss = np.array(
    [0.18, 0.12, 0.25, 0.16]
)
```

筛选：

```text
Accuracy ≥ 0.90
且
Loss < 0.20
```

可以：

```python
mask = (
    (accuracy >= 0.90)
    &
    (loss < 0.20)
)

print(mask)
```

注意 NumPy 数组组合多个条件时通常使用：

```text
&
|
```

并为每个条件添加括号。

---

# 十、特征标准化初体验

人工智能数据中的不同特征可能具有不同的数值范围。

例如：

```python
feature = np.array(
    [50, 60, 70, 80, 90]
)
```

计算：

```python
mean = np.mean(feature)
std = np.std(feature)

standardized = (
    feature - mean
) / std

print(standardized)
```

这是一种常见的：

# 标准化

形式。

它使数据围绕：

```text
0
```

附近分布。

本阶段只需要理解计算过程，不要求深入讨论机器学习理论。

---

# 十一、任务4：AI多轮实验数值分析

## 1. 任务背景

在真实 AI 实验中，一个模型往往需要进行多轮实验。

每次实验可能记录：

```text
Accuracy
Loss
Training Time
```

例如：

```text
Run 1：0.912, 0.185, 12.6
Run 2：0.925, 0.171, 13.1
Run 3：0.898, 0.204, 12.2
...
```

如果仍然使用：

```text
多个列表
+
大量for循环
```

虽然能够处理，但 NumPy 更适合这种规则的数值数据。

本任务要求完成：

# AI多轮实验数值分析系统

---

## 2. 创建程序

创建：

```text
task04_ai_numpy_analyzer.py
```

---

## 3. 创建实验结果数组

准备：

```python
import numpy as np

results = np.array(
    [
        [0.912, 0.185, 12.6],
        [0.925, 0.171, 13.1],
        [0.898, 0.204, 12.2],
        [0.941, 0.153, 13.8],
        [0.936, 0.160, 13.4],
        [0.952, 0.141, 14.0],
        [0.929, 0.169, 13.0],
        [0.944, 0.150, 13.7]
    ]
)
```

数组形状：

```python
print(results.shape)
```

应该为：

```text
(8, 3)
```

表示：

```text
8次实验
×
3个指标
```

---

## 4. 分离不同指标

使用：

```python
accuracies = results[:, 0]
losses = results[:, 1]
training_times = results[:, 2]
```

输出三个数组。

---

## 5. Accuracy统计

计算：

```python
average_accuracy = np.mean(
    accuracies
)

best_accuracy = np.max(
    accuracies
)

worst_accuracy = np.min(
    accuracies
)

accuracy_std = np.std(
    accuracies
)
```

输出：

```text
平均Accuracy
最高Accuracy
最低Accuracy
Accuracy标准差
```

---

## 6. Loss统计

计算：

```python
average_loss = np.mean(
    losses
)

best_loss = np.min(
    losses
)

worst_loss = np.max(
    losses
)
```

注意：

> 对 Loss 而言，较小值通常比较大值更理想。

---

## 7. Training Time统计

计算：

```python
average_time = np.mean(
    training_times
)

total_time = np.sum(
    training_times
)

fastest_time = np.min(
    training_times
)
```

---

# 十二、查找最佳实验

使用：

```python
best_index = np.argmax(
    accuracies
)

print(best_index)
```

由于数组索引从 0 开始：

```python
best_run = best_index + 1
```

最佳实验完整数据：

```python
best_result = results[
    best_index
]
```

输出：

```text
最佳Run
Accuracy
Loss
Training Time
```

---

# 十三、查找最低Loss实验

使用：

```python
best_loss_index = np.argmin(
    losses
)
```

观察：

> Accuracy最高的实验与Loss最低的实验是否一定是同一次？

---

# 十四、筛选达标实验

规定：

```text
Accuracy ≥ 0.93
```

使用：

```python
qualified_mask = (
    accuracies >= 0.93
)

qualified_results = results[
    qualified_mask
]
```

输出：

```python
print(
    qualified_results
)
```

统计：

```python
qualified_count = np.sum(
    qualified_mask
)
```

达标率：

```python
qualified_rate = (
    qualified_count
    / len(results)
    * 100
)
```

---

# 十五、多条件筛选

进一步要求：

```text
Accuracy ≥ 0.93
且
Loss < 0.17
```

构造：

```python
good_mask = (
    (accuracies >= 0.93)
    &
    (losses < 0.17)
)

good_results = results[
    good_mask
]
```

观察筛选结果。

---

# 十六、比较前后实验结果

前4次：

```python
first_half = accuracies[:4]
```

后4次：

```python
second_half = accuracies[4:]
```

分别计算：

```python
first_mean = np.mean(
    first_half
)

second_mean = np.mean(
    second_half
)
```

输出：

```text
前4次平均Accuracy
后4次平均Accuracy
```

并判断模型近期实验结果是否有所提升。

---

# 十七、二维数组按列统计

直接：

```python
means = np.mean(
    results,
    axis=0
)

mins = np.min(
    results,
    axis=0
)

maxs = np.max(
    results,
    axis=0
)
```

观察：

```text
axis=0
```

如何一次性完成三列指标统计。

---

# 十八、生成分析报告

程序最终可以输出类似：

```text
==================================================
              AI实验NumPy分析报告
==================================================

数据形状：(8, 3)

---------------- Accuracy ----------------

平均Accuracy：0.9296
最高Accuracy：0.9520
最低Accuracy：0.8980
Accuracy标准差：0.0165

最佳实验：Run 6

----------------- Loss -------------------

平均Loss：0.1666
最低Loss：0.1410
最高Loss：0.2040

------------- Training Time -------------

平均训练时间：13.23
总训练时间：105.80
最快实验时间：12.20

--------------- 达标情况 ----------------

目标Accuracy：0.9300
达标实验数量：4
达标率：50.00%

------------- 前后实验比较 --------------

前4次平均Accuracy：0.9190
后4次平均Accuracy：0.9403

模型近期实验结果有所提升。

==================================================
```

---

# 十九、NumPy与前面方法的比较

## Lab06

使用：

```text
循环
+
累加变量
```

边输入边统计。

---

## Lab07

使用：

```text
Python list
+
sum()
+
max()
+
min()
```

保存全部实验数据。

---

## Lab13

进一步使用：

```text
NumPy ndarray
+
向量化运算
+
axis
+
布尔索引
```

处理数值数据。

整个演进过程：

```text
独立变量
   ↓
Python列表
   ↓
NumPy数组
   ↓
二维数值数据
   ↓
向量化数据处理
```

---

# 二十、AI数据的“样本—特征”表示

NumPy 二维数组不仅可以保存实验结果，更重要的是可以表示人工智能数据集。

例如：

```python
X = np.array(
    [
        [5.1, 3.5, 1.4, 0.2],
        [4.9, 3.0, 1.4, 0.2],
        [6.2, 3.4, 5.4, 2.3],
        [5.9, 3.0, 5.1, 1.8]
    ]
)
```

这里：

```text
每一行
=
一个样本

每一列
=
一个特征
```

因此：

```python
print(X.shape)
```

得到：

```text
(4, 4)
```

表示：

```text
4个样本
×
4个特征
```

这也是后续机器学习中最常见的数据表示形式之一。

---

# 二十一、拓展任务：AI样本特征标准化分析

创建：

```text
extension_feature_analysis.py
```

准备一个简单的样本特征矩阵：

```python
import numpy as np

X = np.array(
    [
        [5.1, 3.5, 1.4, 0.2],
        [4.9, 3.0, 1.4, 0.2],
        [4.7, 3.2, 1.3, 0.2],
        [6.4, 3.2, 4.5, 1.5],
        [6.9, 3.1, 4.9, 1.5],
        [6.3, 3.3, 6.0, 2.5]
    ]
)
```

---

## 1. 查看数据形状

输出：

```text
样本数量
特征数量
```

提示：

```python
sample_count = X.shape[0]
feature_count = X.shape[1]
```

---

## 2. 计算每个特征均值

使用：

```python
feature_means = np.mean(
    X,
    axis=0
)
```

---

## 3. 计算每个特征标准差

```python
feature_stds = np.std(
    X,
    axis=0
)
```

---

## 4. 对数据标准化

使用：

```python
X_standardized = (
    X - feature_means
) / feature_stds
```

输出标准化后的数组。

---

## 5. 验证标准化结果

再次计算：

```python
np.mean(
    X_standardized,
    axis=0
)
```

和：

```python
np.std(
    X_standardized,
    axis=0
)
```

观察标准化后的：

```text
均值
```

是否接近：

```text
0
```

标准差是否接近：

```text
1
```

---

## 6. 筛选样本

筛选：

```text
第1个特征 > 5.0
```

例如：

```python
selected = X[
    X[:, 0] > 5.0
]
```

输出符合条件的样本。

---

## 7. 提高要求

自行完成：

```text
同时满足：
第1个特征 > 5.0
第4个特征 > 1.0
```

的样本筛选。

进一步观察：

> NumPy 是怎样在不显式编写 `for` 循环的情况下处理整批样本的？

---

# 二十二、本次实训提交内容

本次实训至少完成：

```text
lab13-numpy-data-analysis/
├── task01_numpy_basics.py
├── task02_indexing_reshape.py
├── task03_vectorized_analysis.py
└── task04_ai_numpy_analyzer.py
```

拓展任务可以创建：

```text
extension_feature_analysis.py
```

本次实验主要使用程序内部构造的数据，因此暂时不要求提供外部数据文件。

---

# 二十三、实训检查

完成本次实训后，应能够：

* [ ] 正确导入 NumPy；
* [ ] 使用 `np.array()` 创建数组；
* [ ] 理解 `ndarray`；
* [ ] 查看 `ndim`、`shape`、`size` 和 `dtype`；
* [ ] 创建一维和二维数组；
* [ ] 使用 `np.arange()` 创建数值序列；
* [ ] 使用 `np.zeros()` 和 `np.ones()`；
* [ ] 使用索引访问数组元素；
* [ ] 使用切片获取数组子集；
* [ ] 使用二维索引访问行和列；
* [ ] 使用 `reshape()` 改变数组形状；
* [ ] 使用 `flatten()` 将数组展平；
* [ ] 理解“样本 × 特征”的二维数组结构；
* [ ] 对整个数组进行向量化运算；
* [ ] 使用 `mean()`、`max()`、`min()`、`sum()` 和 `std()`；
* [ ] 初步理解 `axis=0` 和 `axis=1`；
* [ ] 使用布尔数组进行数据筛选；
* [ ] 使用多个条件筛选数据；
* [ ] 使用 `argmax()` 和 `argmin()` 查找位置；
* [ ] 对简单特征数据进行标准化；
* [ ] 使用 NumPy 分析多轮 AI 实验数值结果。

---

# 二十四、本次实训知识路线

```text
Python list
     ↓
NumPy ndarray
     ↓
一维数组
     ↓
二维数组
     ↓
索引与切片
     ↓
reshape
     ↓
向量化运算
     ↓
统计函数
     ↓
axis
     ↓
布尔索引
     ↓
样本 × 特征
     ↓
AI数值数据分析
```

---

# 二十五、第三阶段的开始

从 Lab13 开始，课程进入：

# 数据处理与人工智能基础阶段

前面的重点是：

```text
怎样写程序
怎样组织程序
怎样保存数据
```

从现在开始重点逐渐转变为：

```text
怎样表示数据
怎样批量处理数据
怎样分析数据
怎样为AI模型准备数据
```

---

# 二十六、阶段衔接

本次实验虽然已经能够使用 NumPy 处理二维数值数组，但真实的数据集通常不仅包含数值，还可能包含：

```text
样本编号
类别名称
文本字段
缺失值
不同类型的数据列
```

例如：

```text
sample_id   age   score   category
001         21    88      A
002         20    92      B
003         22    --      A
```

如果继续单纯使用 NumPy，处理这类表格数据就会变得不够方便。

因此下一阶段将进入：

# Lab 14：Pandas数据处理与可视化

下一次实验将学习：

```text
CSV文件
   ↓
Pandas DataFrame
   ↓
查看数据
   ↓
缺失值处理
   ↓
筛选与分组
   ↓
统计分析
   ↓
Matplotlib可视化
```

数据处理方式也将从：

```python
array[:, 0]
```

进一步发展为更直观的：

```python
df["Accuracy"]
```

为 Lab15 的机器学习实验做好数据准备。
