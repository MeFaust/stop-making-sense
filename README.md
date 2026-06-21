# Stop Making Sense

`stop-making-sense` 是一个 Codex skill，用于根据课程项目中的教材、习题、答案、课件、讲义、往年卷、OCR 文本和整理笔记，生成面向期末考试复习的中文 Markdown 教程。

GitHub 仓库：<https://github.com/MeFaust/stop-making-sense>

这个 skill 的目标不是简单摘要资料，而是让 Codex 按照统一的教程结构，把课程资料整理成可复习、可查题型、可考前速记的章节化文档。

## 适用场景

适合在以下任务中使用：

- 根据课程资料生成某一章或某一专题的复习教程
- 整理知识点、公式、定义、常见题型和考试陷阱
- 从教材、习题、答案和往年卷中提炼例题与题型
- 生成期末冲刺讲义、考前速记或可复用的 Markdown 学习材料

不适合用于：

- 生成与当前项目资料无关的通用百科内容
- 在没有课程资料的情况下凭空编写例题
- 替代人工核对最终答案和排版

## 目录结构

```text
stop-making-sense/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
├── assets/
│   └── 教程空模板.md
└── references/
    └── 第十章-常微分方程初步教程.md
```

说明：

- `SKILL.md`：Codex 读取的 skill 主说明文件，包含触发描述和执行规则。
- `agents/openai.yaml`：Codex app 使用的展示元数据，包括名称、简介和默认提示词。
- `assets/教程空模板.md`：生成新教程时可使用的空白结构模板。
- `references/第十章-常微分方程初步教程.md`：风格与结构参考文件。

## 安装方式

### 方法一：通过 Codex 安装器从 GitHub 安装

在 Codex 中直接使用内置安装器：

```text
$skill-installer https://github.com/MeFaust/stop-making-sense
```

安装完成后，执行 `Force Reload Skills` 或重启 Codex。

### 方法二：手动克隆并安装到 Codex 用户 skills 目录

在 Windows PowerShell 中执行：

```powershell
git clone https://github.com/MeFaust/stop-making-sense.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills" | Out-Null
Copy-Item -Recurse -Force ".\stop-making-sense" "$env:USERPROFILE\.codex\skills\stop-making-sense"
```

安装后目录应类似：

```text
C:\Users\你的用户名\.codex\skills\stop-making-sense\SKILL.md
```

### 方法三：安装到 `.agents` 用户 skills 目录

部分 Codex 版本也会读取 `$HOME/.agents/skills`。如果你的客户端使用这个目录，可以执行：

```powershell
git clone https://github.com/MeFaust/stop-making-sense.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.agents\skills" | Out-Null
Copy-Item -Recurse -Force ".\stop-making-sense" "$env:USERPROFILE\.agents\skills\stop-making-sense"
```

安装后目录应类似：

```text
C:\Users\你的用户名\.agents\skills\stop-making-sense\SKILL.md
```

如果不确定当前 Codex 版本读取哪个目录，可以两个目录都安装一份。若两个目录中存在同名 skill，建议保持内容一致，避免调用时混淆。

## 刷新 Codex 客户端

安装或更新后，建议按以下顺序刷新：

1. 在 Codex app 中打开命令菜单。
2. 执行 `Force Reload Skills`。
3. 新建一个 thread。
4. 在输入框中输入 `$`，查看是否出现 `stop-making-sense` 或 `Stop Making Sense`。
5. 如果仍未出现，完全退出并重启 Codex app。

也可以使用 Codex CLI 检查模型可见的 skills 列表：

```powershell
codex debug prompt-input "test skill loading" | Select-String "stop-making-sense"
```

如果命令能输出 `stop-making-sense`，说明 skill 已被 Codex 读取。

## 使用方法

在 Codex 中打开包含课程资料的项目文件夹，然后显式调用 skill：

```text
$stop-making-sense 请根据当前项目 source 目录中的资料，生成第六章的期末复习教程。
```

也可以描述更具体的目标：

```text
$stop-making-sense 阅读当前项目中的教材、习题答案和往年卷，整理一份“多元函数积分学”的考前速记和常见题型清单。
```

建议项目中按以下方式组织资料：

```text
course-project/
├── source/
│   ├── textbook.pdf
│   ├── exercises.pdf
│   ├── answers.docx
│   ├── slides/
│   └── past-exams/
└── outputs/
```

Codex 会优先搜索 `source/`，再搜索其他明显包含教材、习题、答案、往年卷、讲义、课件、OCR 文本或整理笔记的目录。

## 输出要求

该 skill 会引导 Codex 生成中文 Markdown 教程，通常包含：

- 资料依据
- 章节主线
- 教材或课程框架
- 主要知识点
- 公式、定义与解释
- 教材例题和习题选题
- 往年卷题型
- 本章常见题型清单
- 考前速记

生成结果应基于项目资料，不应凭空编造例题或结论。

## 发布到 GitHub

本仓库已经适合直接发布到 GitHub。维护者在仓库根目录执行以下命令即可。

### 1. 检查文件

```powershell
git status
Get-ChildItem -Force
```

确认至少包含：

```text
SKILL.md
README.md
agents/
assets/
references/
```

### 2. 初始化仓库

如果当前目录还不是 Git 仓库：

```powershell
git init
```

### 3. 添加文件

```powershell
git add SKILL.md README.md agents assets references
```

### 4. 提交

```powershell
git commit -m "Add stop-making-sense skill"
```

### 5. 绑定 GitHub 远程仓库

```powershell
git remote add origin https://github.com/MeFaust/stop-making-sense.git
```

如果远程已经存在，先查看：

```powershell
git remote -v
```

需要修改远程地址时：

```powershell
git remote set-url origin https://github.com/MeFaust/stop-making-sense.git
```

### 6. 推送

```powershell
git branch -M main
git push -u origin main
```

推送完成后，打开 <https://github.com/MeFaust/stop-making-sense>，确认文件显示正常，尤其检查中文文件名和 README 渲染是否正确。

## 发布前检查清单

上传前建议确认：

- `SKILL.md` 位于仓库根目录
- `README.md` 位于仓库根目录
- `agents/openai.yaml` 存在
- `assets/教程空模板.md` 存在
- `references/第十章-常微分方程初步教程.md` 存在
- 没有提交课程隐私资料、个人笔记、账号信息或临时输出
- 中文文件名在 GitHub 页面中显示正常
- Codex 能在安装后看到并调用 `$stop-making-sense`