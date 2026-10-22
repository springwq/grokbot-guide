# 01 · 入门：安装、登录、套餐与界面导览

[← 返回目录](../README.md)

## 1. 系统要求与下载

| 平台 | 支持情况 | 获取方式 |
|------|---------|---------|
| macOS | Apple silicon 与 Intel | <https://cursor.com/download/bot> 或 <https://cursor.com/dashboard/bot> |
| Windows | x64 与 Arm64 | 同上 |
| Linux | x64 与 Arm64：`.deb`（Debian/Ubuntu）、`.rpm`（Fedora/RHEL）、AppImage | 同上（x.ai/bot 的 More downloads 也有） |
| iPhone | iOS 18 及以上（iPad 上 iPadOS 18+ 也可运行 iOS 版） | App Store |
| Android | Android 9 及以上 | Google Play |

安装要点：

- **macOS**：打开 dmg → 把 Grok Bot 拖进「应用程序」→ 打开（系统询问时选 Open）。
- **Windows**：运行安装程序 → 从开始菜单打开。
- **Linux**：用包管理器安装 `.deb` / `.rpm`，或给 AppImage 加执行权限后运行。

桌面 App 会 **自动检查更新**。也可以手动：**Settings → Updates → Check for Updates**，有更新时选 **Restart to Update**。如果版本落后超过 14 天且有新版，App 会显示 **Update required**，必须更新。

> 注意：**更新 App** 和 **更新 Bot 的电脑** 是两回事。前者在 Settings → Updates，后者在 Settings → Computer（见 [第 12 章](12-faq-troubleshooting.md)）。

## 2. 登录

- Grok Bot 使用 **Cursor 账号**，没有单独的 Grok Bot 登录。
- 欢迎页点 **Sign in** → 在浏览器完成登录 → 回到 App。
- 公司使用 SSO 的，走公司的正常 SSO 流程即可。
- 如果使用权来自 **Grok Business** 席位：在浏览器中选 **Sign in with Grok**，用持有席位的 Grok 账号登录。
- 桌面端支持多账号：账号菜单里有 **Switch account** / **Add account**。
- Grok Bot 需要云端数据存储；账号若处于 **Privacy Mode (Legacy)**，需要先切换到受支持的隐私设置才能开始使用。

### 常见登录问题

1. 先把 App 更新到最新版，再退出并重新登录。
2. 清除浏览器中 cursor.com 和 x.ai 的缓存与 Cookie，用无痕窗口再试。
3. 桌面端也可以试试在 <https://x.ai/bot> 用同一个 Cursor 账号登录。
4. 如果是新出现的错误，等 30–60 分钟再试。**重装 App 通常没用。**
5. 手机一直循环登录：先在桌面端登录成功。

## 3. 套餐与用量（简要）

> 套餐体系近期有变化（2026-10 Grok Bot 并入 *The X Subscription*）。**具体价格本指南不列出**，请以 App 内 **Settings → Usage & Billing** 和官方「Plans and billing」页面为准。

根据官方帮助中心：

- **The X Subscription**：Premium、Super、Ultra 包含 Grok Bot（Free 和 Plus 不包含）。Grok Bot 与 Cursor、Grok 共用 **一个每周用量池**；用完后从 **预付额度（prepaid credits）** 扣，可在 grok.com 的账单页设置 Auto Top-up 与月度上限。
- **旧版 Cursor 方案（legacy）**：Pro、Pro+、Ultra 和自助版 Teams 都包含 Grok Bot，用量按周重置；用完后可开启 **On-demand（按需）** 计费，并在 **Settings → Usage & Billing → On-demand monthly limit** 设置月度上限。
- **关联 SuperGrok / X Premium+**（旧版账号）：可关联个人 SuperGrok、SuperGrok Plus、SuperGrok Heavy、X Premium+。**关联是永久的，不能自己解除或转移。** Cursor 方案和关联 **不叠加**，取用量更高的那一个。SuperGrok Lite 不包含 Grok Bot。
- **试用**：免费试用是一笔「用量额度」，另有 7 天期限；一个大任务就可能把它用完，用掉的不退。
- **Grok App ≠ Grok Bot**：Grok 聊天 App 里的 "Weekly SuperGrok Limit" 与 Grok Bot 无关；Grok Bot 用量看 **Settings → Usage & Billing**。
- **模型**：Grok Bot 会为每个任务自动选择模型，**没有模型选择器**，也看不到某次请求用了哪个模型。
- 手机端：用同一个 Cursor 账号登录，权益自动带过去，**不要在 App Store / Google Play 再买一次**。

## 4. 第一次打开：引导流程

1. 登录后，App 会介绍 Bot、共享电脑和例程，并问你常用哪些工具（只用于推荐，不会自动连接）。
2. 云电脑在后台完成初始化。
3. 自动创建第一个 Bot（名为 **Grok Bot**）并打开对话；某些版本最后一步会打开 **Meet a future teammate**，你可以挑一个推荐的「同事」，或 **Create your own**。

## 5. 界面导览

### 左侧边栏

- **New chat（+ 按钮，`Cmd+N`）**：新建 Bot（**Create new Bot**）或新建群聊。想一开始就命名：先输入名字，再选 **Create "名字" Bot**。
- **Bot 列表**：右键某个 Bot 可以 **Pin（置顶）**、**Move to new section / Move to（分组）**、**Mark as Unread**、**Rename Bot**、**Copy conversation ID**、**Hide from sidebar（隐藏）**、**Delete（永久删除）**。
  - 隐藏的 Bot 仍在运行、保留历史、例程照跑，但不再发通知；在 **Hidden Bots** 里可以 **Show in sidebar** 恢复。
  - **Delete 是永久删除**，会删掉 Bot 的资料、对话和例程（云电脑上的文件和登录状态不会自动清理）。可能还要用的话，用「隐藏」代替删除。
- **Connect apps**：连接器 / 插件 / 打包技能的入口（不在设置里）。
- **账号按钮（左下角头像）**：设置、支持（Support → About 查看版本，**Copy version info** 复制版本信息）、获取手机版等。

### 对话区

- 可以粘贴文字、链接、图片，附加文件（桌面每条消息最多 6 个附件；文档/图片/音频单个 25 MB，视频 200 MB）。
- 输入 `/` 调用已保存的 **技能**；输入 `@` 提及某个 Bot、群聊、例程或应用。
- 可以回复或对某条消息加表情；Bot 工作中途你也可以继续发指令。你的直接消息 **优先于** 后台工作，可以改变当前任务方向。
- 发 **"Stop now"** 可以立刻停止（已完成的操作不会被撤销）。
- 对话里会显示工具活动、电脑操作、生成的文件、提问和审批请求。
- 消息框为空时会出现 **Start voice chat**（波形按钮）；**Start voice input** / `Cmd+D`（Win/Linux `Ctrl+D`）是语音输入。

### 单个 Bot 的信息面板（Details）

点击对话顶部的 Bot 名字（或 `Cmd+Shift+I`）打开。这里可以：

- 实时预览这个 Bot 的电脑画面，点击进入全屏查看；
- 查看 / 暂停 / 测试 / 编辑 **Routines（例程）**；
- **Library**：这个 Bot 制作的 Pages、文件和应用；
- 有可用的渠道连接器时显示 **Channels**；群聊里显示 **Members**；
- 点名字或头像修改 **名称、标签（label/title）、头像**（头像可选角色样式、**Generate** AI 生成或 **Upload** 上传，<25 MB）。

> 官方帮助中心说明：个人 Bot 已经没有单独的「描述」字段，**要改变 Bot 做什么，直接在聊天里告诉它**并让它记住。团队 Bot（Team Bot）仍有 **About** 描述。

### 全局设置（Settings）

标签页：**General**、**Computer**、**Vault**（仅部分账号）、**Usage & Billing**（仅部分账号）、**Updates**。

| 标签 | 常用内容 |
|------|---------|
| General | 账号（Sign In with Cursor / Sign Out）、主题（Follow System / Light / Dark）、语言、拼写检查、麦克风、通知声音、**时区（例程用）**、**Auto-review 开关与 Custom Rules**、硬件安全密钥、Team Bots 相关（Slack 关联、清除连接器偏好） |
| Computer | **Your computer**：本机执行策略（Execution on this computer）、**Route traffic through this computer**；**Bot's computer**：**Update Bot's Computer**、**Reset Bot's Computer** |
| Usage & Billing | 每周用量、按需用量、套餐管理 |
| Updates | Update Track（Stable / Nightly）、Check for Updates、Automatic Updates |

> 某些设置项只在部分账号、版本或状态下出现。找不到就先更新 App。

## 6. 手机端

- 与桌面端 **同一账号、同一台云电脑、同一批 Bot 和对话**，随时接着聊。
- 手机上不能更新 / 恢复 / 重置云电脑，这些要在桌面端做。
- 手机上可以 **Duplicate（复制）** 一个 Bot：会复制资料、设置、已启用技能、例程和头像，但不复制对话历史、学到的记忆和附件。
- iPhone 15 Pro 及以上的 **操作按钮（Action Button）**：在 iPhone「设置 → 操作按钮 → 快捷指令 → Grok Bot → Start Voice Chat」一键开始和主 Bot 语音对话（需 Grok Bot 1.16+，并先打开一次 App）。
- 通知：单个 Bot 的 **Notifications** 开关在 Bot 资料页；手机「设置」里可以整体关闭通知。没有「只在桌面端打开时静音手机」的选项。

## 7. 下一步

- 理解核心概念 → [02 核心概念](02-core-concepts.md)
- 连接常用应用 → [03 连接器](03-connectors.md)
