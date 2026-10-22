# 12 · 常见问题与故障排查

[← 返回目录](../README.md)

## 第一原则：先完全退出再打开

**大多数问题，完全退出 Grok Bot 再重开就能解决。** Mac 上要从菜单栏选 **Quit**，而不是只关窗口。

---

## A. 账号与套餐

**Q：需要单独订阅 Grok Bot 吗？**
不需要。The X Subscription 的 Premium / Super / Ultra，以及旧版 Cursor Pro / Pro+ / Ultra / 自助版 Teams 都包含；旧版账号还可以关联 SuperGrok、SuperGrok Plus、SuperGrok Heavy 或 X Premium+。Enterprise 请问客户经理。详见 [第 1 章](01-getting-started.md)。

**Q：Grok Bot 和 Grok App 是一个东西吗？**
不是。Grok（xAI 的聊天 App）和 Grok Bot 是两个不同的 App。Grok App 里的付费墙或 "Weekly SuperGrok Limit" 与 Grok Bot 无关。

**Q：Bot 不回复了，说我用量用完了，是坏了吗？**
不是，每周用量用完了，每周会重置。想继续：The X Subscription 用预付额度；旧版 Cursor 方案开启按需用量；或升级套餐。

**Q：怎么防止用量用完后继续扣钱？**
The X Subscription：在 grok.com 账单页关闭 Auto Top-up 或设置月度额外用量上限。旧版 Cursor：**Settings → Usage & Billing → On-demand monthly limit**，或网页 cursor.com/dashboard → Spending → Monthly Limit。注意上限不会中途打断正在运行的任务，可能略微超出。

**Q：用量掉得特别快？**
先看例程频率。每小时、短间隔、或盯着热闹频道的 Slack 触发，可能一天用掉一周的量。暂停不需要的例程，放宽时间表，收窄触发条件。群聊里 Bot 越多、回复越多。

**Q：试用在一个任务里就用完了，能退回吗？**
不能。试用是一笔用量额度，用掉不退。

**Q：在手机上要再付一次钱吗？**
不用。用同一个 Cursor 账号登录即可。在 App 内购买的订阅由 Apple / Google 处理取消和退款。

**Q：SuperGrok 关联错了 Cursor 账号能解除吗？**
不能自己解除，关联是永久的。联系官方支持。

**Q：能改账号邮箱吗？**
不能，Cursor 账号邮箱不可更改。

**Q：能选模型吗？**
不能。Grok Bot 为每个任务自动选择模型，没有模型选择器。

**Q：Grok Bot 挂了吗？**
看 <https://status.cursor.com> 的 **Grok Bot** 一栏（App 里不显示服务状态）。有事故时：等待，**不要 Reset 电脑或重装 App**，事故解决后重发消息。

## B. Bot 与对话

**Q：我的对话或 Bot 不见了？**
通常没被删。按顺序：完全退出重开 → 在另一台设备（比如手机）上看 → 打开侧边栏 **Hidden Bots** → 确认登录的是同一个 Cursor 账号。**不要用 Recover 或 Reset 去找对话**。都没有再联系支持。

**Q：删除和隐藏有什么区别？**
**Hide from sidebar**：只是从列表移走，Bot 继续运行、保留历史、例程照跑、不发通知，可以恢复。**Delete**：永久删除资料、对话和例程，不可恢复（云电脑上的文件和登录不会被删）。

**Q：怎么让 Bot 在群聊里回复而不是私聊我？**
在群里说"就在群里回复，不要私信我"，并让每个 Bot 记住。

**Q：怎么关掉「助手 Bot」的通知？**
桌面端：让那个 Bot 自己关掉通知；手机：打开它的对话 → 点名字 → 关 **Notifications**；或者直接隐藏它。

**Q：为什么改不了某个 Bot 的名字？**
只有拥有者能改名称、头像、标签（例如同事的 Team Bot）。

**Q：怎么拿到 request ID 报错？**
右键消息 → **Copy request ID**（或悬停 → More message actions）。

**Q：怎么看 App 版本？**
账号菜单 → **Support → About**，**Copy version info** 复制版本、更新通道和系统信息。

## C. 云电脑（Bot's computer）

**Q：电脑显示 Reconnecting / Couldn't Reach Grok Bot's Computer / Bot failed to respond？**
按这个顺序，**从最不具破坏性的开始**：

1. 等一下，点 **Retry**（重连期间 Bot、文件、登录都是安全的，**这时不要 Reset**）。
2. 完全退出 App 重开；检查 App 更新。
3. 有提示时选 **Recover Grok Bot's Computer**。
4. **Settings → Computer → Update Bot's Computer**（按钮写 **Update**，需要点两次确认 "Click Again to Confirm"）。
5. **Reset Bot's Computer** 只作为最后手段。

| 操作 | 做什么 | 保留 | 清除 |
|------|-------|------|------|
| **Update** | 升级到最新版本。软件更新只刷新 Grok Bot 软件；计算机更新会重建整台电脑（有时可以排期） | 软件更新：全部；计算机更新：Bot、文件、登录 | 计算机更新：已安装的软件和包 |
| **Recover** | 尽量保存后，用保存的数据在最新版本上新建电脑；会中断运行中的工作 | 已保存的 Bot、文件、登录 | 已安装的软件和包；电脑无法连接时的极近期改动 |
| **Reset** | 用上次保存的数据新建电脑；会中断运行中的工作 | 已保存的 Bot、文件、登录 | 同上 |

- 不要在一个 Update/Reset 还在进行时再开一个。
- Recover/Reset 失败，点一次 **Retry Recovery / Retry Reset**，还不行就联系支持。
- 「Update 说文件还没准备好」：等一会儿再试，不要用 Reset 强推。
- 「An agent couldn't pause in time」：等那个 Bot 做完再点 Update。
- 手机上不能做这些操作，要用桌面端。
- 对话存在电脑之外，即使 Reset 也不会丢对话。

**Q：Update 后我装的软件 / 存的密钥没了？**
计算机更新、Recover、Reset 会清除已安装的软件和包（`node_modules`、Python 虚拟环境等也不保存），需要重装。写在文件、shell 配置或已安装工具里的密钥可能随之消失；**通过安全卡片保存的密钥不受影响**（终端里打印不出来不代表被删）。

**Q：提示 "Computer is low on disk space"？**
说的是云电脑，不是你的笔记本。点 **Go to Disk Saver**——Disk Saver 是侧边栏里的一个 Bot，会检查空间占用并建议清理，**你确认前不会删除任何东西**，也不影响对话。

**Q：我在电脑里 `rm -rf` 删了文件怎么办？**
对话不受影响。Grok Bot 保存了已同步数据的持久副本，重新打开电脑通常能恢复已同步的文件。Recover 后仍为空，停止操作并联系支持。只存在你 Mac/PC 本地的文件不在保护范围内。

**Q：网站超时 / 连接错误 / 一直加载不出来？**
云电脑走 Cursor 的共享网络出口，有些网站会掐断这种连接。**Update / Recover / Reset 都没用。** 试试 **Settings → Computer → Your computer → Route traffic through this computer**，或开启本机执行。见 [第 5 章](05-browser-and-desktop.md)。

**Q：网站把 Bot 拦住了 / 一直出验证码？**
Bot 会把这一步交给你；也可以开启 **Route traffic through this computer**。

**Q：Bot 会用我自己的电脑吗？**
只有你允许时。**Settings → Computer → Your computer → Execution on this computer**，默认每次都问。

**Q：Bot 说 "Local tools are turned off"，可我设置的是允许？**
官方已知问题，你的设置没错，改设置或重装都清不掉，等修复。

## D. 连接器与登录

**Q：应用显示已添加，但 Bot 说没有？**
"Added"只代表已安装。打开应用看状态，**Needs auth / Disconnected** 就点 **Authenticate**（手机上叫 **Authorize**）。

**Q：连接卡片点了没反应？**
等待授权就点 **Reopen**，失败就点 **Retry**，10 分钟左右内在浏览器完成登录。

**Q：能连两个 Gmail 吗？**
不能，一次一个。Notion 等部分应用可以加第二个账号。

**Q：公司 Google 账号提示管理员需要审核 Grok？**
需要 Google Workspace 管理员在 Admin console（Security → Access and data control → API controls → App access control → Manage third-party app access）把 **Grok** 设为 Trusted。

**Q：Zoom 连不上（错误 4700）？**
官方已知问题，暂无解决办法。

**Q：X 插件连上了，但书签、私信、时间线读不了？**
公开 X 内容不需要插件；私有数据需要你在 console.x.com 的 X API 账户有余额。重连插件或换套餐都没用。

**Q：公司应用要 Okta / SSO，Face ID 和通行密钥用不了？**
它们在 Bot 的云电脑上本来就不能用。用 **Take over** 接管电脑，用公司允许的方式（密码+验证码、推送确认）登录；Mac/Windows 可用硬件安全密钥。

**Q：一直登录循环 / 认证错误？**
更新 App → 退出重登 → 清除 cursor.com 和 x.ai 的 Cookie 用无痕窗口 → 桌面端试 x.ai/bot → 等 30–60 分钟。重装通常没用。

## E. 例程、审批、通知

**Q：例程没运行？** 见 [第 4 章第 10 节](04-routines.md#10-例程为什么没运行)。

**Q：审批还没看到就过期了？**
例程、触发器、其他 Bot 发起的工作中的审批约 10 分钟过期。给这些 Bot 打开通知，信任的动作用 Always allow，过期后让 Bot 重试。

**Q：为什么例程留了一封草稿而不是直接发？**
设计如此。Bot 邮箱的每封邮件都需要你按 Send，没有无人值守发送选项。

**Q：手机和桌面都在弹通知？**
没有「桌面开着时手机静音」的选项。可以关掉单个 Bot 的 Notifications，或在手机设置里整体关闭。

**Q：Grok Bot 窗口在前台时没有桌面通知？**
设计如此，前台时通知被抑制，侧边栏和 Dock 角标仍会显示。

## F. 其他

**Q：Pages 看不到？**
逐步推出中，Enterprise 暂不支持。桌面更新到 0.60.0+，手机 1.14.0+。

**Q：Teach a task 按钮找不到？**
逐步推出中。改为用文字描述 + 完成一次任务，然后让 Bot 存成技能。

**Q：语音通话按钮找不到？**
**Start voice chat** 只在输入框为空时显示。仍看不到就更新 App。

**Q：Bot 邮箱名字起错了能改吗？**
不能。每人一个地址，不能改名也不能删除。

**Q：怎么联系支持？**
登录 Cursor 账号后在 <https://cursor.com/help> 联系支持。附上：账号邮箱、Grok Bot 版本（Support → About → Copy version info）、截图、request ID、已尝试的步骤。不要发送任何密钥的值。

---

## 设置速查表

| 想做什么 | 位置 |
|---------|------|
| 打开设置 | 左下角账号按钮 / `Cmd+,` / 命令面板 "Open settings" |
| 改语言、主题 | Settings → General → Appearance |
| 改例程时区 | Settings → General → Bot → Timezone |
| Auto-review 与自定义规则 | Settings → General → Bot 区域 → Auto-review / Custom Rules |
| 硬件安全密钥 | Settings → General → Security Key |
| Team Bot 的 Slack 关联、清除连接器偏好 | Settings → General → Team Bots |
| 本机执行策略 | Settings → Computer → Your computer → Execution on this computer |
| 流量走本机 | Settings → Computer → Your computer → Route traffic through this computer |
| 更新 / 重置云电脑 | Settings → Computer → Bot's computer |
| 用量与套餐 | Settings → Usage & Billing |
| 更新 App、切换 Stable/Nightly | Settings → Updates |
| 连接器、私有技能 | 侧边栏 Connect apps（不在设置里） |
| 单个 Bot 的名称/头像/例程/Library | 点对话顶部 Bot 名字（`Cmd+Shift+I`） |
| 删除 Bot | 侧边栏右键 Bot → Delete（不在设置里） |

> 某些设置项只在部分账号、版本或状态下出现。如果找不到，先更新 App，再查官方文档。
