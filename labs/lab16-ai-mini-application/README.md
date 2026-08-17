# Lab 16：AI Mini Application——手写数字智能识别与分析系统

## 一、实训定位

Lab 16 是本课程 Labs 阶段的最后一次综合实训。

前面的 Lab 已经分别学习了：

```text
Python基础语法
      ↓
条件与循环
      ↓
字符串与数据结构
      ↓
函数与模块
      ↓
文件与异常
      ↓
面向对象
      ↓
NumPy
      ↓
Pandas
      ↓
Matplotlib
      ↓
Scikit-learn
```

本次实验不再重点学习新的语法或工具，而是解决一个更重要的问题：

> **怎样把已经学习过的 Python 知识组合起来，开发一个相对完整的小型 AI 应用？**

本次实训最终完成：

# 手写数字智能识别与分析系统

系统基本流程为：

```text
加载数据
   ↓
理解数据
   ↓
数据可视化
   ↓
训练集 / 测试集划分
   ↓
数据预处理
   ↓
模型训练
   ↓
模型评价
   ↓
混淆矩阵
   ↓
样本预测
   ↓
预测结果展示
   ↓
结果保存
   ↓
完整AI应用
```

---

# 二、实训目标

完成本次实训后，应能够综合运用前面所学知识完成：

1. AI 数据集加载与基本分析；
2. NumPy 多维数据处理；
3. Pandas 表格数据组织；
4. Matplotlib 图像与结果可视化；
5. Scikit-learn 模型训练与预测；
6. 模型性能评价；
7. 函数化与模块化程序组织；
8. 文件结果保存；
9. 异常处理与用户输入检查；
10. 菜单式 AI 应用程序设计。

本次实训采用：

**1 个综合项目 + 5 个开发阶段 + 1 个提高任务。**

---

# 三、推荐项目目录

本次实验不再建议只编写一个很长的 `.py` 文件。

推荐采用：

```text
lab16-ai-mini-application/
│
├── main.py
├── data_utils.py
├── model_utils.py
├── visualization.py
│
└── outputs/
```

其中：

| 文件                 | 主要职责           |
| ------------------ | -------------- |
| `main.py`          | 程序入口、菜单和整体流程   |
| `data_utils.py`    | 数据加载、数据拆分和结果整理 |
| `model_utils.py`   | 模型建立、训练、预测和评价  |
| `visualization.py` | 样本图像和评价结果可视化   |
| `outputs/`         | 保存预测结果和生成的图像   |

如果暂时无法完成多文件版本，可以先在一个 Python 文件中实现完整功能，再进行模块化拆分。

---

# 四、实验准备

本次实验主要使用：

```text
NumPy
Pandas
Matplotlib
Scikit-learn
```

首先测试：

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import sklearn

print(sklearn.__version__)
```

---

# 五、综合应用开发路线

整个系统分为五个阶段完成：

```text
阶段1
认识手写数字数据
      ↓
阶段2
可视化与数值分析
      ↓
阶段3
训练并评价分类模型
      ↓
阶段4
实现手写数字预测
      ↓
阶段5
整合为完整AI应用
```

不建议一开始直接编写完整系统。

应按照阶段逐步开发和测试。

---

# 六、阶段1：认识手写数字数据

## 1. 加载数据

使用：

```python
from sklearn.datasets import load_digits

digits = load_digits()
```

获取：

```python
X = digits.data
y = digits.target
images = digits.images
```

分别输出：

```python
print(X.shape)
print(y.shape)
print(images.shape)
```

根据实际程序输出分析：

* 有多少个样本；
* 每个样本有多少个数值特征；
* 单幅数字图像的尺寸；
* 一共有多少种分类标签。

---

## 2. 理解三种数据表示

重点比较：

```python
digits.data
```

和：

```python
digits.images
```

之间的关系。

可以理解为：

```text
一幅数字图像

8 × 8
二维图像

      ↓ 展平

64个数值
一维特征向量
```

即：

```text
图像表示
      ↓
特征表示
      ↓
机器学习模型输入
```

---

## 3. 查看单个样本

例如：

```python
sample_index = 0

print(
    X[sample_index]
)

print(
    y[sample_index]
)

print(
    images[sample_index]
)
```

观察：

```text
特征
标签
图像
```

三者之间的对应关系。

---

# 七、阶段2：数据探索与可视化

## 1. 显示一幅手写数字

创建：

```text
visualization.py
```

设计函数：

```python
def show_digit(image, label):
    ...
```

核心可以使用：

```python
plt.figure()

plt.imshow(
    image,
    cmap="gray"
)

plt.title(
    f"Digit: {label}"
)

plt.axis("off")
plt.tight_layout()
plt.show()
```

---

## 2. 显示多幅数字

选择若干样本进行显示。

建议至少显示：

```text
10幅
```

不同手写数字样本。

观察：

* 同一个数字的书写是否完全相同；
* 不同数字之间是否存在形态相似情况；
* 为什么手写数字分类不是简单的规则判断问题。

---

## 3. 分析类别分布

使用 Pandas：

```python
import pandas as pd

label_counts = (
    pd.Series(y)
      .value_counts()
      .sort_index()
)

print(label_counts)
```

绘制：

```text
不同数字类别样本数量柱状图
```

要求：

```text
横轴：Digit
纵轴：Number of Samples
```

---

## 4. 数据基本统计

使用 NumPy 查看：

```python
print(np.min(X))
print(np.max(X))
print(np.mean(X))
print(np.std(X))
```

观察像素特征的数据范围和整体分布。

---

# 八、阶段3：训练手写数字分类模型

## 1. 划分数据

在：

```text
data_utils.py
```

中设计：

```python
def split_dataset(X, y):
    ...
```

可以使用：

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

输出：

```text
训练样本数量
测试样本数量
特征数量
```

---

# 九、建立模型

在：

```text
model_utils.py
```

设计：

```python
def build_model():
    ...
```

推荐继续使用学生在 Lab15 已经接触过的：

```text
StandardScaler
+
LogisticRegression
```

形成 Pipeline。

例如：

```python
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import make_pipeline
```

系统不要求学习新的分类算法。

重点是：

> **把已经掌握的机器学习方法放入一个完整应用。**

---

# 十、训练模型

设计：

```python
def train_model(
    model,
    X_train,
    y_train
):
    ...
```

核心流程：

```python
model.fit(
    X_train,
    y_train
)
```

---

# 十一、模型预测

设计：

```python
def predict(
    model,
    X
):
    ...
```

完成：

```python
y_pred = model.predict(
    X_test
)
```

---

# 十二、模型评价

至少计算：

```text
Accuracy
Classification Report
Confusion Matrix
```

可以设计：

```python
def evaluate_model(
    model,
    X_test,
    y_test
):
    ...
```

至少输出：

```text
========================================
         手写数字分类模型评价
========================================

测试样本数量：XXXX
Accuracy：XXXX

========================================
```

具体结果以实际程序运行结果为准。

---

# 十三、绘制混淆矩阵

在：

```text
visualization.py
```

设计：

```python
def show_confusion_matrix(
    y_test,
    y_pred
):
    ...
```

可以使用：

```python
from sklearn.metrics import ConfusionMatrixDisplay
```

绘制数字：

```text
0～9
```

之间的分类情况。

保存：

```text
outputs/confusion_matrix.png
```

---

# 十四、分析错误预测

仅仅知道 Accuracy 还不够。

找出：

```text
真实标签
≠
预测标签
```

的样本。

例如：

```python
error_indices = np.where(
    y_test != y_pred
)[0]
```

统计：

```text
错误预测数量
错误率
```

进一步显示若干错误预测样本。

图像标题可以设计为：

```text
True: 8
Predicted: 3
```

---

# 十五、阶段4：实现单个样本智能预测

## 1. 任务目标

让系统不再只是：

```text
训练
+
统计Accuracy
```

而能够真正完成：

```text
输入一个样本
   ↓
模型预测
   ↓
显示预测结果
```

---

## 2. 从测试集中选择样本

允许用户输入：

```text
请输入测试样本编号：
```

例如：

```text
15
```

系统找到对应样本：

```python
sample = X_test[
    sample_index
]
```

---

## 3. 检查输入范围

如果用户输入：

```text
-1
```

或者超过测试集范围的编号，程序应该提示：

```text
样本编号无效，请重新输入。
```

还需要处理：

```text
abc
```

等非整数输入。

这里需要重新使用：

```text
try
except
```

---

# 十六、执行预测

由于模型需要二维输入，可以将单个样本转换为：

```python
sample_for_prediction = (
    sample.reshape(1, -1)
)
```

然后：

```python
prediction = model.predict(
    sample_for_prediction
)[0]
```

---

# 十七、显示预测结果

输出：

```text
========================================
          手写数字预测结果
========================================

样本编号：15

真实数字：8
预测数字：8

预测结果：正确

========================================
```

如果预测错误：

```text
真实数字：8
预测数字：3

预测结果：错误
```

---

# 十八、显示对应数字图像

需要注意：

模型输入使用：

```text
64维特征
```

但显示时应使用对应的：

```text
8 × 8
```

数字图像。

因此系统需要保持：

```text
X
images
y
```

之间的样本对应关系。

---

# 十九、预测概率

如果最终使用的模型支持：

```python
predict_proba()
```

可以进一步输出：

```text
数字0：0.xxxx
数字1：0.xxxx
...
数字9：0.xxxx
```

并找出最大概率对应数字。

这一功能可以作为提高内容，不作为最低完成要求。

---

# 二十、阶段5：整合为完整AI应用

现在将前面的功能整合到：

```text
main.py
```

最终程序启动时：

```text
加载数据
   ↓
划分训练/测试集
   ↓
建立模型
   ↓
训练模型
   ↓
进入系统菜单
```

---

# 二十一、系统菜单

建议设计：

```text
==================================================
        手写数字智能识别与分析系统
==================================================

1. 查看数据集信息
2. 查看数字样本
3. 查看模型评价结果
4. 查看混淆矩阵
5. 预测指定测试样本
6. 查看错误预测样本
7. 导出测试集预测结果
0. 退出系统

==================================================
```

---

# 二十二、功能1：查看数据集信息

输出：

```text
数据集名称
样本数量
特征数量
类别数量
训练样本数量
测试样本数量
```

---

# 二十三、功能2：查看数字样本

用户输入样本编号。

系统显示：

```text
图像
+
真实标签
```

需要检查输入是否合法。

---

# 二十四、功能3：查看模型评价

输出：

```text
Accuracy
Classification Report
测试样本数量
错误预测数量
```

---

# 二十五、功能4：查看混淆矩阵

调用：

```python
show_confusion_matrix(...)
```

显示并保存：

```text
outputs/confusion_matrix.png
```

---

# 二十六、功能5：预测指定测试样本

流程：

```text
输入样本编号
   ↓
检查是否合法
   ↓
获取测试样本
   ↓
模型预测
   ↓
显示数字图像
   ↓
显示真实标签
   ↓
显示预测标签
```

---

# 二十七、功能6：查看错误预测样本

显示若干模型预测错误的数字。

至少输出：

```text
样本编号
真实标签
预测标签
```

并可选择显示对应图像。

---

# 二十八、功能7：导出预测结果

将测试集预测结果组织为 Pandas DataFrame：

```python
results = pd.DataFrame(
    {
        "true_label": y_test,
        "predicted_label": y_pred
    }
)
```

增加：

```python
results["correct"] = (
    results["true_label"]
    ==
    results["predicted_label"]
)
```

保存：

```python
results.to_csv(
    "outputs/prediction_results.csv",
    index=False
)
```

最终形成：

```text
outputs/
├── confusion_matrix.png
└── prediction_results.csv
```

---

# 二十九、main.py的基本结构

主程序不应该包含所有具体实现代码。

建议保持类似：

```python
def show_menu():
    ...


def main():

    # 1. 加载数据

    # 2. 数据划分

    # 3. 创建模型

    # 4. 训练模型

    # 5. 得到预测结果

    while True:

        show_menu()

        choice = input(
            "请选择功能："
        )

        if choice == "1":
            pass

        elif choice == "2":
            pass

        elif choice == "3":
            pass

        elif choice == "4":
            pass

        elif choice == "5":
            pass

        elif choice == "6":
            pass

        elif choice == "7":
            pass

        elif choice == "0":

            print(
                "系统已退出。"
            )

            break

        else:

            print(
                "无效选择，请重新输入。"
            )


if __name__ == "__main__":
    main()
```

各项具体功能由其他函数或模块完成。

---

# 三十、推荐函数设计

可以至少设计：

```text
data_utils.py

load_data()
split_dataset()
create_prediction_table()
```

---

```text
model_utils.py

build_model()
train_model()
evaluate_model()
predict_sample()
```

---

```text
visualization.py

show_digit()
show_digit_samples()
show_confusion_matrix()
show_error_samples()
```

---

```text
main.py

show_menu()
main()
```

形成：

```text
main.py
   ↓
整体流程

data_utils.py
   ↓
数据

model_utils.py
   ↓
模型

visualization.py
   ↓
显示

outputs/
   ↓
结果
```

---

# 三十一、必须体现的课程知识

Lab16 不只是机器学习实验。

最终程序至少应体现前面课程中的以下知识。

## Python基础

```text
变量
输入输出
条件判断
循环
```

---

## 数据结构

```text
列表
字典
```

---

## 函数与模块

```text
def
参数
return
import
```

---

## 文件处理

```text
CSV结果保存
```

---

## 异常处理

```text
try-except
```

---

## NumPy

```text
ndarray
shape
reshape
布尔索引
```

---

## Pandas

```text
DataFrame
to_csv()
```

---

## Matplotlib

```text
数字图像显示
混淆矩阵
```

---

## Scikit-learn

```text
数据集
train_test_split
模型
fit
predict
评价
```

因此，本 Lab 真正要解决的是：

```text
多个知识点
      ↓
如何协同工作
      ↓
完整应用
```

---

# 三十二、最低完成要求

完成基本版本至少需要实现：

* [ ] 能够加载手写数字数据集；
* [ ] 能够输出数据集基本信息；
* [ ] 能够显示数字图像；
* [ ] 能够划分训练集和测试集；
* [ ] 能够建立分类模型；
* [ ] 能够完成模型训练；
* [ ] 能够完成测试集预测；
* [ ] 能够计算 Accuracy；
* [ ] 能够显示混淆矩阵；
* [ ] 能够预测指定测试样本；
* [ ] 能够显示真实标签和预测标签；
* [ ] 能够找出部分错误预测样本；
* [ ] 能够导出测试集预测结果；
* [ ] 程序具有菜单式交互界面；
* [ ] 对非法用户输入进行基本异常处理；
* [ ] 使用函数组织程序。

---

# 三十三、规范完成要求

在最低要求基础上，还应：

* [ ] 将程序拆分为多个 `.py` 文件；
* [ ] 函数命名清晰；
* [ ] 每个模块职责明确；
* [ ] 避免大量重复代码；
* [ ] 对重要函数添加简单注释；
* [ ] 输出结果格式清晰；
* [ ] 自动创建或正确使用 `outputs/`；
* [ ] 将混淆矩阵保存为图片；
* [ ] 将预测结果保存为 CSV；
* [ ] README 或实验记录中说明程序结构。

---

# 三十四、提高任务：模型比较模式

完成基本系统后，可以进一步加入：

```text
8. 模型比较
```

比较：

```text
Logistic Regression
KNN
Decision Tree
```

对每个模型计算：

```text
Accuracy
错误样本数量
```

使用 Pandas 保存：

```text
Model
Accuracy
Error Count
```

例如：

```text
========================================
             模型比较结果
========================================

Model                   Accuracy
----------------------------------------
Logistic Regression     ....
KNN                     ....
Decision Tree           ....

========================================
```

具体结果必须由程序实际运行产生。

---

# 三十五、提高任务：模型比较可视化

利用 Matplotlib 绘制：

```text
不同模型Accuracy柱状图
```

保存：

```text
outputs/model_comparison.png
```

思考：

> 在同一数据集上的一次实验结果，是否足以证明某一种模型在所有任务中都最好？

---

# 三十六、不要直接输入真实手写数字矩阵

本 Lab 的基础版本不要求学生手工输入：

```text
64个像素值
```

来构造新数字。

这是因为：

```text
64维手工输入
```

并不适合作为教学应用交互方式。

基础版本采用：

```text
从测试集中选择样本
      ↓
模拟未知样本
      ↓
模型预测
```

即可完成完整的分类流程。

真正的：

```text
鼠标手写数字
图片上传
图像预处理
```

可以留到课程 `projects/` 阶段作为更高级的综合项目。

---

# 三十七、项目测试要求

最终系统至少进行以下测试。

## 测试1：正常启动

检查：

```text
数据加载
模型训练
菜单显示
```

是否正常。

---

## 测试2：数据查看

能够正确显示：

```text
数据规模
类别
特征
```

---

## 测试3：图像显示

至少查看：

```text
数字0
数字1
数字5
数字8
```

等不同数字样本。

---

## 测试4：模型预测

至少随机检查：

```text
10个测试样本
```

记录：

```text
真实标签
预测标签
```

---

## 测试5：错误预测

找出模型预测错误的样本，并观察对应图像。

---

## 测试6：非法输入

分别输入：

```text
abc
```

```text
-1
```

以及超出样本范围的编号。

程序不能直接崩溃。

---

## 测试7：结果保存

检查：

```text
outputs/prediction_results.csv
```

和：

```text
outputs/confusion_matrix.png
```

是否正常生成。

---

# 三十八、本次实训提交内容

本次实训最终建议提交：

```text
lab16-ai-mini-application/
│
├── main.py
├── data_utils.py
├── model_utils.py
├── visualization.py
│
└── outputs/
    ├── prediction_results.csv
    └── confusion_matrix.png
```

如果完成提高任务，可以增加：

```text
outputs/model_comparison.png
```

以及相关代码。

---

# 三十九、实验总结要求

完成程序后，提交简短实验总结，回答：

1. 整个 AI 应用包含哪些主要模块？
2. NumPy 在程序中承担什么作用？
3. Pandas 在程序中承担什么作用？
4. Matplotlib 在程序中承担什么作用？
5. Scikit-learn 在程序中承担什么作用？
6. 为什么程序要拆分为多个函数或模块？
7. 模型为什么会出现错误预测？
8. 哪些数字类别更容易产生混淆？
9. 如果继续完善该应用，可以增加哪些功能？
10. 从 Lab01 到 Lab16，自己的程序设计方式发生了什么变化？

---

# 四十、Lab16知识路线

```text
数据集
  ↓
NumPy数组
  ↓
数据探索
  ↓
图像可视化
  ↓
训练 / 测试划分
  ↓
机器学习模型
  ↓
fit()
  ↓
predict()
  ↓
模型评价
  ↓
混淆矩阵
  ↓
错误样本分析
  ↓
用户交互
  ↓
结果保存
  ↓
模块化组织
  ↓
AI Mini Application
```

---

# 四十一、16个Lab整体学习路线

完成 Lab16 后，整个 Labs 阶段形成完整路线：

```text
Lab01
环境与GitHub
   ↓
Lab02
输入输出与数据类型
   ↓
Lab03
运算与表达式
   ↓
Lab04
条件分支
   ↓
Lab05
循环
   ↓
Lab06
控制结构综合
   ↓
Lab07
字符串 / 列表 / 元组
   ↓
Lab08
字典 / 集合
   ↓
Lab09
数据结构综合
   ↓
Lab10
函数与模块化
   ↓
Lab11
文件与异常
   ↓
Lab12
面向对象
   ↓
Lab13
NumPy
   ↓
Lab14
Pandas + Matplotlib
   ↓
Lab15
Scikit-learn
   ↓
Lab16
AI综合应用
```

整体能力演进可以概括为：

```text
会运行Python
      ↓
会写简单程序
      ↓
会使用控制结构
      ↓
会组织数据
      ↓
会设计较完整程序
      ↓
会使用函数和对象组织代码
      ↓
会读取和保存数据
      ↓
会处理与分析数据
      ↓
会训练机器学习模型
      ↓
会开发一个小型AI应用
```

---

# 四十二、从Labs进入Projects

Lab16 并不是课程学习的终点。

它承担的是：

```text
Labs
基础和专项训练
       ↓
Lab16
综合能力整合
       ↓
Projects
开放式综合项目
```

Lab16 中：

```text
任务
数据
模型
功能
```

仍然由教师进行了较明确的规定。

进入 `projects/` 后，学生将进一步面对：

```text
更加开放的问题
+
更大的程序规模
+
更多自主设计
+
更多功能选择
```

因此 Lab16 是从：

```text
“按照任务完成程序”
```

向：

```text
“根据需求设计项目”
```

过渡的重要一步。

---

# 四十三、课程Labs阶段完成

完成本次实训后，学生已经完成《高级语言程序设计实训》课程的全部 16 个 Lab。

接下来进入：

# Projects 综合项目阶段

在综合项目中，需要进一步综合：

```text
问题分析
+
数据处理
+
程序设计
+
AI模型
+
结果展示
+
项目文档
+
Git / GitHub
```

完成一个相对独立的 Python / AI 综合实践项目。
