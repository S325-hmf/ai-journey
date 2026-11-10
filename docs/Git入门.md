# Git 入门：从第一次 commit 到推到 GitHub

> 这份文档你会反复用到。忘了就回来看。

## 零、两个概念先搞清（30 秒）

| 概念 | 是什么 |
|---|---|
| **本地仓库** | 你电脑上 `ai-journey\.git` 这个隐藏文件夹，记录你所有的历史版本 |
| **远程仓库** | GitHub 网页上的那个仓库，是本地仓库的备份 + 展示窗口 |
| **commit** | 给当前所有代码拍一张快照，附一句话说明 |
| **push** | 把本地快照传到 GitHub |

一句话：`commit` 是存档，`push` 是上传。

---

## 一、本地第一次 commit（5 分钟）

打开终端，先进入项目目录（**每次都要先 cd**）：

```powershell
cd C:\Users\Administrator\Documents\deepseek-harness\default-workspace\ai-journey
```

### 1. 初始化仓库（只做一次）

```powershell
git init
```

看到 `Initialized empty Git repository in ...` 就对了。这时目录里会多出一个隐藏的 `.git` 文件夹。

### 2. 看看当前状态

```powershell
git status
```

会显示红色的 `Untracked files`——意思是这些文件 Git 还没管。

### 3. 把文件加入暂存区

```powershell
git add .
```

> `.` 表示「当前目录下所有文件」。
> `.gitignore` 里写的文件（比如 `.env`、`__pycache__`）会被自动跳过，不用你操心。

### 4. 拍快照

```powershell
git commit -m "chore: 第0周 环境准备与 hello.py"
```

`-m` 后面引号里就是这次改动的说明。**写清楚做了什么**，以后回看能看懂。

### 5. 查看历史

```powershell
git log --oneline
```

输出类似：

```
a1b2c3d chore: 第0周 环境准备与 hello.py
```

**有一行 = 第 0 周第 2 项过关。**

---

## 二、在 GitHub 上建远程仓库（5 分钟）

### 1. 先得有账号

如果还没有：https://github.com/signup

- 用户名建议用真名拼音，例如 `zhangwei-trade`，它会出现在简历上
- 验证邮件可能在 QQ 邮箱的**垃圾邮件**里

### 2. 建仓库

打开 **https://github.com/new**

| 字段 | 填什么 |
|---|---|
| Repository name | `ai-journey` |
| Description | `AI 学习 24 周：项目与练习`（可留空） |
| Public / Private | 选 **Public**（面试官要能点开看） |
| Add a README file | ❌ **不要勾** |
| Add .gitignore | ❌ **不要勾** |
| Choose a license | 不选 |

⚠️ 那三个初始化选项**一个都不要勾**。勾了会生成远程文件，和你本地的冲突，新手最容易卡在这。

点 **Create repository**。

---

## 三、把本地和远程连起来（5 分钟）

建完页面会显示一堆命令，照着下面敲就行（把 `你的用户名` 换成实际的）：

```powershell
git remote add origin https://github.com/你的用户名/ai-journey.git
```

```powershell
git branch -M main
```

```powershell
git push -u origin main
```

### 第一次 push 会弹窗

会跳出一个浏览器窗口或弹窗让你登录 GitHub，点 **Authorize / 授权** 即可。

> Git for Windows 自带了凭据管理器（GCM），会帮你记住，只用授权这一次。
> **不要输账号密码**——GitHub 早就不支持密码推送了，必须走浏览器授权。

### 验证

刷新 GitHub 仓库页面，能看到 `hello.py`、`README.md`、`docs/` 就成功了。

---

## 四、以后的日常循环（每天就这三步）

```powershell
git status                      # 看改了什么
git add .
git commit -m "feat: 完成第1周D1 变量练习"
git push                        # 第二次之后不用再写 -u origin main
```

**计划铁律 4：每天至少 1 个 commit。commit 记录就是你的学习证据。**

---

## 五、commit message 怎么写

格式：`类型: 做了什么`

| 类型 | 什么时候用 | 例子 |
|---|---|---|
| `feat` | 新增功能/练习 | `feat: 完成九九乘法表` |
| `fix` | 修 bug | `fix: 修正闰年判断逻辑错误` |
| `docs` | 改文档 | `docs: 补第2周复盘` |
| `chore` | 杂项（环境、配置） | `chore: 安装 uv` |

---

## 六、报错对照表

| 报错 | 原因 | 怎么办 |
|---|---|---|
| `fatal: not a git repository` | 没 cd 到项目目录 | 先 `cd` 到 `ai-journey` |
| `remote origin already exists` | 之前加过 remote | `git remote -v` 看一眼，错了就 `git remote remove origin` 再来 |
| `Updates were rejected` | 远程有本地没有的提交 | 说明你建仓库时勾了 README，`git pull --rebase origin main` 再 push |
| `403 / Authentication failed` | 授权失败 | 清凭据：控制面板 → 凭据管理器 → Windows 凭据 → 删掉 github 相关的，重新 push |
| `fatal: unable to access` | 网络问题 | 换个网络/开热点重试 |
| 提交里全是乱码文件名 | 中文路径 | `git config --global core.quotepath false` |
| 提交了不该提交的密钥 | 疏忽 | **立刻**去平台后台吊销该密钥，再 `git rm --cached` |

---

## 七、三条安全铁律

1. **密钥永远不进仓库**：API Key 写进 `.env`，`.env` 已在 `.gitignore` 里
2. **公司真实客户/合同数据永不上传**，一律脱敏或合成数据
3. 提交前跑一次 `git status`，看清楚要提交什么
