# Lab 08：字典与集合

## 一、实训目的

通过本次实训掌握 Python 中字典和集合两种常用数据结构，理解“键—值对应关系”和“唯一元素集合”的基本思想，能够根据实际问题选择合适的数据结构组织和处理数据。

在 Lab 07 中，我们已经能够使用列表保存一组数据：

```python
scores = [85, 92, 78, 96]
```

但是对于一个学生、一个模型或一次 AI 实验，仅仅保存若干数值通常无法清楚说明每个数据代表什么。

例如：

```python
experiment = ["SimpleCNN", "MNIST", 0.952, 0.138]
```

虽然可以保存数据，但仅从数据本身很难直接理解每个位置的含义。

使用字典以后，可以表示为：

```python
experiment = {
    "model": "SimpleCNN",
    "dataset": "MNIST",
    "accuracy": 0.952,
    "loss": 0.138
}
```

数据的含义会更加清晰。

本次实训进一步建立：

```text
一组数据
   ↓
键—值关系
   ↓
结构化对象
   ↓
字典
   ↓
唯一元素
   ↓
集合
   ↓
列表 + 字典 + 集合
   ↓
结构化数据处理
```

的程序设计思维。

---

## 二、实训内容

本次实训主要包括：

1. 字典的创建、访问、增加、修改和删除；
2. 字典的遍历和结构化信息组织；
3. 集合的创建、去重和基本集合运算；
4. 综合使用列表、字典和集合处理 AI 实验数据。

本次实训设置 **4 个必做任务** 和 **1 个拓展任务**。

---

# 三、任务1：字典的创建与基本操作

## 1. 任务目标

掌握字典的基本操作：

```text
创建
访问
增加
修改
删除
成员判断
```

理解字典中的：

```text
key → value
```

对应关系。

---

## 2. 创建程序

创建：

```text
task01_dictionary_basics.py
```

首先定义一个学生信息字典：

```python
student = {
    "name": "张三",
    "student_id": "20260001",
    "major": "人工智能",
    "python_score": 88
}

print(student)
print(type(student))
```

运行程序并观察结果。

---

## 3. 访问字典数据

分别输出：

```python
print(student["name"])
print(student["major"])
print(student["python_score"])
```

观察字典访问数据的方式与列表有什么不同。

列表通常使用：

```python
scores[0]
```

字典则可以使用：

```python
student["name"]
```

因此字典中的数据通常具有更加明确的含义。

---

## 4. 使用get()访问数据

尝试：

```python
print(student.get("name"))
print(student.get("python_score"))
```

然后尝试：

```python
print(student.get("email"))
```

观察结果。

进一步尝试：

```python
print(student.get("email", "暂无邮箱"))
```

思考：

```python
student["email"]
```

与：

```python
student.get("email")
```

在键不存在时有什么不同。

---

## 5. 增加数据

为学生增加邮箱：

```python
student["email"] = "zhangsan@example.com"

print(student)
```

再增加：

```python
student["grade"] = 2024
```

观察字典内容变化。

---

## 6. 修改数据

修改 Python 成绩：

```python
student["python_score"] = 92

print(student)
```

观察：

> 当指定的 key 已经存在时，赋值操作会修改原来的 value。

---

## 7. 删除数据

尝试：

```python
removed_value = student.pop("email")

print(student)
print(f"删除的数据：{removed_value}")
```

也可以使用：

```python
del student["grade"]
```

观察字典变化。

---

## 8. 判断键是否存在

使用：

```python
if "python_score" in student:
    print("字典中包含Python成绩")
```

继续判断：

```python
if "ai_score" not in student:
    print("字典中暂时没有AI课程成绩")
```

---

## 9. 思考

回答以下问题：

1. 字典和列表访问数据的方式有什么不同？
2. 一个字典中的 key 是否可以重复？
3. 如果使用已有 key 再次赋值，会发生什么？
4. 为什么学生信息、模型参数等数据适合使用字典保存？

---

# 四、任务2：字典遍历与结构化数据

## 1. 任务目标

掌握：

```python
keys()
values()
items()
```

以及字典遍历方法。

进一步理解如何使用字典描述一个完整对象。

---

## 2. 创建程序

创建：

```text
task02_dictionary_processing.py
```

定义一个 AI 模型信息字典：

```python
model = {
    "name": "SimpleCNN",
    "dataset": "MNIST",
    "epochs": 20,
    "batch_size": 32,
    "learning_rate": 0.001,
    "accuracy": 0.9568
}
```

---

## 3. 查看所有键

```python
print(model.keys())
```

遍历：

```python
for key in model.keys():
    print(key)
```

也可以简写为：

```python
for key in model:
    print(key)
```

---

## 4. 查看所有值

```python
print(model.values())
```

遍历：

```python
for value in model.values():
    print(value)
```

---

## 5. 同时遍历键和值

使用：

```python
for key, value in model.items():
    print(f"{key}: {value}")
```

观察：

```python
items()
```

如何同时获得 key 和 value。

---

## 6. 完成AI模型信息卡

将字典信息输出为：

```text
========================================
             AI模型信息
========================================

模型名称：SimpleCNN
数据集：MNIST

Epoch：20
Batch Size：32
Learning Rate：0.001

Accuracy：0.9568

========================================
```

---

## 7. 根据字典数据完成判断

例如：

```python
if model["accuracy"] >= 0.95:
    print("模型准确率表现优秀")
elif model["accuracy"] >= 0.90:
    print("模型准确率表现良好")
else:
    print("模型仍需进一步优化")
```

---

## 8. 使用列表保存多个字典

现在假设有三次 AI 实验：

```python
experiments = [
    {
        "model": "SimpleCNN",
        "accuracy": 0.92,
        "loss": 0.20
    },
    {
        "model": "ResNet18",
        "accuracy": 0.95,
        "loss": 0.15
    },
    {
        "model": "MLP",
        "accuracy": 0.88,
        "loss": 0.28
    }
]
```

输出：

```python
print(experiments)
print(type(experiments))
print(type(experiments[0]))
```

观察：

```text
experiments
```

是什么类型；

而：

```text
experiments[0]
```

又是什么类型。

---

## 9. 遍历多个实验

```python
for experiment in experiments:
    print(
        f"模型：{experiment['model']}，"
        f"Accuracy：{experiment['accuracy']:.4f}，"
        f"Loss：{experiment['loss']:.4f}"
    )
```

这形成了一种非常常见的数据结构：

```text
列表
 ↓
多个字典
 ↓
多条结构化记录
```

例如：

```text
实验1 → 字典
实验2 → 字典
实验3 → 字典
```

---

# 五、任务3：集合与数据去重

## 1. 任务目标

掌握集合的：

* 创建；
* 添加；
* 删除；
* 成员判断；
* 自动去重；
* 交集；
* 并集；
* 差集。

理解集合适合处理：

```text
唯一元素
```

和：

```text
集合关系
```

---

## 2. 创建程序

创建：

```text
task03_set_operations.py
```

定义：

```python
datasets = {
    "MNIST",
    "CIFAR10",
    "ImageNet"
}

print(datasets)
print(type(datasets))
```

---

## 3. 集合的唯一性

尝试：

```python
datasets = {
    "MNIST",
    "CIFAR10",
    "MNIST",
    "ImageNet",
    "CIFAR10"
}

print(datasets)
```

观察：

```text
MNIST
CIFAR10
```

是否会重复出现。

---

## 4. 使用集合实现列表去重

假设：

```python
model_names = [
    "CNN",
    "MLP",
    "CNN",
    "ResNet",
    "MLP",
    "Transformer"
]
```

转换为集合：

```python
unique_models = set(model_names)

print(model_names)
print(unique_models)
```

思考：

> 为什么集合特别适合完成“去重”操作？

---

## 5. 添加元素

```python
datasets.add("FashionMNIST")

print(datasets)
```

---

## 6. 删除元素

尝试：

```python
datasets.remove("MNIST")
```

也可以：

```python
datasets.discard("CIFAR10")
```

观察集合变化。

思考：

```text
remove()
```

与：

```text
discard()
```

在删除不存在的元素时有什么不同。

---

## 7. 成员判断

```python
if "ImageNet" in datasets:
    print("包含ImageNet数据集")
```

集合中的成员判断在数据量较大时也是一种非常常见的操作。

---

## 8. 集合运算

假设两个学习小组分别使用过以下 AI 数据集：

```python
group_a = {
    "MNIST",
    "CIFAR10",
    "ImageNet"
}

group_b = {
    "MNIST",
    "FashionMNIST",
    "ImageNet"
}
```

---

### 并集

```python
all_datasets = group_a | group_b

print(all_datasets)
```

表示：

```text
两个小组使用过的所有数据集
```

---

### 交集

```python
common_datasets = group_a & group_b

print(common_datasets)
```

表示：

```text
两个小组都使用过的数据集
```

---

### 差集

```python
only_a = group_a - group_b

print(only_a)
```

表示：

```text
只有A组使用过的数据集
```

---

## 9. 思考

根据应用场景思考：

| 问题           | 更适合的数据结构 |
| ------------ | -------- |
| 保存5次Accuracy | 列表       |
| 保存一个模型的多个属性  | 字典       |
| 保存不重复的数据集名称  | 集合       |
| 保存多个模型的完整信息  | 列表 + 字典  |

---

# 六、任务4：AI实验信息管理与分析

## 1. 任务背景

一次 AI 实验通常具有多个属性，例如：

```text
模型名称
数据集
Epoch
Batch Size
Accuracy
Loss
```

如果需要保存多次实验，仅使用若干独立列表：

```python
models = [...]
accuracies = [...]
losses = [...]
```

虽然可以完成任务，但不同属性之间的对应关系不够直观。

更合适的结构是：

```text
列表
  ↓
多个实验字典
```

例如：

```python
experiments = [
    {
        "model": "CNN",
        "dataset": "MNIST",
        "accuracy": 0.92,
        "loss": 0.18
    },
    {
        "model": "MLP",
        "dataset": "MNIST",
        "accuracy": 0.88,
        "loss": 0.25
    }
]
```

本任务要求完成一个：

# AI实验信息管理与分析程序

---

## 2. 创建程序

创建：

```text
task04_ai_experiment_manager.py
```

---

## 3. 输入实验数量

首先：

```python
experiment_count = int(input("请输入实验数量："))
```

创建空列表：

```python
experiments = []
```

---

## 4. 输入每次实验信息

每次实验输入：

```text
模型名称
数据集名称
Epoch
Batch Size
Accuracy
Loss
```

参考：

```python
for i in range(1, experiment_count + 1):

    print()
    print(f"---------- Experiment {i} ----------")

    model = input("模型名称：")
    dataset = input("数据集名称：")
    epochs = int(input("Epoch："))
    batch_size = int(input("Batch Size："))

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
```

---

## 5. 将一次实验保存为字典

创建：

```python
experiment = {
    "model": model,
    "dataset": dataset,
    "epochs": epochs,
    "batch_size": batch_size,
    "accuracy": accuracy,
    "loss": loss
}
```

然后：

```python
experiments.append(experiment)
```

最终：

```text
experiments
```

中保存所有实验。

---

## 6. 输出全部实验

```python
print()
print("=" * 60)
print("AI实验记录")
print("=" * 60)

for i in range(len(experiments)):

    experiment = experiments[i]

    print(
        f"Experiment {i + 1}: "
        f"{experiment['model']} | "
        f"{experiment['dataset']} | "
        f"Accuracy={experiment['accuracy']:.4f} | "
        f"Loss={experiment['loss']:.4f}"
    )
```

---

## 7. 统计平均Accuracy

```python
total_accuracy = 0

for experiment in experiments:
    total_accuracy += experiment["accuracy"]

average_accuracy = total_accuracy / len(experiments)
```

输出：

```python
print(f"平均Accuracy：{average_accuracy:.4f}")
```

---

## 8. 查找最佳实验

先：

```python
best_experiment = experiments[0]
```

然后遍历：

```python
for experiment in experiments:

    if experiment["accuracy"] > best_experiment["accuracy"]:
        best_experiment = experiment
```

最终：

```python
print("最佳实验：")
print(f"模型：{best_experiment['model']}")
print(f"数据集：{best_experiment['dataset']}")
print(f"Accuracy：{best_experiment['accuracy']:.4f}")
print(f"Loss：{best_experiment['loss']:.4f}")
```

---

## 9. 筛选达到目标的实验

输入：

```python
target_accuracy = float(input("请输入目标Accuracy："))
```

输出所有满足：

```text
Accuracy ≥ target_accuracy
```

的实验。

参考：

```python
qualified_count = 0

for experiment in experiments:

    if experiment["accuracy"] >= target_accuracy:

        qualified_count += 1

        print(
            f"{experiment['model']} | "
            f"{experiment['dataset']} | "
            f"Accuracy={experiment['accuracy']:.4f}"
        )
```

---

## 10. 使用集合统计使用过的数据集

创建：

```python
datasets = set()
```

遍历：

```python
for experiment in experiments:
    datasets.add(experiment["dataset"])
```

输出：

```python
print(f"本次实验共涉及 {len(datasets)} 个不同数据集：")

for dataset in datasets:
    print(dataset)
```

这里就同时使用了：

```text
列表
+
字典
+
集合
```

三种数据结构。

---

## 11. 统计使用过的模型

同样可以：

```python
models = set()

for experiment in experiments:
    models.add(experiment["model"])
```

输出不同模型数量。

---

## 12. 最终报告

程序最终可以输出类似：

```text
============================================================
                  AI实验统计报告
============================================================

实验总数：5

------------------- 实验记录 -------------------

Experiment 1: CNN | MNIST | Accuracy=0.9200 | Loss=0.1800
Experiment 2: MLP | MNIST | Accuracy=0.8800 | Loss=0.2500
Experiment 3: ResNet18 | CIFAR10 | Accuracy=0.9400 | Loss=0.1600
Experiment 4: CNN | CIFAR10 | Accuracy=0.9100 | Loss=0.2100
Experiment 5: ResNet18 | MNIST | Accuracy=0.9500 | Loss=0.1400

------------------- 统计结果 -------------------

平均Accuracy：0.9200

最佳实验：
模型：ResNet18
数据集：MNIST
Accuracy：0.9500
Loss：0.1400

------------------- 数据概况 -------------------

不同模型数量：3
不同数据集数量：2

模型：
CNN
MLP
ResNet18

数据集：
MNIST
CIFAR10

============================================================
```

---

## 13. 数据结构分析

本程序中：

### 列表

```python
experiments = []
```

负责：

```text
保存多次实验
```

### 字典

```python
experiment = {
    ...
}
```

负责：

```text
描述一次完整实验
```

### 集合

```python
models = set()
datasets = set()
```

负责：

```text
保存不重复的模型名称和数据集名称
```

因此可以理解为：

```text
列表
负责“多个”

字典
负责“属性”

集合
负责“唯一”
```

这是本次实训最需要理解的核心思想。

---

# 七、拓展任务：两个实验组的数据集合分析

创建：

```text
extension_group_analysis.py
```

假设两个实验小组分别完成了以下模型：

```python
group_a_models = {
    "CNN",
    "MLP",
    "ResNet18",
    "Transformer"
}

group_b_models = {
    "CNN",
    "ResNet18",
    "ViT",
    "LSTM"
}
```

要求完成以下分析。

---

## 1. 两组一共使用过哪些模型

使用并集：

```python
all_models = group_a_models | group_b_models
```

---

## 2. 两组共同使用过哪些模型

使用交集：

```python
common_models = group_a_models & group_b_models
```

---

## 3. 只有A组使用过哪些模型

```python
only_a = group_a_models - group_b_models
```

---

## 4. 只有B组使用过哪些模型

```python
only_b = group_b_models - group_a_models
```

---

## 5. 输出分析报告

例如：

```text
========================================
          两组AI实验模型分析
========================================

A组模型：
CNN
MLP
ResNet18
Transformer

B组模型：
CNN
ResNet18
ViT
LSTM

两组共同使用：
CNN
ResNet18

仅A组使用：
MLP
Transformer

仅B组使用：
ViT
LSTM

两组合计涉及模型数量：6

========================================
```

---

## 提高要求

自行增加两个数据集集合：

```python
group_a_datasets = {...}
group_b_datasets = {...}
```

对两个小组使用的数据集继续进行：

```text
并集
交集
差集
```

分析。

---

# 八、本次实训提交内容

本次实训至少完成：

```text
lab08-dict-set/
├── task01_dictionary_basics.py
├── task02_dictionary_processing.py
├── task03_set_operations.py
└── task04_ai_experiment_manager.py
```

拓展任务可以创建：

```text
extension_group_analysis.py
```

---

# 九、实训检查

完成本次实训后，应能够：

* [ ] 正确创建字典；
* [ ] 理解字典中的 key 和 value；
* [ ] 使用 key 访问字典数据；
* [ ] 使用 `get()` 获取字典数据；
* [ ] 向字典中增加新的键值对；
* [ ] 修改字典中的数据；
* [ ] 删除字典中的数据；
* [ ] 使用 `keys()`、`values()` 和 `items()`；
* [ ] 使用循环遍历字典；
* [ ] 使用字典描述一个结构化对象；
* [ ] 使用列表保存多个字典；
* [ ] 正确创建集合；
* [ ] 理解集合中元素不重复的特点；
* [ ] 使用集合完成数据去重；
* [ ] 使用并集、交集和差集；
* [ ] 根据实际问题选择列表、字典或集合；
* [ ] 综合使用列表、字典和集合组织 AI 实验数据；
* [ ] 完成简单的结构化实验数据统计与筛选。

---

# 十、本次实训知识路线

```text
列表
 ↓
一组数据
 ↓
字典
 ↓
一个对象的多个属性
 ↓
列表 + 字典
 ↓
多条结构化记录
 ↓
集合
 ↓
唯一数据与集合关系
 ↓
列表 + 字典 + 集合
 ↓
AI实验信息管理
```

---

# 十一、数据结构选择

学习到目前为止，可以根据问题特点选择不同的数据结构：

```text
需要按顺序保存一组数据
        ↓
       list

需要描述一个对象的多个属性
        ↓
       dict

需要保存不重复的数据
        ↓
       set

需要保存多个结构化对象
        ↓
    list + dict
```

例如：

```python
accuracies = [0.91, 0.93, 0.95]
```

适合保存：

```text
多次Accuracy
```

而：

```python
model = {
    "name": "CNN",
    "accuracy": 0.95
}
```

适合描述：

```text
一个模型
```

进一步：

```python
experiments = [
    {
        "model": "CNN",
        "accuracy": 0.95
    },
    {
        "model": "MLP",
        "accuracy": 0.88
    }
]
```

则适合表示：

```text
多次结构化实验记录
```

---

# 十二、阶段衔接

Lab07 和 Lab08 解决了程序设计中非常重要的：

# 数据组织问题

学习路线已经由：

```text
单个变量
   ↓
字符串
   ↓
列表 / 元组
   ↓
字典
   ↓
集合
   ↓
组合数据结构
```

发展到：

```text
结构化数据
```

完成本次实训后，将进入：

# Lab 09：数据结构综合应用

Lab09 不再重点学习新的数据结构语法，而是综合使用：

```text
字符串
+
列表
+
元组
+
字典
+
集合
+
条件判断
+
循环
```

完成一个规模更大的数据管理程序。

届时重点将从：

```text
“这个数据结构怎么使用？”
```

转变为：

```text
“面对一个实际问题，
应该怎样选择和组合数据结构？”
```
