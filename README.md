# Devin Cloud 零基础教程

> 从零开始，手把手教你使用 Devin Cloud 进行 AI 辅助开发和团队协作。
> 本教程面向小白，细致到每一次鼠标点击。

---

## 目录

### [第一章：注册与初始设置](01-注册与初始设置.md)
- 注册 Devin 账号（GitHub 注册 / 邮箱注册）
- 首次进入 Devin 主界面
- 连接 GitHub（最关键的一步）
- 选择仓库权限

### [第二章：配置开发环境](02-配置开发环境.md)
- 为什么要配置环境
- 两种配置方式（自动 / 手动）
- 使用经典向导配置（8 个步骤详解）
- 添加 Secrets（密钥）
- 验证环境是否配置成功
- 理解快照（Snapshot）机制

### [第三章：创建 Session 与布置任务](03-创建Session与布置任务.md)
- Ask 模式 vs Agent 模式
- 如何创建新 Session
- 如何写好任务描述（4 要素 + 实际例子）
- 使用 @ 提及引用资源
- Ask 模式详解（问答 + 规划）
- Agent 模式详解（自主执行）
- 并行运行多个 Session

### [第四章：PR 操作与 GitHub 工作流](04-PR操作与GitHub工作流.md)（最核心）
- Devin 的 Git 工作流程（分支机制）
- Devin 创建 PR 后你在 GitHub 上会看到什么
- 如何审查 Devin 的 PR（详细步骤）
- Approve / Request Changes / Comment 三种操作
- 处理 Devin 对 Review 的响应
- CI 检查失败的处理
- main 分支 vs 其他分支的区别
- Devin Review — 更强大的审查工具
- Auto-Fix 和 Auto-Review
- 完整工作流示例（从创建 session 到合并 PR）

### [第五章：Knowledge 与 Playbook](05-Knowledge与Playbook.md)
- Knowledge — 给 Devin 做"入职培训"
- Playbook — 标准化任务流程
- 团队协作中的 Knowledge 和 Playbook
- 典型的团队 Knowledge 和 Playbook 清单

### [第六章：团队协作](06-团队协作.md)
- 连接 Slack / Teams
- 连接 Jira / Linear
- Managed Devins — 并行任务分发
- 定时任务 — Scheduled Sessions
- 团队最佳实践

### [第七章：常见问题与故障排除](07-常见问题与故障排除.md)
- 注册与账号问题
- 环境配置问题
- Session 问题
- PR 相关问题
- Devin Review 问题
- 团队协作问题
- 费用相关问题
- 通用排错步骤

### [第八章：多人共管一个仓库](08-多人共管一个仓库.md)（实用场景）
- 方案一：各自独立 + GitHub 协调
- 方案二：使用 Teams 组织
- 为什么 Pro / Max 账号不能多人共享
- GitHub Organization、分支保护、CODEOWNERS
- 规则与流程共享（AGENTS.md / Skills / Git-backed Blueprint）
- 冲突处理
- 各方案对比和 2-5 人团队推荐

### [第九章：分支策略与直接推送](09-分支策略与直接推送.md)（进阶必读）
- 两种模式：PR 工作流 vs 直接推送
- 名词扫盲（分支 / main / init / base / commit / push / PR）
- PR 工作流下 base = main vs base = init 的区别
- 直接推送到 main vs 直接推送到 init 的区别
- 直接推送模式下如何在 GitHub 上查看和撤销（git revert）
- 我该选哪种模式？（决策建议）

### [第十章：官方最佳实践与提示词模板](10-官方最佳实践与提示词模板.md)（新手必读）
- 什么时候适合使用 Devin
- 任务前检查清单
- Ask Devin → Agent Session 的稳妥流程
- 好提示词 vs 坏提示词
- Bug / 功能 / 重构 / 测试 / 文档 / 排查模板
- Slash Commands（/plan、/implement、/test、/review、/think-hard）
- 如何让 Devin 自测、录屏和复盘

### [第十一章：进阶功能与自动化](11-进阶功能与自动化.md)（官方功能补全）
- Blueprint / Snapshot / Git-backed Blueprint
- AGENTS.md、Knowledge、Playbook、Skill 的区别
- Secrets 与 Site Cookies
- MCP Marketplace
- Devin Review、Auto-Review、Auto-Fix
- 测试录屏、Automations、Scheduled Sessions
- Slack / Teams / Jira / Linear 集成
- Devin CLI、Handoff、Session Insights

### [第十二章：团队管理与生产工作流](12-团队管理与生产工作流.md)（团队进阶）
- 邀请成员、Member / Admin 与席位的区别
- 导入本地 VS Code 设置、扩展和快捷键
- Slack Auto-triage 自动调查与分流
- Devin 的部署能力和限制
- Autofix Bot Comments 白名单与防循环
- 官方产品指南覆盖索引

---

## 快速开始（5 分钟版）

如果你只想快速体验，按以下步骤操作：

1. 打开 https://app.devin.ai ，用 GitHub 账号注册
2. 进入 Settings → Integrations → GitHub，连接你的仓库
3. 先用 Ask Devin 问清楚代码结构和实现计划
4. 确认计划后，点击 New Session，选择 Agent 模式
5. 选择仓库，输入“背景 + 任务 + 验收标准”
6. 让 Devin 自己运行 lint/test/build，必要时录屏测试
7. 等 Devin 创建 PR，在 GitHub 或 Devin Review 中审查
8. CI 和 Review 都没问题后再 Approve 并 merge

---

## 新手最稳任务描述公式

把任务写成 5 段，成功率会明显更高：

```text
背景：现在发生了什么问题，或者为什么要做这个功能。
目标：希望 Devin 完成什么。
范围：相关仓库、分支、文件、页面、接口、设计图或日志。
约束：不要改什么，必须保持什么兼容。
验收：跑哪些命令，看哪个页面，什么结果算完成。
```

最短可用模板：

```text
请在（仓库/功能）中完成（具体任务）。
参考（文件/链接/截图）。
不要改动（限制）。
完成后运行（lint/test/build 命令）。
创建 PR，并在 PR 描述中写清楚改了什么、为什么改、如何验证。
```

---

## 核心概念速查

| 概念 | 说明 |
|------|------|
| Session | 一次与 Devin 的交互，从创建到完成 |
| Ask 模式 | 问答/规划模式，不修改代码 |
| Agent 模式 | 自主执行模式，可以写代码、创建 PR |
| Snapshot | Devin 的虚拟机快照，包含所有工具和代码 |
| Knowledge | 团队知识，Devin 会自动回忆 |
| Playbook | 可复用的任务模板 |
| PR | Pull Request，Devin 提交代码变更的方式 |
| Devin Review | 专门的代码审查平台 |
| ACU | Agent Compute Unit，Devin 的计费单位 |
| Managed Devins | 并行执行多个子任务 |
| AGENTS.md | 仓库中的通用指令文件，Devin 会自动读取 |
| 分支（Branch） | 代码的"平行存档"，可独立修改后再合并 |
| Base 分支 | Devin 从哪个分支创建工作分支、PR 合并回哪个分支（默认 main） |
| 直接推送模式 | 配置 Devin 不开 PR，直接 commit + push 到某分支（见第九章） |
| Slash Commands | 输入 `/` 使用官方提示词快捷命令，如 `/plan`、`/test` |
| Skill | 仓库内可复用操作流程，常用于测试、部署、登录 |
| MCP | 连接外部工具的协议，可接 Sentry、Datadog、Figma、数据库等 |
| Automations | 按 Slack、GitHub、Linear、Webhook 等事件自动触发 Devin |
| Auto-triage | 持续监听 Slack Bug 频道，自动去重、调查和分流问题 |
| Scheduled Sessions | 按时间自动运行 Devin 任务 |
| Session Insights | 会话复盘工具，用于分析 ACU、卡点和改进建议 |
| Computer Use | Devin 使用浏览器/桌面进行 UI 操作、截图和录屏 |
| Devin CLI | 在本地终端使用 Devin，并可 `/handoff` 交给云端 Devin |
| Autofix Bot Comments | 控制 Devin 是否处理可信 PR 机器人的评论 |

---

## 方案选择指南

| 场景 | 推荐方案 | 月成本 |
|------|----------|--------|
| 个人学习 | Free 方案 | $0 |
| 个人开发 | Pro 方案 | $20 |
| 临时小团队 | GitHub Org + 每人独立 Free/Pro | 每人 $0-20 |
| 正式团队 | Teams（Full seat / Flex seat） | 最低 $80 |
| 高频团队成员 | Teams Full seat | $40/席位，仍受 $80 最低费用约束 |
| 低频团队成员 | Teams Flex seat | 席位免费，使用共享 on-demand credits |
| 大型企业 | Enterprise 方案 | 定制 |

> Pro 和 Max 是单用户方案，不能通过共享账号供多人使用。价格可能调整，请以 https://devin.ai/pricing 为准。

---

## 官方资源

- 官方文档：https://docs.devin.ai
- 官方 Essential Guidelines：https://docs.devin.ai/zh/essential-guidelines
- Web 应用：https://app.devin.ai
- 代码审查：https://app.devin.ai/review
- 支持邮箱：support@cognition.ai
- 编码代理入门：https://devin.ai/agents101

---

*本教程基于 Devin 官方文档编写，共 12 章，最后更新：2026年7月*
