# 06 · 用 Grok Bot 写代码：云端编码代理、GitHub 与本机执行

[← 返回目录](../README.md)

## 1. 核心思路：Bot 是「外循环」，Cursor 云端代理是「内循环」

官方 DevRel 博客 *Grok Bot 101* 讲得很清楚：

> 我的「外循环」Bot 从 Slack、Notion、GitHub 和文档里收集上下文，然后把一份干净的提示词交给 Cursor 云端代理，由它在「内循环」里真正写代码……Grok Bot 并不是自己写代码，而是生成我本来会写的那份提示词，再把它交给 Cursor 里专门的编码工具。

所以在 Grok Bot 里做编码工作时：

- **Bot 负责**：理解需求、收集上下文、写清任务、启动 Cursor 云端代理、跟进进度、向你汇报结果（分支、PR、摘要）。
- **Cursor 云端代理负责**：读整个仓库、调查问题、改代码、开新分支和 Pull Request。

这样做的好处是「脏上下文」（讨论、争论、试错）留在外循环，执行代码的代理拿到的是干净的任务。

## 2. 你可以这样用

### 修 Bug / 加功能（已有仓库）

```text
在 github.com/<owner>/<repo> 里：用户反馈导出 CSV 时中文乱码。复现方法：在设置页导出任意含中文的列表。
期望：Excel 打开不乱码。请交给云端代理处理，完成后把 PR 链接和改动摘要发给我。
```

要点（来自 App 内置的编码工作说明）：

- 描述 **问题与期望结果**（症状、复现方法、约束、怎么算完成），而不是规定「改第 N 行」。
- 如果你有怀疑的原因，标明是「猜测，请自行验证」。
- 截图、设计稿、日志、规格文档可以作为附件交给代理（它真的能看到图片和文件）。
- 已有仓库的改动会在 **新分支 + Pull Request** 中完成。
- 对正在进行或刚完成的同一任务追加修改时，Bot 会回复 **同一个代理**，保留它的分支和上下文，而不是另起一个。
- 代理启动后会立即返回，Bot 会在代理完成时自动被唤醒，带回状态、分支、PR 和摘要。

### 从零开始一个新项目

```text
帮我从零做一个记账小网页应用：可以记录收入支出、按月汇总、导出 CSV。用你觉得合适的技术栈。
```

全新项目会在 **Cursor Origin**（Cursor 的源代码托管平台，GitHub 的替代品）里创建一个私有仓库开始工作。初始是一个未命名的草稿仓库，你之后可以让 Bot 给它命名并发布（选择仅自己可见或团队内部可见）。注意：**Cursor 不能代你创建 GitHub 仓库**，想放在 GitHub 上就先自己建一个空仓库，把链接给 Bot。

### 只是查一下

"这个配置文件里写了什么？""那个 PR 改了什么？"这类简单查询，Bot 会通过 GitHub / Origin 的远程只读接口直接看，**不会把仓库克隆到电脑上**。更深入的调查也会交给云端代理。

### 日常 GitHub 操作

Bot 可以直接在对话里帮你：查看 PR 和 diff、CI 状态、评审意见；查找或新建 Issue；评论、回复、评审；合并 PR（合并不可逆，若不是你明确要求的，会先确认，并先检查可合并状态和 CI）。所有操作都以 **你自己的 GitHub 账号权限** 进行，不会超出你本来能做的事。

GitHub（以及 GitLab、Bitbucket、Azure DevOps）连接是 **Cursor 账号里的一套集成**：你给 Cursor 云端代理连过 GitHub，Bot 就能用；没连过时 Bot 会在聊天中弹出连接或授权卡片。仓库「找不到」通常是 **没有授权给 Cursor 应用**，而不是仓库不存在。

## 3. 用例程盯 PR 和 CI

```text
盯着 <owner/repo> 的 PR #42：有评审意见或 CI 失败时，总结给我；如果是我能直接修的小问题，交给原来的云端代理去修。PR 合并或关闭后自动停止。
```

```text
<owner/repo> 的 main 分支 CI 失败时通知我，附上失败的检查名称和链接。
```

GitHub 例程支持的事件包括：PR 新建/推送/合并/关闭、评审请求/通过/要求修改/评论、PR 评论和行内评论、讨论串解决/重开、Issue 被指派、CI 通过/失败。可以只针对某个 PR，或用 GitHub 用户名过滤（例如"只看我自己开的 PR"）。详见 [第 4 章](04-routines.md)。

## 4. 官方博客里的真实工作流

*Grok Bot 101* 的作者（SpaceXAI DevRel）分享的 "Tech Demos" Bot：

```text
Name: Tech Demos
Title: Daily X tech scout
Description: Look at my bookmarks each weekday, pick one technology worth demoing, draft a prompt in my style,
wait for approve or deny, then kick a Cursor cloud agent.
```

每个工作日，它浏览作者的 X 书签挑出值得做 demo 的新技术，起草一份原型提示词并请作者批准；批准后通过 Cursor 连接启动云端代理；完成后发截图或短视频并开 PR。

## 5. 在你自己的电脑上执行（本机执行）

云电脑和你面前的 Mac/PC 是两台不同的机器。Bot 可以通过桌面 App 在 **你的本机** 上运行命令、读取文件，以及在云电脑和本机之间传文件，但这受 **单独的本机执行策略** 控制：

- 位置：**Settings → Computer → Your computer → Execution on this computer**（本机还没列出时显示为 **Execution on Local Computer**）。
- 选项：**Ask every time**（默认，逐条批准，审批卡片会显示确切命令）、**Always allow**、**Never allow**。
- 每台桌面电脑各自设置。团队管理员可以为全队设置上限；你自己的设置更严格时以你的为准。
- 官方安全文档建议：**除非 Bot 有明确理由处理本机文件，否则设为 Never allow。**
- 本机执行策略与 Auto-review（管云电脑上的操作）是两套独立控制。

什么时候需要本机执行？例如：某个服务只能从你的网络访问、需要处理只存在于你本机的文件、云电脑访问某个 API 被拦截。

> 已知问题（官方 FAQ）：Bot 有时会误报 "Local tools are turned off… set to Never"，即使你设置的是 Always allow 或 Ask every time。这是官方侧的问题，改设置或重装都不能解决，等待修复即可。

## 6. 用云电脑本身跑代码

云电脑有终端，Bot 可以写脚本处理数据、生成报表、跑一次性的自动化。但要记住：

- 手动安装的软件包在「计算机更新」/ Recover / Reset 后会被清掉；`node_modules`、Python 虚拟环境等不会被保存。
- 重要结果复制到 `/workspace` 或作为附件发到对话里。
- 真正的仓库改动交给云端代理，而不是在云电脑上克隆仓库自己改。

## 7. 小结：什么时候用什么

| 需求 | 用什么 |
|------|-------|
| 改代码、修 Bug、加功能、调查代码行为 | 让 Bot 启动 Cursor 云端代理 |
| 新项目 | 云端代理 + Cursor Origin 新仓库 |
| 查 PR / diff / CI / Issue、评论、合并 | Bot 在对话里直接操作 GitHub/Origin |
| 盯 PR 或 CI | GitHub 事件例程 |
| 数据处理、一次性脚本 | 云电脑终端 |
| 必须在你本机/你的网络里做的事 | 本机执行（逐条批准） |
