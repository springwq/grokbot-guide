# Grokbot Guide · Grok Bot 中文使用指南

> 一份面向中文用户、尤其是 **ChatGPT / Claude 老用户** 的 Grok Bot 实用指南。
> A practical, Chinese-first guide to **Grok Bot** — the desktop & mobile app that gives you persistent AI teammates ("Bots") with their own cloud computer.

本指南的内容全部来自：Cursor / SpaceXAI 官方文档与帮助中心、官方博客与公告、Grok Bot App 内置的功能说明，以及少量注明来源的社区经验。**凡是没有官方依据的内容都会明确标注「未验证」或「社区经验」**。完整来源见 [resources.md](resources.md)。

> ⚠️ Grok Bot 迭代很快（很多功能写着 "rolling out gradually / 逐步推出"）。如果你在 App 里找不到某个按钮，先更新 App，再查官方文档。本指南写于 2026 年 10 月。

---

## Grok Bot 是什么？（一句话版）

**Grok Bot 不是又一个聊天框，而是一群「有自己电脑的 AI 同事」。**

- 每个 **Bot** 都有名字、岗位、自己的对话和长期记忆；
- 你的所有 Bot 共用一台 **持久化的云端电脑**（浏览器 + 文件系统 + 终端），你合上笔记本它们也照常干活；
- 能用 **连接器（Connect apps，基于 MCP）** 操作 Gmail、日历、Notion、Slack、GitHub 等；没有连接器的网站就直接用浏览器去点；
- 能按 **例程（Routines）** 定时或按事件自动运行；
- 遇到登录、验证码、付款、发邮件这类敏感步骤，会 **停下来请你批准或接管**。

它由 SpaceXAI 推出、基于 Cursor 技术，使用你的 **Cursor 账号** 登录。桌面端支持 macOS / Windows / Linux，移动端支持 iPhone 和 Android。

---

## 目录

| # | 章节 | 你会学到 |
|---|------|---------|
| 0 | [5 分钟快速上手](#5-分钟快速上手) | 装好、登录、建第一个 Bot、交出第一个任务 |
| 1 | [docs/01-getting-started.md](docs/01-getting-started.md) | 安装、登录、套餐与用量、界面导览、移动端 |
| 2 | [docs/02-core-concepts.md](docs/02-core-concepts.md) | Bot、云电脑（box）、桌面、记忆、技能、团队/多 Bot |
| 3 | [docs/03-connectors.md](docs/03-connectors.md) | 连接器 / 插件：添加、授权、多账号、常见问题 |
| 4 | [docs/04-routines.md](docs/04-routines.md) | 例程：定时、事件触发、Webhook、测试、省用量（含大量示例） |
| 5 | [docs/05-browser-and-desktop.md](docs/05-browser-and-desktop.md) | 云电脑上的浏览器与桌面、登录流程、接管、安全 |
| 6 | [docs/06-coding-with-grokbot.md](docs/06-coding-with-grokbot.md) | Cursor 云端编码代理、GitHub、在你自己电脑上执行命令 |
| 7 | [docs/07-pages-canvas.md](docs/07-pages-canvas.md) | Pages：报告、看板、追踪表，以及分享 |
| 8 | [docs/08-email-meetings-channels.md](docs/08-email-meetings-channels.md) | Bot 专属邮箱、日程与会议、Slack 等渠道、语音 |
| 9 | [docs/09-shopping-travel-food.md](docs/09-shopping-travel-food.md) | 购物、付款、订餐、订位、机票酒店、打车、退换货 |
| 10 | [docs/10-security-and-privacy.md](docs/10-security-and-privacy.md) | 审批、Auto-review、先草稿后发送、密钥、隐私 |
| 11 | [docs/11-tips-for-chatgpt-claude-users.md](docs/11-tips-for-chatgpt-claude-users.md) | 从 ChatGPT / Claude 迁移：思维转换与实用提示词 |
| 12 | [docs/12-faq-troubleshooting.md](docs/12-faq-troubleshooting.md) | 常见问题与故障排查 |
| — | [examples/prompts.md](examples/prompts.md) | 按场景分类的大型提示词库（可直接复制） |
| — | [resources.md](resources.md) | 所有外部来源链接 |

---

## 5 分钟快速上手

### 第 1 分钟：安装

1. 打开官方下载页 <https://cursor.com/download/bot>（或 Cursor 控制台的 Grok Bot 页面 <https://cursor.com/dashboard/bot>），按系统选择安装包：
   - macOS：Apple silicon 或 Intel（「关于本机」里显示 *芯片* = Apple silicon，显示 *处理器* = Intel）
   - Windows：x64 或 Arm64
   - Linux：`.deb` / `.rpm` / AppImage（x64 或 Arm64；`uname -m` 输出 `x86_64` 即 x64，`aarch64` 即 Arm64）
2. 手机：App Store / Google Play 搜索 **Grok Bot**（iOS 18+ / Android 9+）。

### 第 2 分钟：登录

1. 打开 App，点欢迎页上的 **Sign in**，在浏览器里用 **Cursor 账号** 完成登录（没有单独的 Grok Bot 账号）。
2. 如果你的使用权来自 SuperGrok 订阅，按提示关联 Grok 账号；来自 Grok Business 席位的，在浏览器里选 **Sign in with Grok**。
3. 想用中文界面：**Settings → General → Appearance → Language → Chinese (Simplified)**。新 Bot 之后会用该语言回复你（除非你用别的语言跟它说话）。

> 打开设置的方式：左下角头像/账号按钮、快捷键 `Cmd+,`（Windows/Linux 为 `Ctrl+,`），或命令面板里的 "Open settings"。

### 第 3 分钟：认识你的第一个 Bot

登录并点完简短介绍后，App 会自动创建第一个 Bot（名字就叫 **Grok Bot**）并打开对话。首次使用时它还会问你常用哪些工具——这只用来推荐「未来同事」，不会自动连接或修改这些工具。

### 第 4 分钟：给它一个「岗位」并让它记住

在第一条消息里写清 **职责、信息来源、什么时候必须先问你**，并要求它 **记住**：

```text
你的工作是我的「研究助理」。一次只研究一个主题，使用网页搜索和我发给你的文档。
结论要附来源链接，把事实和推测分开写。任何要改动外部服务（发消息、提交表单、购买）的操作都先问我。
请记住这些规则，用于以后所有工作。
```

### 第 5 分钟：交出第一个任务

选一个 **结果清晰、不改动外部服务** 的小任务。比如附上一个 PDF：

```text
把这份文档总结成 5 个要点。另起一节列出所有日期、决定和未解决的问题，每条注明出处章节。不要修改原文件。
```

看结果、提修改意见。满意之后，下一步可以：

- 让它把这套做法 **保存成技能**（"把刚才的流程保存为一个叫『周报整理』的技能"）；
- 让它 **定时自动做**（"每个工作日早上 8:30 把……发到这个对话"）——见 [例程](docs/04-routines.md)；
- 去侧边栏 **Connect apps** 连上 Gmail / 日历 / Notion 等——见 [连接器](docs/03-connectors.md)。

---

## 最重要的 7 条心法

1. **一个 Bot 一个岗位。** 「研究员」「收件箱管家」「出行助理」比一个「万能助手」好用得多，记忆也更干净。
2. **把边界写进请求。** 明确「可以改什么、必须在哪一步停下来」。例如："起草但不要发送"、"加入购物车但不要下单"。
3. **先跑通一次，再存成技能，最后才做成例程。** 官方推荐的顺序就是这样。
4. **所有 Bot 共用一台电脑。** 在云电脑上登录的网站，所有 Bot 都能用。不想让某个 Bot 碰的账号就别登录。
5. **密码和验证码永远不要贴到聊天里。** 用 Bot 弹出的安全表单 / 安全密钥卡片，或者「接管」电脑自己输入。
6. **审批卡片要认真看。** 学习阶段用 **Allow once**；真正信任某类操作后再用 **Always allow**。
7. **例程会消耗用量。** 频率越高、触发越宽泛越贵。先用最低有用频率。

---

## 关于本仓库

- 仓库名：`grokbot-guide`（显示名 *Grokbot Guide*）
- 维护者：Steven Wu
- 语言：简体中文为主，保留常用英文术语（界面按钮名保持英文原文，方便对照 App）
- 本指南为个人整理的非官方资料，**不代表 SpaceXAI / Cursor 官方立场**。以官方文档为准。
