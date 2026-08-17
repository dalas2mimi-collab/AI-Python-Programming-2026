# Lab 14：Pandas数据处理与可视化

## 一、实训目的

通过本次实训掌握 Pandas 中 `Series` 和 `DataFrame` 的基本使用方法，能够读取 CSV 表格数据，对数据进行查看、筛选、清洗、排序、分组和统计，并使用 Matplotlib 对分析结果进行基本可视化。

在 Lab 13 中，我们主要使用 NumPy 二维数组表示数据：

```python
results = np.array([
    [0.92, 0.18, 12.5],
    [0.94, 0.15, 13.2]
])
```

其中：

```text
第1列 → Accuracy
第2列 → Loss
第3列 → Training Time
```

需要由程序员记住每一列的含义。

从本次实验开始，将进一步使用：

```python
df["accuracy"]
df["loss"]
df["training_time"]
```

这样的带列名数据结构。

学习路线为：

```text
CSV文件
   ↓
Pandas DataFrame
   ↓
查看数据
   ↓
检查数据质量
   ↓
缺失值 / 重复值处理
   ↓
筛选与排序
   ↓
分组统计
   ↓
Matplotlib可视化
   ↓
AI实验数据分析
```

---

## 二、实训内容

本次实训主要包括：

1. 使用 Pandas 读取 CSV 数据；
2. 认识 `DataFrame` 及其基本属性；
3. 数据选择、筛选和排序；
4. 缺失值、重复值等数据质量检查；
5. 数据清洗与简单数据转换；
6. 使用 `groupby()` 完成分组统计；
7. 使用 Matplotlib 绘制基本统计图；
8. 综合完成 AI 实验数据探索性分析。

本次实训设置：

**4 个必做任务 + 1 个拓展任务。**

---

# 三、实验准备

本次实验需要使用：

```text
pandas
matplotlib
```

首先测试：

```python
import pandas as pd
import matplotlib.pyplot as plt

print(pd.__version__)
```

如果尚未安装，可以在终端执行：

```bash
pip install pandas matplotlib
```

---

# 四、实验数据

本次实验统一使用：

```text
data/ai_experiments.csv
```

数据主要记录多次人工智能模型实验结果。

主要字段包括：

| 字段              | 含义         |
| --------------- | ---------- |
| `experiment_id` | 实验编号       |
| `model`         | 模型名称       |
| `dataset`       | 数据集名称      |
| `epochs`        | 训练轮数       |
| `batch_size`    | Batch Size |
| `learning_rate` | 学习率        |
| `accuracy`      | Accuracy   |
| `loss`          | Loss       |
| `training_time` | 训练时间/min   |
| `gpu_memory`    | GPU显存占用/GB |

数据中将有意保留少量：

```text
缺失数据
重复数据
```

供后续数据清洗实验使用。

---

# 五、任务1：DataFrame基础与数据读取

## 1. 任务目标

掌握：

```text
pd.read_csv()
head()
tail()
shape
columns
dtypes
info()
describe()
```

并理解 Pandas `DataFrame` 的基本结构。

---

## 2. 创建程序

创建：

```text
task01_dataframe_basics.py
```

导入：

```python
import pandas as pd
```

读取数据：

```python
df = pd.read_csv(
    "data/ai_experiments.csv"
)

print(df)
```

---

## 3. 查看DataFrame类型

```python
print(type(df))
```

观察结果。

可以初步理解：

```text
DataFrame
=
带有行和列标签的二维表格数据
```

---

## 4. 查看前几行数据

```python
print(df.head())
```

默认显示前：

```text
5
```

行。

尝试：

```python
print(df.head(3))
```

---

## 5. 查看最后几行

```python
print(df.tail())
```

---

## 6. 查看数据规模

```python
print(df.shape)
```

如果结果为：

```text
(20, 10)
```

表示：

```text
20条实验记录
×
10个字段
```

分别输出：

```python
print(
    f"实验数量：{df.shape[0]}"
)

print(
    f"字段数量：{df.shape[1]}"
)
```

---

## 7. 查看列名

```python
print(df.columns)
```

---

## 8. 查看数据类型

```python
print(df.dtypes)
```

观察：

```text
object
int64
float64
```

等数据类型。

思考：

> 为什么 `model` 通常不是数值类型，而 `accuracy` 通常是浮点类型？

---

## 9. 查看整体数据情况

使用：

```python
df.info()
```

重点观察：

```text
数据数量
非空数据数量
数据类型
```

---

## 10. 查看数值统计

```python
print(
    df.describe()
)
```

观察：

```text
count
mean
std
min
25%
50%
75%
max
```

分别表示什么。

---

# 六、按列访问数据

获取模型名称：

```python
print(
    df["model"]
)
```

获取 Accuracy：

```python
print(
    df["accuracy"]
)
```

查看类型：

```python
print(
    type(df["accuracy"])
)
```

这里会看到：

```text
DataFrame
↓
二维表

Series
↓
一列数据
```

---

# 七、选择多列

例如：

```python
selected = df[
    [
        "model",
        "dataset",
        "accuracy",
        "loss"
    ]
]

print(selected)
```

---

# 八、选择指定行

使用：

```python
print(
    df.iloc[0]
)
```

访问第一条实验记录。

继续：

```python
print(
    df.iloc[0:5]
)
```

获取前5条记录。

---

# 九、基本筛选

筛选：

```text
Accuracy ≥ 0.90
```

可以：

```python
high_accuracy = df[
    df["accuracy"] >= 0.90
]

print(high_accuracy)
```

---

## 多条件筛选

筛选：

```text
Accuracy ≥ 0.90
且
Loss < 0.20
```

使用：

```python
selected = df[
    (df["accuracy"] >= 0.90)
    &
    (df["loss"] < 0.20)
]

print(selected)
```

---

# 十、按模型筛选

例如：

```python
cnn_results = df[
    df["model"] == "SimpleCNN"
]

print(cnn_results)
```

---

# 十一、排序

按 Accuracy 降序：

```python
sorted_df = df.sort_values(
    by="accuracy",
    ascending=False
)

print(
    sorted_df[
        [
            "model",
            "dataset",
            "accuracy"
        ]
    ]
)
```

观察哪一次实验 Accuracy 最高。

---

# 十二、任务1思考

完成后回答：

1. NumPy `ndarray` 和 Pandas `DataFrame` 有什么区别？
2. `df.shape` 表示什么？
3. `df.head()` 有什么作用？
4. 为什么分析数据前通常先使用 `info()`？
5. 使用列名访问数据有什么优势？
6. 布尔筛选与 Lab13 的 NumPy 布尔索引有什么联系？

---

# 十三、任务2：数据质量检查与清洗

## 1. 任务目标

掌握真实数据处理中常见的：

```text
缺失值
重复值
异常数据
数据类型
```

检查和基本处理方法。

创建：

```text
task02_data_cleaning.py
```

---

# 十四、检查缺失值

读取数据：

```python
import pandas as pd

df = pd.read_csv(
    "data/ai_experiments.csv"
)
```

查看：

```python
print(
    df.isnull()
)
```

进一步统计每一列：

```python
print(
    df.isnull().sum()
)
```

结果可能类似：

```text
experiment_id    0
model            0
dataset          0
epochs           0
batch_size       0
learning_rate    0
accuracy         1
loss             0
training_time    1
gpu_memory       0
```

这表示：

```text
accuracy
training_time
```

中存在缺失数据。

---

# 十五、检查重复数据

使用：

```python
print(
    df.duplicated()
)
```

统计：

```python
duplicate_count = (
    df.duplicated().sum()
)

print(
    f"重复记录数量："
    f"{duplicate_count}"
)
```

---

# 十六、删除重复数据

```python
df = df.drop_duplicates()
```

然后再次：

```python
print(
    df.duplicated().sum()
)
```

---

# 十七、处理缺失值

## 方法1：删除

可以：

```python
df_clean = df.dropna()
```

但这样会删除整行数据。

思考：

> 缺失一个指标时，是否一定应该删除整条实验？

---

## 方法2：使用统计值填补

例如使用 Accuracy 平均值：

```python
accuracy_mean = (
    df["accuracy"].mean()
)

df["accuracy"] = (
    df["accuracy"].fillna(
        accuracy_mean
    )
)
```

---

## 训练时间缺失

可以使用中位数：

```python
time_median = (
    df[
        "training_time"
    ].median()
)

df["training_time"] = (
    df[
        "training_time"
    ].fillna(
        time_median
    )
)
```

---

# 十八、再次检查

执行：

```python
print(
    df.isnull().sum()
)
```

检查是否仍存在缺失值。

---

# 十九、检查异常范围

理论上：

```text
0 ≤ Accuracy ≤ 1
Loss ≥ 0
Epoch > 0
Batch Size > 0
Learning Rate > 0
Training Time > 0
```

例如筛选 Accuracy 异常值：

```python
invalid_accuracy = df[
    (df["accuracy"] < 0)
    |
    (df["accuracy"] > 1)
]

print(invalid_accuracy)
```

---

# 二十、字符串清理

实际 CSV 中有时会出现：

```text
" MNIST "
"mnist"
"MNIST"
```

这种不一致问题。

可以：

```python
df["dataset"] = (
    df["dataset"]
    .str.strip()
)
```

进一步：

```python
print(
    df["dataset"].unique()
)
```

观察有哪些不同数据集。

---

# 二十一、unique()与nunique()

使用：

```python
print(
    df["model"].unique()
)
```

查看模型名称。

统计：

```python
print(
    df["model"].nunique()
)
```

得到不同模型数量。

同样查看：

```python
print(
    df["dataset"].unique()
)
```

---

# 二十二、保存清洗后的数据

将处理后的数据保存：

```python
df.to_csv(
    "data/ai_experiments_clean.csv",
    index=False,
    encoding="utf-8-sig"
)
```

最终形成：

```text
原始数据
ai_experiments.csv
      ↓
数据清洗
      ↓
清洗后数据
ai_experiments_clean.csv
```

---

# 二十三、任务2思考

回答：

1. 为什么真实数据分析前需要进行数据质量检查？
2. 缺失值是否一定应该删除？
3. 平均值与中位数填补有什么区别？
4. 重复数据为什么可能影响统计结果？
5. 为什么数据清洗通常发生在正式分析之前？

---

# 二十四、任务3：分组统计与数据可视化

## 1. 任务目标

掌握：

```text
groupby()
mean()
count()
agg()
```

以及 Matplotlib 基本绘图方法。

创建：

```text
task03_statistics_visualization.py
```

建议使用清洗后的：

```text
data/ai_experiments_clean.csv
```

---

# 二十五、整体指标统计

读取：

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv(
    "data/ai_experiments_clean.csv"
)
```

输出：

```python
print(
    df["accuracy"].mean()
)

print(
    df["accuracy"].max()
)

print(
    df["accuracy"].min()
)

print(
    df["loss"].mean()
)

print(
    df["training_time"].mean()
)
```

---

# 二十六、按模型分组

使用：

```python
model_accuracy = (
    df.groupby("model")[
        "accuracy"
    ].mean()
)

print(model_accuracy)
```

可以得到：

```text
不同模型
↓
平均Accuracy
```

---

# 二十七、同时统计多个指标

使用：

```python
model_summary = (
    df.groupby("model")
      .agg(
          {
              "accuracy": "mean",
              "loss": "mean",
              "training_time": "mean"
          }
      )
)

print(model_summary)
```

---

# 二十八、按数据集统计

例如：

```python
dataset_summary = (
    df.groupby("dataset")
      .agg(
          {
              "accuracy": "mean",
              "loss": "mean"
          }
      )
)

print(dataset_summary)
```

---

# 二十九、模型实验次数

使用：

```python
model_counts = (
    df["model"].value_counts()
)

print(model_counts)
```

---

# 三十、图1：Accuracy分布直方图

创建新的图：

```python
plt.figure()

plt.hist(
    df["accuracy"],
    bins=8
)

plt.xlabel("Accuracy")
plt.ylabel("Frequency")
plt.title(
    "Accuracy Distribution"
)

plt.tight_layout()
plt.show()
```

观察 Accuracy 大致集中在哪个区间。

---

# 三十一、图2：不同模型平均Accuracy

首先：

```python
model_accuracy = (
    df.groupby("model")[
        "accuracy"
    ].mean()
)
```

绘制：

```python
plt.figure()

model_accuracy.plot(
    kind="bar"
)

plt.xlabel("Model")
plt.ylabel("Mean Accuracy")
plt.title(
    "Mean Accuracy by Model"
)

plt.xticks(
    rotation=45
)

plt.tight_layout()
plt.show()
```

---

# 三十二、图3：Accuracy与Loss关系

绘制散点图：

```python
plt.figure()

plt.scatter(
    df["loss"],
    df["accuracy"]
)

plt.xlabel("Loss")
plt.ylabel("Accuracy")
plt.title(
    "Accuracy vs Loss"
)

plt.tight_layout()
plt.show()
```

观察：

> Loss 较低的实验是否往往具有较高 Accuracy？

这里只要求观察数据现象，不要求建立统计因果关系。

---

# 三十三、图4：训练时间与Accuracy

```python
plt.figure()

plt.scatter(
    df["training_time"],
    df["accuracy"]
)

plt.xlabel(
    "Training Time (min)"
)

plt.ylabel("Accuracy")

plt.title(
    "Training Time vs Accuracy"
)

plt.tight_layout()
plt.show()
```

思考：

> 训练时间更长是否一定意味着 Accuracy 更高？

---

# 三十四、保存图像

除了：

```python
plt.show()
```

还可以：

```python
plt.savefig(
    "accuracy_distribution.png",
    dpi=150
)
```

建议先：

```python
plt.tight_layout()
```

再保存。

---

# 三十五、可视化基本要求

本阶段绘图不追求复杂的视觉设计。

重点做到：

```text
图形选择合理
标题明确
横轴名称明确
纵轴名称明确
数据能够正确表达
```

避免为了“好看”加入过多无关装饰。

---

# 三十六、任务4：AI实验数据探索性分析

## 1. 任务背景

前面已经分别学习了：

```text
数据读取
数据检查
数据清洗
数据统计
数据可视化
```

本任务要求将这些步骤连接起来，完成一次相对完整的：

# AI实验数据探索性分析

即：

```text
EDA
Exploratory Data Analysis
```

---

## 2. 创建程序

创建：

```text
task04_ai_experiment_analysis.py
```

程序应按照完整数据分析流程组织。

---

# 三十七、第一步：读取数据

读取：

```text
data/ai_experiments.csv
```

输出：

```text
数据行数
数据列数
前5条数据
字段名称
数据类型
```

---

# 三十八、第二步：数据质量报告

程序自动输出：

```text
==============================
数据质量检查
==============================

数据记录数量：XX
字段数量：XX

缺失值：
accuracy         1
training_time    1
...

重复记录数量：1

模型数量：4
数据集数量：3
```

---

# 三十九、第三步：数据清洗

至少完成：

1. 删除完全重复记录；
2. 使用合理方法处理缺失的 Accuracy；
3. 使用合理方法处理缺失 Training Time；
4. 检查 Accuracy 是否在 0～1；
5. 检查 Loss 是否非负；
6. 清理模型和数据集名称两侧空格。

然后保存：

```text
data/ai_experiments_clean.csv
```

---

# 四十、第四步：整体实验分析

计算：

```text
实验总数
平均Accuracy
最高Accuracy
最低Accuracy
Accuracy标准差

平均Loss
最低Loss

平均训练时间
总训练时间

平均GPU显存占用
```

---

# 四十一、第五步：查找最佳实验

按照：

```text
Accuracy最高
```

查找最佳实验。

可以：

```python
best_index = (
    df["accuracy"].idxmax()
)

best_experiment = (
    df.loc[best_index]
)
```

输出：

```text
实验编号
模型
数据集
Epoch
Batch Size
Learning Rate
Accuracy
Loss
Training Time
GPU Memory
```

---

# 四十二、第六步：模型级分析

对每一种模型统计：

```text
实验次数
平均Accuracy
最高Accuracy
平均Loss
平均训练时间
```

可以使用：

```python
model_summary = (
    df.groupby("model")
      .agg(
          experiment_count=(
              "experiment_id",
              "count"
          ),
          mean_accuracy=(
              "accuracy",
              "mean"
          ),
          best_accuracy=(
              "accuracy",
              "max"
          ),
          mean_loss=(
              "loss",
              "mean"
          ),
          mean_time=(
              "training_time",
              "mean"
          )
      )
)
```

输出统计表。

---

# 四十三、第七步：数据集级分析

对不同数据集统计：

```text
实验数量
平均Accuracy
平均Loss
平均训练时间
```

观察：

> 不同数据集上的指标能否直接简单比较？

思考模型性能可能受到：

```text
数据规模
任务难度
模型结构
训练参数
```

等因素影响。

---

# 四十四、第八步：达标实验筛选

规定：

```text
Accuracy ≥ 0.90
```

为基本达标。

筛选：

```python
qualified = df[
    df["accuracy"] >= 0.90
]
```

统计：

```text
达标实验数量
达标率
```

进一步筛选：

```text
Accuracy ≥ 0.90
且
Loss < 0.20
```

---

# 四十五、第九步：生成至少4幅图

至少绘制：

### 图1

```text
Accuracy分布直方图
```

### 图2

```text
不同模型平均Accuracy柱状图
```

### 图3

```text
Accuracy与Loss散点图
```

### 图4

```text
Training Time与Accuracy散点图
```

要求每幅图均包含：

```text
标题
横轴标签
纵轴标签
```

---

# 四十六、第十步：输出分析结论

根据程序结果，至少回答以下问题：

1. 哪种模型的平均 Accuracy 最高？
2. 哪次实验获得最高 Accuracy？
3. 哪种模型平均训练时间最长？
4. Accuracy 与 Loss 是否表现出明显的反向变化趋势？
5. 训练时间更长是否一定能获得更高 Accuracy？
6. 是否存在 Accuracy 较高但训练时间也明显较长的模型？
7. 数据中是否存在明显异常或缺失问题？

注意：

> 分析结论必须由实际数据结果支持，不应只根据模型名称主观判断。

---

# 四十七、参考分析流程

完整程序推荐组织为：

```text
读取CSV
   ↓
查看数据
   ↓
数据质量检查
   ↓
数据清洗
   ↓
保存Clean CSV
   ↓
整体统计
   ↓
模型分组
   ↓
数据集分组
   ↓
实验筛选
   ↓
最佳实验
   ↓
数据可视化
   ↓
分析结论
```

这就是一个基本的数据分析工作流。

---

# 四十八、拓展任务：模型性能与计算代价分析

创建：

```text
extension_model_efficiency.py
```

人工智能实验不仅需要关注：

```text
Accuracy
```

还需要考虑：

```text
训练时间
GPU显存占用
```

本任务要求尝试从：

# 性能—效率

两个角度比较模型。

---

## 1. 模型平均指标

对每种模型计算：

```text
平均Accuracy
平均Loss
平均Training Time
平均GPU Memory
```

---

## 2. 创建简单效率指标

为了练习数据计算，可以人为定义一个简单指标：

```python
df["efficiency_score"] = (
    df["accuracy"]
    / df["training_time"]
)
```

> 该指标仅用于本次编程与数据分析训练，并不是通用或标准的机器学习评价指标。

---

## 3. 找出效率最高实验

使用：

```python
best_efficiency_index = (
    df["efficiency_score"]
      .idxmax()
)
```

输出对应实验。

---

## 4. 比较两种排序

分别按照：

```text
Accuracy
```

和：

```text
Efficiency Score
```

对实验进行排序。

观察：

> Accuracy最高的实验是否同时也是效率最高的实验？

---

## 5. 绘制散点图

绘制：

```text
横轴：Training Time
纵轴：Accuracy
```

观察不同实验在：

```text
性能
和
计算时间
```

两个维度上的关系。

---

## 6. 提高要求

尝试同时考虑：

```text
Accuracy
Training Time
GPU Memory
```

自行设计一个新的综合指标。

但必须在程序注释中说明：

1. 指标是如何计算的；
2. 为什么这样设计；
3. 该指标存在什么局限。

---

# 四十九、本次实训提交内容

本次实训至少完成：

```text
lab14-pandas-visualization/
│
├── task01_dataframe_basics.py
├── task02_data_cleaning.py
├── task03_statistics_visualization.py
├── task04_ai_experiment_analysis.py
│
└── data/
    ├── ai_experiments.csv
    └── ai_experiments_clean.csv
```

拓展任务可以创建：

```text
extension_model_efficiency.py
```

如果保存分析图像，也可以自行创建：

```text
outputs/
```

用于保存：

```text
.png
```

等结果文件。

---

# 五十、实训检查

完成本次实训后，应能够：

* [ ] 正确导入 Pandas；
* [ ] 使用 `pd.read_csv()` 读取 CSV；
* [ ] 理解 `DataFrame` 和 `Series`；
* [ ] 使用 `head()` 和 `tail()` 查看数据；
* [ ] 使用 `shape` 查看数据规模；
* [ ] 使用 `columns` 查看列名；
* [ ] 使用 `dtypes` 和 `info()` 检查数据类型；
* [ ] 使用 `describe()` 查看统计信息；
* [ ] 使用列名访问数据；
* [ ] 使用 `iloc` 获取指定行；
* [ ] 使用布尔条件筛选数据；
* [ ] 使用多个条件筛选数据；
* [ ] 使用 `sort_values()` 排序；
* [ ] 使用 `isnull()` 检查缺失值；
* [ ] 使用 `duplicated()` 检查重复数据；
* [ ] 使用 `drop_duplicates()` 删除重复数据；
* [ ] 使用 `dropna()` 和 `fillna()` 处理缺失值；
* [ ] 使用字符串方法清理文本数据；
* [ ] 使用 `unique()` 和 `nunique()`；
* [ ] 使用 `groupby()` 完成分组统计；
* [ ] 使用 `agg()` 对多个指标进行统计；
* [ ] 使用 `value_counts()` 完成类别统计；
* [ ] 使用 Matplotlib 绘制直方图；
* [ ] 绘制柱状图；
* [ ] 绘制散点图；
* [ ] 为图形设置标题和坐标轴名称；
* [ ] 使用 `to_csv()` 保存处理后的数据；
* [ ] 完成基本的数据探索性分析流程；
* [ ] 根据数据分析结果形成基本结论。

---

# 五十一、本次实训知识路线

```text
CSV
 ↓
Pandas
 ↓
DataFrame
 ↓
数据查看
 ↓
数据类型
 ↓
缺失值
 ↓
重复值
 ↓
数据清洗
 ↓
条件筛选
 ↓
排序
 ↓
groupby
 ↓
统计分析
 ↓
Matplotlib
 ↓
数据可视化
 ↓
EDA
 ↓
AI实验数据分析
```

---

# 五十二、Lab13与Lab14的关系

## Lab13

主要处理：

```text
纯数值数组
```

例如：

```python
X[:, 0]
```

重点是：

```text
ndarray
shape
axis
向量化
布尔索引
```

---

## Lab14

进一步处理：

```text
具有列名的表格型数据
```

例如：

```python
df["accuracy"]
```

重点转变为：

```text
DataFrame
数据清洗
分组统计
可视化
探索性分析
```

因此形成：

```text
NumPy
数值计算基础
     ↓
Pandas
表格数据处理
     ↓
Matplotlib
结果可视化
```

---

# 五十三、从数据处理到机器学习

到 Lab14 结束时，我们已经能够完成：

```text
读取数据
   ↓
理解数据
   ↓
发现问题
   ↓
清洗数据
   ↓
选择特征
   ↓
统计分析
   ↓
可视化
```

但是目前程序仍然主要回答：

```text
“数据是什么样的？”
```

以及：

```text
“数据中有什么规律？”
```

下一阶段将进入：

# Lab 15：Python机器学习基础实践

届时将进一步使用：

```text
Scikit-learn
```

完成：

```text
数据集
  ↓
特征 X
  ↓
标签 y
  ↓
训练集 / 测试集
  ↓
模型
  ↓
fit()
  ↓
predict()
  ↓
评价指标
```

程序将第一次真正完成一个完整的：

# 机器学习训练与预测流程
