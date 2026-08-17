# 实训提交指南（Submission Guide）

本文件说明《高级语言程序设计实训》课程中 Lab 实验的仓库创建、代码编写、Git 提交、GitHub 上传和最终作业提交规范。

请所有同学在开始第一次实训前完整阅读本说明。

---

# 1. 课程仓库说明

本课程使用 GitHub 进行实训代码发布、版本管理和过程记录。

教师课程仓库：

```text
AI-Python-Programming-2026
```

主要目录结构为：

```text
AI-Python-Programming-2026/
│
├── examples/
│   └── 课堂示例代码
│
├── labs/
│   └── Lab01～Lab16实训任务
│
├── projects/
│   └── 综合项目
│
├── SUBMISSION_GUIDE.md
│
├── GRADING_RUBRIC.md
│
└── README.md
```

其中：

```text
examples/
```

用于查看教师提供的课堂示例；

```text
labs/
```

用于完成日常实训任务；

```text
projects/
```

用于后续综合项目。

---

# 2. 重要原则

教师仓库主要用于：

```text
发布任务
提供示例
提供课程资源
```

学生不要直接修改教师仓库，也不要将自己的实验答案提交到教师公共仓库。

每名学生应建立自己的：

# Private GitHub Repository

用于保存整个学期的实训代码。

---

# 3. 第一次实训前：建立个人课程仓库

## 3.1 创建个人仓库

进入教师提供的课程模板仓库。

点击：

```text
Use this template
```

然后选择：

```text
Create a new repository
```

---

## 3.2 仓库名称

个人课程仓库必须按照以下格式命名：

```text
AI-Python-Programming-2026-学号
```

例如：

```text
AI-Python-Programming-2026-2026123456
```

不得使用：

```text
python
python-homework
my-code
lab
test
```

等无法识别学生身份的名称。

---

## 3.3 仓库可见性

个人作业仓库必须设置为：

```text
Private
```

原因是：

```text
避免其他同学直接查看和复制实验代码
```

---

# 4. 邀请教师进入个人仓库

个人仓库创建后，进入：

```text
Settings
↓
Collaborators
```

添加课程教师 GitHub 账号：

```text
[dalas2mimi-collab]
```

教师需要具有访问学生仓库的权限，以便进行：

```text
作业检查
代码运行
版本检查
评分
```

整个学期只需要邀请一次。

---

# 5. 将个人仓库下载到本地

推荐使用 Git 将个人仓库克隆到本地。

例如：

```bash
git clone 你的个人仓库地址
```

进入课程目录：

```bash
cd AI-Python-Programming-2026-学号
```

以后所有 Lab 均在该目录中完成。

---

# 6. 本地目录要求

学生应保持教师提供的目录结构。

例如：

```text
AI-Python-Programming-2026-2026123456/
│
├── examples/
│
├── labs/
│   ├── lab01-environment-git/
│   ├── lab02-input-output/
│   ├── lab03-expressions/
│   ├── ...
│   └── lab16-ai-mini-application/
│
├── projects/
│
├── SUBMISSION_GUIDE.md
├── GRADING_RUBRIC.md
└── README.md
```

不要随意修改教师规定的 Lab 文件夹名称。

---

# 7. 每次Lab的基本完成流程

每次实验建议按照以下顺序完成：

```text
阅读README
   ↓
理解任务要求
   ↓
编写程序
   ↓
运行程序
   ↓
测试不同输入
   ↓
修改错误
   ↓
完成REPORT.md
   ↓
git add
   ↓
git commit
   ↓
git push
   ↓
提交最终Commit链接
```

---

# 8. 阅读Lab任务

例如进行 Lab05：

进入：

```text
labs/lab05-loops/
```

首先阅读：

```text
README.md
```

README 中包含：

```text
实训目的
任务要求
文件名称
知识点
参考代码片段
测试要求
拓展任务
```

请先理解任务，再编写代码。

---

# 9. 学生程序文件

例如 Lab08 要求：

```text
lab08-dict-set/
├── task01_dictionary_basics.py
├── task02_dictionary_processing.py
├── task03_set_operations.py
└── task04_ai_experiment_manager.py
```

学生应按照 README 中规定的文件名创建程序。

不要使用：

```text
1.py
2.py
test.py
new.py
aaa.py
final.py
final2.py
```

等缺乏意义的文件名替代规定名称。

---

# 10. 每个Lab必须包含REPORT.md

除 Lab README 中另有说明外，每个 Lab 最终应增加：

```text
REPORT.md
```

例如：

```text
lab08-dict-set/
│
├── task01_dictionary_basics.py
├── task02_dictionary_processing.py
├── task03_set_operations.py
├── task04_ai_experiment_manager.py
└── REPORT.md
```

---

# 11. REPORT.md模板

建议使用以下格式：

```markdown
# Lab 08 实验记录

学号：2026123456

姓名：张三

## 1. 完成情况

- [x] Task 01
- [x] Task 02
- [x] Task 03
- [x] Task 04
- [ ] Extension

## 2. 自测结果

所有必做程序均能够正常运行。

测试了正常输入、边界输入以及部分异常输入。

## 3. 遇到的问题

在遍历嵌套字典时最初出现键访问错误，
检查数据结构后完成修改。

## 4. 本次实训收获

理解了列表、字典和集合在不同数据组织场景中的作用。

## 5. AI辅助说明

如使用了AI工具，请简要说明使用范围。

例如：

使用AI帮助解释了 `dict.items()` 的用法，
最终程序由本人理解、修改并完成测试。

如果未使用，可填写：

未使用。
```

不要求撰写长篇实验报告。

重点是记录：

```text
完成情况
自测情况
遇到的问题
学习收获
```

---

# 12. 为什么必须进行自测

程序：

```text
能够运行
```

并不代表：

```text
结果一定正确
```

例如一个成绩输入程序至少应测试：

```text
正常成绩
0
100
负数
超过100
非数字输入
```

一个菜单程序至少应测试：

```text
有效菜单项
无效菜单项
退出功能
重复操作
```

因此完成代码后必须主动测试不同情况。

---

# 13. Git提交基本流程

完成 Lab 后，首先检查：

```bash
git status
```

确认修改文件。

然后：

```bash
git add labs/labXX-目录名
```

例如：

```bash
git add labs/lab05-loops
```

---

# 14. 正式提交Commit Message

每个 Lab 的最终正式提交必须使用统一格式：

```text
Submit Lab XX
```

例如：

```bash
git commit -m "Submit Lab 05"
```

Lab16：

```bash
git commit -m "Submit Lab 16"
```

正式提交信息不要写成：

```text
finish
123
update
new
ok
homework
```

---

# 15. 上传到GitHub

完成 Commit 后：

```bash
git push origin main
```

然后进入 GitHub 个人仓库检查文件是否已经更新。

---

# 16. 推荐的日常Commit方式

实验过程中可以进行多次正常 Commit。

例如：

```text
Complete Lab 08 Task 01
Complete Lab 08 Task 02
Fix Lab 08 input validation
Update Lab 08 report
Submit Lab 08
```

这比：

```text
整个实验一次Commit
```

更能够体现真实的开发过程。

正式提交仍以最后的：

```text
Submit Lab XX
```

作为该 Lab 的最终版本。

---

# 17. 每次Lab最终提交什么

学生不需要上传 ZIP 压缩包。

原则上也不需要重复上传所有 `.py` 文件到其他系统。

每次 Lab 最终提交：

```text
本次Lab最终Commit链接
```

如课程教学平台要求填写仓库信息，则同时提供：

```text
个人GitHub仓库地址
+
本次Lab最终Commit地址
```

---

# 18. 如何获取Commit链接

进入个人 GitHub 仓库。

点击：

```text
Commits
```

找到：

```text
Submit Lab XX
```

进入该 Commit 页面。

复制浏览器中的 Commit 地址。

该地址代表：

> 本次实验正式提交的确定版本。

---

# 19. 推荐提交格式

在课程提交平台中填写：

```text
Lab：Lab08

姓名：张三

学号：2026123456

GitHub仓库：
[个人仓库地址]

最终Commit：
[Submit Lab 08对应的Commit地址]
```

---

# 20. 为什么提交Commit而不是只提交仓库主页

仓库内容会不断更新。

如果只提交：

```text
仓库主页
```

教师无法明确判断：

```text
截止时间时的正式版本
```

而 Commit 对应一个确定版本。

因此：

```text
Repository
=
整个学期的课程代码

Commit
=
某一次Lab的正式提交版本
```

---

# 21. 截止时间

每次 Lab 的具体截止时间由教师在课堂或教学平台公布。

例如：

```text
Lab08截止：
2026-XX-XX 23:59
```

请在截止时间之前完成：

```text
代码
+
REPORT.md
+
Commit
+
Push
+
教学平台提交Commit链接
```

其中任何一步未完成，都可能造成提交不完整。

---

# 22. 正式提交时间的认定

如课程使用教学平台收集作业：

> **以教学平台提交最终 Commit 链接的时间作为正式提交时间。**

GitHub Commit 主要用于确定：

```text
提交的是哪个代码版本
```

如果教师另有说明，以当次课程通知为准。

---

# 23. 截止前允许修改

在截止时间之前，如发现程序错误，可以继续：

```text
修改
↓
Commit
↓
Push
```

然后重新提交最新的：

```text
最终Commit链接
```

教师评分以截止时间前最后一次正式提交版本为准。

---

# 24. 截止后修改

截止时间以后仍然可以修改 GitHub 仓库，用于：

```text
继续学习
修复错误
完善代码
```

但评分时仍按照课程迟交规则处理。

不得通过删除 Git 历史等方式隐藏原始提交过程。

---

# 25. 迟交规则

除教师另有说明外，Lab 迟交按照以下规则处理：

| 迟交时间         | 处理方式        |
| ------------ | ----------- |
| 按时提交         | 正常评分        |
| 24小时以内       | Lab原始成绩扣5分  |
| 24～48小时      | Lab原始成绩扣10分 |
| 超过48小时       | 原则上Lab最高80分 |
| 正式请假、疾病等特殊情况 | 按学校和课程规定处理  |

迟交扣分在 Lab 的 100 分原始成绩中执行。

---

# 26. 文件完整性要求

正式提交之前请确认：

```text
程序文件存在
REPORT.md存在
程序能够运行
没有明显调试垃圾文件
```

不要提交：

```text
临时测试文件
无关下载文件
超大数据文件
个人隐私文件
密码
API Key
```

---

# 27. 不应提交的内容

禁止将以下内容上传至 GitHub：

```text
账号密码
Token
API Key
身份证信息
敏感个人数据
未经授权的数据集
```

如果程序需要密钥，应使用环境变量等方式管理，不得直接写入仓库。

---

# 28. outputs和生成结果

部分后期 Lab 会生成：

```text
CSV
PNG
```

等结果。

如果 README 明确要求提交，则需要保留。

例如 Lab16：

```text
outputs/
├── prediction_results.csv
└── confusion_matrix.png
```

如果只是程序运行产生的大量临时文件，不需要全部提交。

---

# 29. data目录

对于教师已经提供的数据：

```text
data/
```

不要无故修改原始数据。

如果实验要求生成清洗后的数据，可以按照 README 中规定的新文件名保存。

例如：

```text
ai_experiments.csv
```

保留为原始数据，

生成：

```text
ai_experiments_clean.csv
```

作为处理结果。

---

# 30. 程序可运行性

教师检查时通常会从学生提交版本运行程序。

因此不要在代码中使用只能在自己电脑上运行的绝对路径，例如：

```python
"D:/Users/zhangsan/Desktop/python/data/test.csv"
```

推荐使用相对路径：

```python
"data/test.csv"
```

以保证代码换到其他电脑后仍然能够运行。

---

# 31. 第三方库

如果程序使用：

```text
numpy
pandas
matplotlib
scikit-learn
```

等课程规定库，可以正常使用。

不要在没有说明的情况下加入大量额外第三方依赖。

如确有必要，应在：

```text
REPORT.md
```

中说明。

---

# 32. 教师如何检查Lab

教师可能采用以下方式进行检查：

```text
检查目录和文件
↓
查看正式Commit
↓
运行核心程序
↓
使用教师测试输入
↓
检查输出结果
↓
检查代码结构
↓
查看REPORT.md
```

部分重点 Lab 还可能进行：

```text
现场代码检查
```

---

# 33. 现场代码检查

以下 Lab 可能重点安排现场检查：

```text
Lab09
Lab10
Lab11
Lab12
Lab15
Lab16
```

教师可能随机要求学生：

```text
解释一段代码
修改一个条件
改变一个参数
增加一个简单功能
运行指定测试
解释程序设计思路
```

例如：

```text
为什么这里使用dict？

为什么find_student()需要return？

CSV文件不存在时程序怎样处理？

Student和StudentManager分别负责什么？

X_train.shape表示什么？

fit()与predict()有什么区别？
```

现场检查通常时间较短，主要用于确认：

> 学生是否真正理解自己提交的程序。

---

# 34. AI工具使用说明

课程允许合理使用 AI 工具辅助学习，例如：

```text
解释语法
帮助理解报错
提供调试思路
解释第三方库API
生成测试思路
```

但学生必须能够：

```text
理解代码
解释代码
修改代码
运行代码
测试代码
```

不能直接提交自己完全无法解释的程序。

---

# 35. AI辅助记录

如果明显使用 AI 工具完成了某部分任务，请在：

```text
REPORT.md
```

的：

```text
AI辅助说明
```

中简要记录用途。

例如：

```text
使用AI帮助分析了FileNotFoundError，
根据提示自行修改了文件异常处理代码。
```

无需复制完整对话。

---

# 36. 学术诚信

禁止：

```text
直接复制其他同学完整作业
互相交换完整代码
使用他人仓库作为自己的提交
购买作业
提交无法理解的完整生成代码
```

基础程序出现部分相似属于正常现象。

课程判断重点不是简单比较代码文本，而会综合：

```text
Git提交过程
程序测试
代码解释
现场修改
实验记录
```

进行判断。

---

# 37. 遇到Git问题怎么办

如果遇到：

```text
clone失败
push失败
merge冲突
身份认证问题
文件误删除
```

不要重新建立大量仓库。

优先：

1. 阅读终端错误信息；
2. 检查当前目录；
3. 使用 `git status`；
4. 查阅课程 Git 示例；
5. 向教师说明具体错误信息。

提问时尽量提供：

```text
执行了什么命令
完整报错
git status结果
```

而不是只说：

```text
“Git不能用了。”
```

---

# 38. 每次提交前检查清单

提交 Lab 前请逐项确认：

```text
□ 已阅读完整README

□ 所有必做Task均已完成

□ 文件名称符合要求

□ 程序能够正常运行

□ 已使用多个输入进行测试

□ 已检查边界情况

□ REPORT.md已完成

□ git status已检查

□ 已完成Commit

□ 最终Commit名称为 Submit Lab XX

□ 已完成git push

□ GitHub网页能看到最新代码

□ 已复制正确的最终Commit链接

□ 已在课程平台完成正式提交
```

---

# 39. 推荐学习习惯

不要采用：

```text
截止前一次性写完所有代码
```

的方式。

推荐：

```text
阅读任务
↓
完成一个小功能
↓
运行
↓
测试
↓
Commit
↓
继续下一功能
```

Git 不只是：

```text
交作业工具
```

更重要的是：

```text
程序开发过程记录工具
```

---

# 40. Lab学习路线

整个课程包含：

```text
Lab01～Lab16
```

学习路线为：

```text
Python环境
   ↓
基础语法
   ↓
控制结构
   ↓
数据结构
   ↓
程序设计
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
数据可视化
   ↓
机器学习
   ↓
AI综合应用
```

请认真完成每一次实验。

后面的综合任务建立在前面 Lab 基础之上。

---

# 41. 最终说明

本课程关注的不只是：

```text
“程序有没有写出来”
```

还关注：

```text
程序是否正确
代码是否清晰
是否能够测试
是否能够解释
是否具有真实开发过程
```

希望通过 16 个 Lab 逐步形成：

```text
会写代码
   ↓
会调试代码
   ↓
会管理代码
   ↓
会组织程序
   ↓
会处理数据
   ↓
会使用机器学习工具
   ↓
会完成小型AI应用
```

的完整实践能力。
