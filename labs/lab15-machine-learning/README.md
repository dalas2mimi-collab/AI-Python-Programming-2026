# Lab 15：Python机器学习基础实践

## 一、实训目的

通过本次实训掌握使用 Scikit-learn 完成基础机器学习分类任务的基本流程，理解特征、标签、训练集、测试集、模型训练、模型预测和模型评价等基本概念，能够使用 Python 独立完成一个简单的监督学习分类程序。

前面的 Lab 已经完成：

```text
Lab13
NumPy
↓
数值数据处理

Lab14
Pandas + Matplotlib
↓
数据读取、清洗、分析与可视化
```

从本次实验开始进一步进入：

```text
数据
 ↓
特征 X
 ↓
标签 y
 ↓
训练集 / 测试集
 ↓
数据预处理
 ↓
机器学习模型
 ↓
fit()
 ↓
predict()
 ↓
模型评价
 ↓
新样本预测
```

本次实验重点不是深入推导机器学习算法，而是掌握：

> **使用 Python 完成一个规范、完整的基础机器学习工作流程。**

---

## 二、实训内容

本次实训主要包括：

1. 认识机器学习中的特征 `X` 与标签 `y`；
2. 使用 Scikit-learn 内置数据集；
3. 将数据划分为训练集和测试集；
4. 使用 `StandardScaler` 对特征进行标准化；
5. 使用分类模型完成训练；
6. 使用 `fit()` 和 `predict()`；
7. 使用 Accuracy 评价分类结果；
8. 使用混淆矩阵和分类报告分析结果；
9. 比较多个机器学习模型；
10. 使用训练后的模型预测新样本。

本次实训设置：

**4 个必做任务 + 1 个拓展任务。**

---

# 三、实验准备

本次实验主要使用：

```text
numpy
pandas
matplotlib
scikit-learn
```

首先测试：

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import sklearn

print(sklearn.__version__)
```

如果 Scikit-learn 尚未安装，可以在终端执行：

```bash
pip install scikit-learn
```

---

# 四、实验数据：Iris鸢尾花数据集

本次实验使用 Scikit-learn 内置的：

```text
Iris Dataset
```

这是一个经典的多分类数据集。

数据包含：

```text
150个样本
4个数值特征
3个类别
```

每个样本具有4个特征：

```text
sepal length
sepal width
petal length
petal width
```

对应3种鸢尾花类别：

```text
setosa
versicolor
virginica
```

本实验不要求深入研究鸢尾花本身，而是利用该数据集学习机器学习程序的完整执行流程。

---

# 五、任务1：认识机器学习数据与数据集划分

## 1. 任务目标

理解机器学习中的：

```text
样本
特征
标签
X
y
训练集
测试集
```

并掌握：

```python
train_test_split()
```

的基本使用方法。

---

## 2. 创建程序

创建：

```text
task01_dataset_split.py
```

首先导入：

```python
from sklearn.datasets import load_iris
```

读取数据：

```python
iris = load_iris(
    as_frame=True
)
```

---

## 3. 查看数据集

输出：

```python
print(iris.data.head())
```

查看特征。

再输出：

```python
print(iris.target.head())
```

查看标签。

---

## 4. 获取X和y

定义：

```python
X = iris.data
y = iris.target
```

可以理解：

```text
X
↓
模型的输入特征

y
↓
模型需要学习预测的目标
```

查看：

```python
print(X.shape)
print(y.shape)
```

---

## 5. 查看特征名称

```python
print(
    iris.feature_names
)
```

---

## 6. 查看类别名称

```python
print(
    iris.target_names
)
```

---

## 7. 查看完整DataFrame

使用：

```python
df = iris.frame

print(df.head())
```

观察最后一列：

```text
target
```

的含义。

---

# 六、理解“样本 × 特征”

输出：

```python
print(X.shape)
```

结果为：

```text
(150, 4)
```

可以理解为：

```text
150个样本
×
4个特征
```

这与 Lab13 中学习的：

```text
二维NumPy数组
=
样本 × 特征
```

完全对应。

---

# 七、查看类别分布

使用：

```python
print(
    y.value_counts()
)
```

观察每个类别包含多少个样本。

进一步：

```python
print(
    y.value_counts(
        normalize=True
    )
)
```

观察类别比例。

---

# 八、划分训练集和测试集

导入：

```python
from sklearn.model_selection import train_test_split
```

划分：

```python
X_train, X_test, y_train, y_test = (
    train_test_split(
        X,
        y,
        test_size=0.2,
        random_state=42,
        stratify=y
    )
)
```

---

## 1. 查看数据形状

输出：

```python
print(
    f"X_train: {X_train.shape}"
)

print(
    f"X_test: {X_test.shape}"
)

print(
    f"y_train: {y_train.shape}"
)

print(
    f"y_test: {y_test.shape}"
)
```

观察：

```text
150个样本
↓
训练集 + 测试集
```

的变化。

---

# 九、训练集与测试集的基本作用

可以初步理解为：

```text
全部数据
   ↓
train_test_split()
   ↓
┌───────────────┬───────────────┐
│               │               │
训练集          测试集
│               │
用于模型学习    用于模型评价
│               │
X_train         X_test
y_train         y_test
```

模型不能只完成：

```text
训练
```

还需要利用未参与当前训练的数据检查预测效果。

---

# 十、random_state

本实验使用：

```python
random_state=42
```

主要是为了让随机划分结果具有可重复性，方便不同学生运行程序时比较结果。

尝试：

```python
random_state=1
```

或者：

```python
random_state=100
```

观察数据划分和后续模型结果是否发生变化。

---

# 十一、stratify

使用：

```python
stratify=y
```

可以使训练集和测试集中的不同类别保持较合理的比例关系。

分别输出：

```python
print(
    y_train.value_counts()
)

print(
    y_test.value_counts()
)
```

观察三个类别在两个数据集中的分布。

---

# 十二、任务1思考

完成后回答：

1. 什么是样本？
2. 什么是特征？
3. 什么是标签？
4. `X` 和 `y` 分别表示什么？
5. 为什么要划分训练集和测试集？
6. `test_size=0.2` 表示什么？
7. `random_state` 有什么作用？
8. 为什么不能只在训练数据上评价模型？

---

# 十三、任务2：完成第一个机器学习分类模型

## 1. 任务目标

掌握机器学习程序中最核心的：

```text
创建模型
   ↓
fit()
   ↓
predict()
   ↓
评价
```

流程。

本任务使用：

# Logistic Regression

完成鸢尾花分类。

---

## 2. 创建程序

创建：

```text
task02_first_classifier.py
```

---

## 3. 导入需要的工具

```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression

from sklearn.pipeline import make_pipeline

from sklearn.metrics import accuracy_score
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
```

---

# 十四、读取数据

```python
iris = load_iris(
    as_frame=True
)

X = iris.data
y = iris.target
```

---

# 十五、划分数据

```python
X_train, X_test, y_train, y_test = (
    train_test_split(
        X,
        y,
        test_size=0.2,
        random_state=42,
        stratify=y
    )
)
```

---

# 十六、标准化与模型组合

创建：

```python
model = make_pipeline(
    StandardScaler(),
    LogisticRegression(
        max_iter=1000
    )
)
```

这里形成：

```text
原始特征
   ↓
StandardScaler
   ↓
标准化特征
   ↓
LogisticRegression
   ↓
分类结果
```

---

# 十七、训练模型

执行：

```python
model.fit(
    X_train,
    y_train
)
```

这是第一次正式使用：

# fit()

可以将：

```text
fit
```

理解为：

> 让模型利用训练数据学习特征与标签之间的关系。

---

# 十八、模型预测

执行：

```python
y_pred = model.predict(
    X_test
)
```

查看：

```python
print(y_pred)
```

再查看真实标签：

```python
print(
    y_test.to_numpy()
)
```

比较：

```text
真实标签
和
预测标签
```

---

# 十九、Accuracy

导入：

```python
from sklearn.metrics import accuracy_score
```

计算：

```python
accuracy = accuracy_score(
    y_test,
    y_pred
)

print(
    f"Test Accuracy: "
    f"{accuracy:.4f}"
)
```

可以简单理解：

```text
Accuracy
=
预测正确样本数
────────────
全部测试样本数
```

---

# 二十、查看预测结果

创建：

```python
results = X_test.copy()
```

增加：

```python
results["true_label"] = (
    y_test
)

results["predicted_label"] = (
    y_pred
)
```

输出：

```python
print(results)
```

---

# 二十一、查看预测类别名称

可以：

```python
results[
    "true_class"
] = iris.target_names[
    y_test
]

results[
    "predicted_class"
] = iris.target_names[
    y_pred
]
```

输出：

```python
print(
    results[
        [
            "true_class",
            "predicted_class"
        ]
    ]
)
```

---

# 二十二、查看错误预测

筛选：

```python
errors = results[
    results["true_class"]
    !=
    results["predicted_class"]
]
```

输出：

```python
print(errors)
```

思考：

> 模型是否能够做到100%正确？

---

# 二十三、混淆矩阵

使用：

```python
cm = confusion_matrix(
    y_test,
    y_pred
)

print(cm)
```

混淆矩阵可以帮助观察：

```text
哪些类别预测正确
哪些类别容易互相混淆
```

---

# 二十四、分类报告

使用：

```python
print(
    classification_report(
        y_test,
        y_pred,
        target_names=
            iris.target_names,
        digits=4
    )
)
```

报告中可以看到：

```text
precision
recall
f1-score
support
```

本次实验要求：

* 能够运行并查看这些指标；
* 初步知道这些指标用于评价分类结果；

暂时不要求深入推导所有公式。

---

# 二十五、理解机器学习API

到这里，一个基础 Scikit-learn 模型的程序已经可以概括为：

```python
model = ...
```

↓

```python
model.fit(
    X_train,
    y_train
)
```

↓

```python
y_pred = model.predict(
    X_test
)
```

↓

```python
accuracy_score(
    y_test,
    y_pred
)
```

也就是：

```text
定义模型
   ↓
fit
   ↓
predict
   ↓
evaluate
```

这是后续学习大量机器学习模型都会反复使用的基本流程。

---

# 二十六、任务3：多模型训练与比较

## 1. 任务背景

解决同一个分类问题时，可以选择不同的机器学习模型。

本任务不深入讨论每个算法的数学推导，而是重点练习：

```text
相同数据
   ↓
多个模型
   ↓
统一训练
   ↓
统一预测
   ↓
统一评价
   ↓
比较结果
```

---

## 2. 创建程序

创建：

```text
task03_model_comparison.py
```

---

# 二十七、使用三个分类模型

本次比较：

```text
Logistic Regression
K-Nearest Neighbors
Decision Tree
```

导入：

```python
from sklearn.linear_model import LogisticRegression

from sklearn.neighbors import KNeighborsClassifier

from sklearn.tree import DecisionTreeClassifier

from sklearn.preprocessing import StandardScaler

from sklearn.pipeline import make_pipeline
```

---

# 二十八、创建模型字典

利用前面学习过的字典：

```python
models = {
    "Logistic Regression":
        make_pipeline(
            StandardScaler(),
            LogisticRegression(
                max_iter=1000
            )
        ),

    "KNN":
        make_pipeline(
            StandardScaler(),
            KNeighborsClassifier(
                n_neighbors=5
            )
        ),

    "Decision Tree":
        DecisionTreeClassifier(
            max_depth=3,
            random_state=42
        )
}
```

这里再次体现：

```text
字典
↓
模型名称 → 模型对象
```

---

# 二十九、统一训练模型

创建：

```python
model_names = []
accuracies = []
```

然后：

```python
for name, model in models.items():

    model.fit(
        X_train,
        y_train
    )

    y_pred = model.predict(
        X_test
    )

    accuracy = accuracy_score(
        y_test,
        y_pred
    )

    model_names.append(
        name
    )

    accuracies.append(
        accuracy
    )

    print(
        f"{name}: "
        f"{accuracy:.4f}"
    )
```

---

# 三十、保存比较结果

使用 Pandas：

```python
import pandas as pd
```

创建：

```python
comparison = pd.DataFrame(
    {
        "Model": model_names,
        "Accuracy": accuracies
    }
)
```

输出：

```python
print(comparison)
```

---

# 三十一、按Accuracy排序

```python
comparison = (
    comparison.sort_values(
        by="Accuracy",
        ascending=False
    )
)
```

输出：

```python
print(comparison)
```

这正好把 Lab14 的 Pandas 知识重新使用起来。

---

# 三十二、绘制模型比较图

导入：

```python
import matplotlib.pyplot as plt
```

绘制：

```python
plt.figure()

plt.bar(
    comparison["Model"],
    comparison["Accuracy"]
)

plt.xlabel("Model")
plt.ylabel("Accuracy")
plt.title(
    "Classifier Comparison"
)

plt.ylim(
    0,
    1
)

plt.xticks(
    rotation=20
)

plt.tight_layout()
plt.show()
```

---

# 三十三、修改模型参数

尝试分别使用：

```python
KNeighborsClassifier(
    n_neighbors=1
)
```

```python
KNeighborsClassifier(
    n_neighbors=3
)
```

```python
KNeighborsClassifier(
    n_neighbors=5
)
```

```python
KNeighborsClassifier(
    n_neighbors=9
)
```

记录结果。

---

## Decision Tree

尝试：

```python
DecisionTreeClassifier(
    max_depth=2,
    random_state=42
)
```

```python
DecisionTreeClassifier(
    max_depth=3,
    random_state=42
)
```

```python
DecisionTreeClassifier(
    max_depth=5,
    random_state=42
)
```

观察结果是否完全相同。

---

# 三十四、参数的基本理解

例如：

```text
n_neighbors
max_depth
```

都属于：

# 模型参数

改变这些参数可能改变模型训练后的表现。

本次实验重点只要求认识：

```text
模型
+
参数
+
训练
+
评价
```

之间的关系。

模型参数选择和更加系统的模型优化将在后续人工智能专业课程中进一步学习。

---

# 三十五、模型比较的注意事项

本次实验中的模型比较主要用于理解：

```text
多个模型
如何使用统一接口训练和评价
```

不要仅根据一次测试划分就简单得出：

```text
“某模型永远比其他模型好”
```

模型表现还可能受到：

```text
数据集
训练样本
测试划分
模型参数
数据预处理
```

等因素影响。

---

# 三十六、任务4：完整的鸢尾花智能分类应用

## 1. 任务背景

前面已经分别完成：

```text
读取数据
数据划分
模型训练
模型预测
模型评价
模型比较
```

本任务进一步将这些内容组织成一个可以实际接收新样本的：

# Iris智能分类程序

程序最终实现：

```text
训练模型
   ↓
评价模型
   ↓
用户输入一个新样本
   ↓
模型进行预测
   ↓
输出预测类别
   ↓
输出类别概率
```

---

## 2. 创建程序

创建：

```text
task04_iris_classifier.py
```

---

# 三十七、第一步：加载数据

```python
from sklearn.datasets import load_iris

iris = load_iris(
    as_frame=True
)

X = iris.data
y = iris.target
```

---

# 三十八、第二步：划分数据

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = (
    train_test_split(
        X,
        y,
        test_size=0.2,
        random_state=42,
        stratify=y
    )
)
```

---

# 三十九、第三步：建立模型

```python
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import make_pipeline

model = make_pipeline(
    StandardScaler(),
    LogisticRegression(
        max_iter=1000
    )
)
```

---

# 四十、第四步：训练

```python
model.fit(
    X_train,
    y_train
)
```

---

# 四十一、第五步：测试集预测

```python
y_pred = model.predict(
    X_test
)
```

---

# 四十二、第六步：模型评价

```python
from sklearn.metrics import accuracy_score

accuracy = accuracy_score(
    y_test,
    y_pred
)

print()
print("=" * 50)
print("Iris分类模型")
print("=" * 50)

print(
    f"测试集Accuracy："
    f"{accuracy:.4f}"
)
```

---

# 四十三、第七步：绘制混淆矩阵

导入：

```python
from sklearn.metrics import ConfusionMatrixDisplay
import matplotlib.pyplot as plt
```

绘制：

```python
ConfusionMatrixDisplay.from_predictions(
    y_test,
    y_pred,
    display_labels=
        iris.target_names
)

plt.title(
    "Iris Classification Confusion Matrix"
)

plt.tight_layout()
plt.show()
```

---

# 四十四、第八步：输入新样本

提示用户输入：

```text
Sepal Length
Sepal Width
Petal Length
Petal Width
```

可以设计一个输入函数：

```python
def input_positive_float(
    prompt
):

    while True:

        try:

            value = float(
                input(prompt)
            )

            if value > 0:
                return value

            print(
                "请输入大于0的数值。"
            )

        except ValueError:

            print(
                "输入格式错误，"
                "请输入有效数字。"
            )
```

---

# 四十五、读取四个特征

```python
sepal_length = input_positive_float(
    "请输入Sepal Length："
)

sepal_width = input_positive_float(
    "请输入Sepal Width："
)

petal_length = input_positive_float(
    "请输入Petal Length："
)

petal_width = input_positive_float(
    "请输入Petal Width："
)
```

---

# 四十六、构造新样本

使用 Pandas：

```python
import pandas as pd
```

创建：

```python
new_sample = pd.DataFrame(
    [
        [
            sepal_length,
            sepal_width,
            petal_length,
            petal_width
        ]
    ],
    columns=iris.feature_names
)
```

这一步再次体现：

```text
一个样本
×
4个特征
```

---

# 四十七、进行预测

```python
prediction = model.predict(
    new_sample
)[0]
```

类别名称：

```python
predicted_class = (
    iris.target_names[
        prediction
    ]
)
```

输出：

```python
print()
print(
    f"预测类别："
    f"{predicted_class}"
)
```

---

# 四十八、预测概率

进一步：

```python
probabilities = (
    model.predict_proba(
        new_sample
    )[0]
)
```

输出：

```python
print()
print("类别预测概率：")

for class_name, probability in zip(
    iris.target_names,
    probabilities
):

    print(
        f"{class_name}: "
        f"{probability:.4f}"
    )
```

---

# 四十九、参考运行结构

最终程序可以形成：

```text
==================================================
                 Iris智能分类器
==================================================

模型测试Accuracy：0.xxxx

请输入Sepal Length：5.1
请输入Sepal Width：3.5
请输入Petal Length：1.4
请输入Petal Width：0.2

---------------- 预测结果 ----------------

预测类别：setosa

类别预测概率：

setosa：0.xxxx
versicolor：0.xxxx
virginica：0.xxxx

==================================================
```

具体概率和测试结果以实际程序运行结果为准。

---

# 五十、完整机器学习程序流程

完成 Task04 后，应能够理解：

```text
数据集
   ↓
X / y
   ↓
train_test_split
   ↓
X_train / X_test
y_train / y_test
   ↓
StandardScaler
   ↓
模型
   ↓
fit
   ↓
predict
   ↓
Accuracy
   ↓
Confusion Matrix
   ↓
新样本
   ↓
predict
   ↓
实际分类结果
```

---

# 五十一、任务4分析

回答：

1. 为什么模型训练使用 `X_train` 和 `y_train`？
2. 为什么评价使用 `X_test` 和 `y_test`？
3. `fit()` 完成什么工作？
4. `predict()` 完成什么工作？
5. 为什么新样本必须具有与训练数据相同的特征结构？
6. 模型输出的预测结果是否一定正确？
7. Accuracy 很高是否意味着模型在所有情况下都一定可靠？

---

# 五十二、拓展任务：交叉验证与模型稳定性

创建：

```text
extension_cross_validation.py
```

前面的模型评价主要使用：

```text
一次训练集 / 测试集划分
```

拓展任务进一步了解：

# Cross Validation

即让模型在不同数据划分上进行多次训练和评价。

---

## 1. 导入

```python
from sklearn.model_selection import cross_val_score
```

---

## 2. 创建模型

例如：

```python
model = make_pipeline(
    StandardScaler(),
    LogisticRegression(
        max_iter=1000
    )
)
```

---

## 3. 进行5折交叉验证

```python
scores = cross_val_score(
    model,
    X,
    y,
    cv=5,
    scoring="accuracy"
)
```

输出：

```python
print(scores)
```

---

## 4. 计算平均结果

使用 NumPy：

```python
import numpy as np

print(
    f"平均Accuracy："
    f"{np.mean(scores):.4f}"
)

print(
    f"Accuracy标准差："
    f"{np.std(scores):.4f}"
)
```

这里再次使用 Lab13 学习的：

```text
mean
std
```

---

# 五十三、比较三个模型的交叉验证结果

创建：

```python
models = {
    "Logistic Regression":
        make_pipeline(
            StandardScaler(),
            LogisticRegression(
                max_iter=1000
            )
        ),

    "KNN":
        make_pipeline(
            StandardScaler(),
            KNeighborsClassifier(
                n_neighbors=5
            )
        ),

    "Decision Tree":
        DecisionTreeClassifier(
            max_depth=3,
            random_state=42
        )
}
```

循环：

```python
for name, model in models.items():

    scores = cross_val_score(
        model,
        X,
        y,
        cv=5,
        scoring="accuracy"
    )

    print()
    print(name)

    print(
        f"各折Accuracy："
        f"{scores}"
    )

    print(
        f"平均Accuracy："
        f"{np.mean(scores):.4f}"
    )

    print(
        f"标准差："
        f"{np.std(scores):.4f}"
    )
```

---

# 五十四、理解平均值与标准差

可以初步理解：

```text
平均Accuracy
↓
模型整体表现

Accuracy标准差
↓
不同数据划分下结果波动情况
```

如果：

```text
平均结果较高
+
标准差较小
```

通常说明在本次实验设置下模型表现相对稳定。

这里暂时不深入讨论交叉验证理论。

---

# 五十五、拓展分析

回答：

1. 单次训练/测试划分与5折交叉验证有什么不同？
2. 三种模型的平均 Accuracy 是否相同？
3. 哪种模型的结果波动更大？
4. 单次测试结果最高的模型，在交叉验证中是否仍然最好？
5. 为什么评价机器学习模型不能只看一次实验结果？

---

# 五十六、本次实训提交内容

本次实训至少完成：

```text
lab15-machine-learning/
├── task01_dataset_split.py
├── task02_first_classifier.py
├── task03_model_comparison.py
└── task04_iris_classifier.py
```

拓展任务可以创建：

```text
extension_cross_validation.py
```

如果保存混淆矩阵或模型比较图，可以自行创建：

```text
outputs/
```

例如：

```text
outputs/
├── confusion_matrix.png
└── model_comparison.png
```

本次实验直接使用 Scikit-learn 内置 Iris 数据集，因此不要求另外提供 `data/` 文件夹。

---

# 五十七、实训检查

完成本次实训后，应能够：

* [ ] 正确导入 Scikit-learn；
* [ ] 使用 `load_iris()` 获取内置数据集；
* [ ] 理解样本、特征和标签；
* [ ] 理解 `X` 与 `y`；
* [ ] 理解二维数据的“样本 × 特征”形式；
* [ ] 使用 `train_test_split()` 划分数据；
* [ ] 理解训练集和测试集的基本作用；
* [ ] 理解 `test_size`；
* [ ] 理解 `random_state` 的基本作用；
* [ ] 使用 `StandardScaler` 进行标准化；
* [ ] 使用 Pipeline 组织预处理与分类模型；
* [ ] 创建机器学习分类器；
* [ ] 使用 `fit()` 训练模型；
* [ ] 使用 `predict()` 完成预测；
* [ ] 使用 Accuracy 评价分类结果；
* [ ] 查看真实标签和预测标签；
* [ ] 查找错误分类样本；
* [ ] 生成混淆矩阵；
* [ ] 查看分类报告；
* [ ] 使用统一程序训练多个模型；
* [ ] 使用 Pandas 整理模型比较结果；
* [ ] 使用 Matplotlib 显示模型比较结果；
* [ ] 修改模型基本参数并观察结果；
* [ ] 使用训练后的模型预测新样本；
* [ ] 查看分类预测概率；
* [ ] 初步理解交叉验证；
* [ ] 完成一个基本的机器学习分类应用。

---

# 五十八、本次实训知识路线

```text
Pandas / NumPy数据
        ↓
    数据集
        ↓
   特征 X
        +
   标签 y
        ↓
train_test_split
        ↓
训练集 / 测试集
        ↓
StandardScaler
        ↓
机器学习模型
        ↓
      fit()
        ↓
    predict()
        ↓
Accuracy / Classification Report
        ↓
Confusion Matrix
        ↓
模型比较
        ↓
新样本预测
        ↓
基础机器学习应用
```

---

# 五十九、Lab13～Lab15的完整关系

第三阶段已经形成完整的数据与机器学习路线：

```text
Lab13
NumPy
   ↓
数值数组与向量化计算
   ↓
样本 × 特征

Lab14
Pandas + Matplotlib
   ↓
数据读取、清洗、统计与可视化
   ↓
理解数据

Lab15
Scikit-learn
   ↓
训练、预测和评价
   ↓
利用数据建立模型
```

可以概括为：

```text
Lab13
“怎样计算数据？”

      ↓

Lab14
“怎样理解和整理数据？”

      ↓

Lab15
“怎样利用数据训练模型？”
```

---

# 六十、第三阶段总结

完成 Lab13～Lab15 后，应已经初步具备：

```text
NumPy
+
Pandas
+
Matplotlib
+
Scikit-learn
```

组成的数据与机器学习基础工具链。

完整流程可以概括为：

```text
原始数据
   ↓
NumPy / Pandas
   ↓
数据处理
   ↓
数据检查
   ↓
数据分析
   ↓
数据可视化
   ↓
特征 X
   ↓
标签 y
   ↓
模型训练
   ↓
模型预测
   ↓
模型评价
```

---

# 六十一、下一阶段

完成 Lab15 后，将进入本课程 Labs 的最后一个实验：

# Lab 16：AI Mini Application

Lab16 将不再以：

```text
“学习一个新的Python语法或库”
```

为主要目的。

而是要求综合运用：

```text
Python基础
+
条件与循环
+
数据结构
+
函数
+
文件
+
NumPy
+
Pandas
+
Matplotlib
+
Scikit-learn
```

完成一个相对完整的小型 AI 应用。

程序流程将进一步发展为：

```text
问题定义
   ↓
数据加载
   ↓
数据探索
   ↓
数据预处理
   ↓
训练集 / 测试集
   ↓
模型训练
   ↓
模型评价
   ↓
结果可视化
   ↓
用户输入
   ↓
模型预测
   ↓
完整AI应用
```

Lab16 将作为：

```text
Labs阶段
      ↓
综合项目Projects阶段
```

之间的最后一次过渡实训。
