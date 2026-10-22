# 03 · 连接器（Connect apps / 插件 / MCP）

[← 返回目录](../README.md)

## 1. 连接器是什么？

连接器（App 里叫 **apps**，底层是 **MCP** 服务器，打包在 **插件 plugin** 里）让 Bot 以 **结构化** 的方式操作外部服务，比如 Gmail、Google 日历、Notion、Slack、GitHub。

- **有连接器时优先用连接器**：比在网页上点来点去更可靠，数据也更准确（例如导出 CSV 而不是读截图）。
- **没有连接器时**：Bot 会直接用云电脑上的浏览器去操作该网站（见 [第 5 章](05-browser-and-desktop.md)）。
- Grok Bot 支持与 Cursor 相同的 MCP 服务器、插件和技能（官方 DevRel 博客 *Grok Bot 101*）。
- 插件保存在你的 **Cursor 账号** 里，跨设备同步。

## 2. 关键事实

- **连接是账号级的**：一个应用连上后，你的 **所有 Bot** 都能用。（同事的 Team Bot 要用你的账号时会先问你。）
- **令牌不落在电脑上**：OAuth 令牌保存在 Cursor 的连接器后端，Bot 调用工具时拿不到令牌本身。
- **权限不会被放大**：应用只能做你授权的那个账号本来就能做的事，不能提升权限，也不能改共享设置。
- **团队策略**：被团队管理员禁用的应用会显示 **Disabled by team admin**。注意：禁用应用不会阻止 Bot 用浏览器访问那个网站（要封网站需要 Enterprise 的 Network Controls）。

## 3. 怎么添加一个连接器

**方法 A：直接让 Bot 做（推荐）**

```text
帮我连接 Notion。
```

Bot 会在目录里搜索、安装，并在聊天中弹出 **Connect 卡片**，你点它在自己的浏览器里完成授权。授权完成后 Bot 会自动继续。新装的工具通常从 **下一条消息** 起可用。

**方法 B：手动**

1. 侧边栏 **Connect apps**（手机：左上角头像 → Connect apps）。
2. 浏览或搜索应用，添加。
3. 出现 **Authorize / Authenticate** 时，在浏览器里完成服务商登录。
4. 没完成的话，点应用上的 **Reconnect** 或聊天卡片上的 **Reopen** 重新打开登录页（大约 10 分钟内要完成）。
5. 确认它出现在 **Installed** 里。

> **Added ≠ 已登录。** "Added" 只表示已安装。打开应用查看状态：**Needs auth / Disconnected** → 点 **Authenticate**；**Connected** → 给 Bot 发条新消息让它再试一次。

**方法 C：目录里没有的服务**

- 如果服务官方提供远程 MCP 地址（https URL），可以让 Bot 直接添加；需要令牌时 Bot 会向你索取（用安全方式，而不是写进 URL）。
- 如果是本地运行的 MCP（文档里的 `npx` / `uvx` 命令），也可以加，它会运行在你的云电脑上，所有 Bot 都会用到。
- 不在官方目录、服务方也没发布的包是 **未经审核** 的，Bot 会先提醒你。
- 实在没有连接器、也没有接口：只要是能登录的网站，Bot 就用浏览器去做。

## 4. 多账号

- 有些应用可以连多个账号（例如两个 Notion 工作区）：**Connect apps → 打开应用 → Accounts → Add Another Account**，给账号起个标签（work / personal），再 **Authorize**。之后对 Bot 说"用我的 work Notion"即可。
- **Gmail 一次只能连一个邮箱**。要换邮箱需先断开再授权另一个。
- 不想让某个 Bot 用某个邮箱？连接是全账号共享的，唯一办法是断开。

## 5. 常见应用能做什么（官方说明）

| 应用 | 能做 | 不能做 / 注意 |
|------|------|--------------|
| Google Calendar | 读取你能看的日历、创建/更新事件、查空闲、回复邀请 | 不能改 Google Meet 设置（等候室、主持人控制）；不能添加 Zoom 链接（那是 Google 的 Zoom 插件） |
| Google Sheets | 读写你有编辑权限的表格单元格 | 查找/打开文件用 **Google Drive** 应用；不能改共享权限 |
| Gmail | 搜索阅读、起草发送、打标签 | 只能连一个邮箱 |
| Slack | 以 **你连接的 Slack 用户身份** 发帖、读取 | 只能在该用户能发言的频道发；每个工作区要分别连接；与「Slack 触发的例程」是两回事 |
| X | **公开 X 内容内置可用**（搜帖子、看主页、提及、趋势、新闻，无需连接也无需额度） | X 插件只用于私有数据（私信、书签、首页时间线、谁点赞了你），需要你自己 X 开发者账号上的 **X API 额度**（console.x.com 购买） |
| Zoom | — | 已知问题：桌面端授权报错 4700，目前无解 |

> 公司 Google 账号连接时提示 "Your admin needs to review Grok" 或 "Access blocked"：Grok Bot 以 **Grok** 的名义登录 Google，需要你的 Google Workspace 管理员在 Admin console 里把 **Grok** 设为 Trusted。换浏览器或重连没用。

## 6. 在聊天里交互的应用界面

据社区对 0.70.2 版本更新的整理：Figma、Notion、Canva 等应用可以直接在聊天里显示交互界面。（来源：X 用户 @mark_k 的版本说明汇总，非官方文档。）

## 7. 管理与告诉 Bot「怎么用」

- 卸载、重启连接器会改动你的账号，Bot 会先征得你同意；搜索和查看状态不需要。
- 你可以告诉 Bot 某个连接器的使用偏好，它会保存下来，例如：
  ```text
  以后用 Notion 时，所有会议纪要都放在「Meetings」数据库里，标题格式为「YYYY-MM-DD 主题」。
  ```
- **有些连接器发出的内容会显示为「某应用」而不是你本人**。如果你需要以自己身份发言，Bot 可能更倾向用你已登录的浏览器来发送、用连接器来读取。

## 8. 起步推荐清单

根据官方用例页和个人用法，下面这些最常用：

1. **Gmail / Outlook**：收件箱整理、找验证码、找订单邮件。
2. **Google Calendar**：日程安排（Bot 对日历的写操作都通过日历连接器，不会去网页上改）。
3. **Google Drive / Docs / Sheets / Slides**：文件读写、上传生成的演示文稿。
4. **Notion**：个人 CRM、知识库、会议纪要。
5. **Slack**：读消息、以你的身份发帖、作为例程触发源。
6. **GitHub**：PR、Issue、CI；配合 Cursor 云端编码代理（见 [第 6 章](06-coding-with-grokbot.md)）。
7. **钱包类**（X Money、Stripe Link、Shop Pay）：代你付款，每笔都需批准（见 [第 9 章](09-shopping-travel-food.md)）。
8. **1Password**：如果你本来就用，可以让 Bot 在登录时用它来填密码。

## 9. 故障排查速查

| 现象 | 处理 |
|------|------|
| 连接卡片一直不出现 | 别等，去 **Connect apps** 打开该应用点 **Authenticate** |
| 卡片显示 waiting for authorization | 点 **Reopen**；显示失败则 **Retry** |
| 显示 Added 但 Bot 说没有 | 检查状态，Needs auth → Authenticate |
| 重新授权后仍显示断开 | **Remove** 后重新添加；仍不行联系支持（附应用名和账号邮箱） |
| Disabled by team admin | 找 Cursor 团队管理员开启 |
