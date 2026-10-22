# 10 · 安全与隐私：审批、Auto-review、先草稿后发送

[← 返回目录](../README.md)

一个能登录你的账号、能付款、能发邮件的 AI，安全机制是第一要务。这一章讲清楚 Grok Bot 的几层防线，以及你应该怎么配置。

## 1. 先建立正确的心智模型

1. **Bot 没有自己的身份**：它以你（登录的成员）的身份行事，权限永远不会超过你本人。
2. **所有 Bot 共用一台电脑**：文件、浏览器登录、命令行凭据对你所有的 Bot 都可见。**多个 Bot 不是安全边界。** 如果某项工作需要独立的电脑和凭据，官方建议给它一个单独的 Cursor 用户。
3. **用户之间严格隔离**：每个用户独享一台硬件隔离的虚拟机，别人碰不到你的电脑。
4. **连接器令牌不在电脑上**：OAuth 令牌保存在 Cursor 后端，Bot 调用工具时拿不到令牌。
5. **凭据留在你手里**：登录、两步验证、付款这类步骤，Bot 会把电脑交给你，或用安全表单让你输入；它不会看到你的密码。

## 2. 审批卡片（Approvals）

当 Bot 要执行需要你确认的操作时，会停下来并在聊天里显示审批卡片（标题如 **Review an action**），列出拟执行的操作和参数。**你选择之前，操作不会执行。**

| 按钮 | 作用 |
|------|------|
| **Allow once** | 这次允许 |
| **Always allow** | 以后同类操作不再询问（会在 Custom Rules 里加一条规则） |
| **Deny** | 阻止这次操作 |

- 审批只控制「拟执行的操作」，不会撤销已完成的工作。
- **看不懂目标或后果的操作，不要批准。**
- 学习阶段多用 **Allow once**；真正信任某类动作后再用 **Always allow**。
- 待处理审批会出现在：对应 Bot 的对话里、侧边栏（显示需要注意）、通知（如果该 Bot 的 **Notifications** 打开；Grok Bot 窗口在前台时桌面通知不弹，但侧边栏仍显示）。
- **过期规则**：你在场发起的对话里，审批会一直等你；**例程、事件触发、其他 Bot 发起的工作**里的审批约 **10 分钟后过期**，过期后操作不执行。对策：给跑例程的 Bot 开通知；信任的动作用 Always allow；过期后让 Bot 重试。
- 在 App 内置规则中，**不可逆或对外可见的操作**（发邮件/消息、发帖、购买、提交表单、删除数据等）都属于需要确认的范围；社区汇总的 0.70.2 更新说明也提到「在购买、发帖、删除数据等不可逆操作前增加了审批检查」。

## 3. Auto-review（自动审查）

Auto-review 是审批背后的审查层：**一个独立的审查模型**，在 Bot 的高风险操作执行前进行评估，覆盖：

- 终端命令（shell）
- 应用/连接器调用
- 电脑操作（computer use）
- 自动化写入（创建或修改例程、事件触发器）
- 委派（启动 Cursor 云端代理、子代理等）

它可以 **放行**、**要求你审批** 或 **直接拒绝**。

### 在哪里设置

**Settings → General**，在 **Bot** 区域找到 **Auto-review** 开关和 **Custom Rules**。（官方帮助中心有的页面写作 "Settings → Bot"，指的是同一处。）开关说明文字为：*Grok Bot checks each action before it runs and asks you first when needed. Add rules to customize what it can do automatically.*

### 写自定义规则

- 用 **自然语言** 写，一条规则对应一类动作。规则有两种：**Ask first**（总是先问）和 **Allow automatically**（审查器没有发现其他问题时自动放行）。
- **规则冲突时 Ask first 优先。**
- 规则要 **窄而具体**，避免"浏览器里什么都允许"这种宽泛规则。
- 个人规则保存在你的账号里，所有桌面端和 iPhone 都生效。
- Enterprise 团队管理员可以强制开启 Auto-review 并添加团队规则（显示为锁定行 *Required by your admin*），成员只能在其上加更严格的规则。

推荐的起步规则（可直接照抄后修改）：

```text
Ask first：发送任何对外邮件或消息之前
Ask first：任何购买、付款、订阅之前
Ask first：删除文件、邮件、日历事件或任何数据之前
Ask first：在任何社交平台发帖或评论之前
Ask first：提交任何在线表单（申请、注册、预约）之前
Ask first：修改任何生产环境设置之前
Allow automatically：在 /workspace/reports 目录下运行 git status
```

### 它不管什么

Auto-review **不审查所有副作用**，例如写入记忆和大多数设置修改。把它当作补充，和明确的边界、最小权限、逐项审批、网络策略、用户隔离一起使用。

## 4. 先草稿、后发送

这是 Grok Bot 最重要的习惯之一：

- **Bot 自己邮箱发出的每一封邮件都要你按 Send**——包括例程和回复，没有无人值守发送的选项。
- **以你的名义发的邮件和 Slack 消息**（通过 Gmail / Outlook / Slack 连接器），默认先出一张可编辑的草稿卡片，你改好再按 Send。只有你明确说"不用给我看，直接发"，Bot 才会跳过卡片。
- 你丢弃草稿卡片，Bot 会当作你拒绝，不会换个方式偷偷发出去。
- 在给 Bot 的请求里也要写边界："起草但不要发送"、"给我一份待审列表，不要发给任何人"。官方用例页的每个起步提示词都 **刻意停在审阅点**。

## 5. 密码、密钥与安全表单

- **永远不要把密码、一次性验证码、API Key 粘贴到普通聊天、终端或普通文件里。**
- Bot 需要密钥时会弹出 **安全密钥卡片（secure secret card）**：输入框是遮蔽的，点 **Save securely** 后显示 *Saved securely and kept private*，值不会出现在对话里，也不会给模型看。之后再也不会显示这个值（只写不读），空白不代表被删了。
- 网页需要你输入时用 **安全表单**：值直接填进网页，卡片显示 *Filled into the page. Secret values were never shown to your Bot.*
- 演示教学（Teach a task）时不要输入密码。
- Team Bot 上保存的密钥会被所有能和它聊天的同事的对话使用，只放你愿意全队使用的 Key。
- 你把密码直接打在聊天里，Bot 会用它完成当前任务但不会复述，可能会提醒你事后改密码。最好还是用安全表单。

## 6. 本机执行与网络

- Bot 在你本机执行命令受 **Settings → Computer → Your computer → Execution on this computer** 控制：**Ask every time**（默认）/ **Always allow** / **Never allow**。官方建议没有明确需要就设为 **Never allow**。
- **Route traffic through this computer** 会让网站看到你的 IP，并让 Bot 能访问你这台设备能访问的网络——开启前想清楚。

## 7. 外部内容与「提示词注入」

网页、邮件、应用结果、命令输出里可能藏着试图操纵 Bot 的文字。Grok Bot 的做法：

- 外部内容在交给模型时被标记为 **不可信数据**；
- 邮件里别人的请求 **不构成你的授权**；
- Auto-review 会对照你的原始请求审查 Bot 的动作；
- 底层还有不依赖模型判断的控制：网络策略、逐项审批、用户隔离。

官方原话：这些控制「降低但不能消除」恶意内容的风险——这正是关键操作要保留审批的原因。

## 8. 数据与隐私

- 登录、数据设置沿用 Cursor 账号；**不支持 Privacy Mode (Legacy)**，需切换到受支持的设置。
- 在团队中时遵循团队的隐私模式；开启 Privacy Mode 时客户数据不用于训练。
- 模型提供方遵循 Cursor 现有的零数据保留协议（服务方可能运行滥用/安全分类器）。
- Grok Bot 自动选择模型（xAI 一方模型或子处理方列表中的第三方模型），用户无法指定或屏蔽某个模型。
- 云电脑目前运行在美国（与 Cursor 的「仅美国数据驻留」计划不是一回事）。
- 删除账号：Grok Bot 用的是 Cursor 账号，删除 Grok Bot 就是删除 Cursor 账号（手机：Settings → 你的账号 → Delete Account；网页：cursor.com/dashboard → Settings → More → Delete Account）。Bot、对话、电脑、连接的应用都会删除，30 天内清除完毕。App Store / Google Play 订阅、SuperGrok、X Premium+ 要另行取消。删除后你的 Bot 邮箱地址会被永久停用、不会再分配。
- Anysphere（Cursor 母公司）持有 ISO/IEC 27001 和 ISO/IEC 42001 认证，Grok Bot 在认证范围内。

## 9. 安全配置清单（第一天就做）

- [ ] 打开 **Auto-review**，加上第 3 节的起步规则
- [ ] **Execution on this computer** 设为 **Ask every time** 或 **Never allow**
- [ ] 给每个 Bot 的第一条消息里写清「哪些事必须先问我」并让它记住
- [ ] 只在云电脑上登录你愿意让 **所有 Bot** 使用的账号
- [ ] 给跑例程的 Bot 打开 **Notifications**，避免审批过期
- [ ] 密钥只通过安全卡片/表单提供
- [ ] 分享 Bot 模板或公开 Page 前检查有没有私密信息
- [ ] 定期清理：不用的例程、连接器、`/workspace` 中的敏感文件、云电脑上的网站登录
