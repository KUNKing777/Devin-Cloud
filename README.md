# Devin Cloud 完全教程

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
- 方案二：共享一个 Devin 账号
- 方案三：GitHub Organization 统一管理
- 知识共享的替代方案（AGENTS.md / REVIEW.md）
- 冲突处理
- 各方案对比（成本 / 知识共享 / 权限隔离）
- 最终推荐方案（2-5 人小团队）

---

## 快速开始（5 分钟版）

如果你只想快速体验，按以下步骤操作：

1. 打开 https://app.devin.ai ，用 GitHub 账号注册
2. 进入 Settings → Integrations → GitHub，连接你的仓库
3. 点击 New Session，选择 Agent 模式
4. 选择仓库，输入任务描述
5. 等待 Devin 完成，在 GitHub 上 review PR
6. Approve 并 merge

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

---

## 方案选择指南

| 场景 | 推荐方案 | 月成本 |
|------|----------|--------|
| 个人学习 | Free 方案 | $0 |
| 个人开发 | Pro 方案 | $20 |
| 2-3 人小团队 | 共享账号或 GitHub Org + 各自 Pro | $20-60 |
| 3-5 人团队 | GitHub Org + 各自 Pro | $60-100 |
| 5 人以上团队 | Teams 方案 | $80 + $40/人 |
| 大型企业 | Enterprise 方案 | 定制 |

---

## 官方资源

- 官方文档：https://docs.devin.ai
- Web 应用：https://app.devin.ai
- 代码审查：https://app.devin.ai/review
- 支持邮箱：support@cognition.ai
- 编码代理入门：https://devin.ai/agents101

---

*本教程基于 Devin 官方文档编写，最后更新：2026年6月*
