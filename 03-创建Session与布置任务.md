# 第三章：创建 Session 并给 Devin 布置任务

> 学会如何与 Devin 交互，让它帮你完成具体的开发任务。

---

## 3.1 两种模式：Ask vs Agent

在创建 session 之前，你需要理解两种模式的区别：

### Ask 模式（问答/规划）

- **不修改代码**，只做探索和规划
- 可以问代码库相关的问题（Devin 会搜索代码并给出带引用的回答）
- 可以帮你规划任务，生成详细的执行计划
- 适合：了解代码库、讨论方案、制定计划

### Agent 模式（自主执行）

- Devin 的**完全自主模式**
- 可以写代码、运行命令、浏览网页、创建 PR
- 适合：实现功能、修 bug、写测试、重构代码

**推荐工作流**：先用 Ask 模式规划 → 再用 Agent 模式执行

---

## 3.2 创建一个新 Session

### 第一步：点击 New Session

在 Devin 主界面，点击 **New Session** 按钮（通常在左上角或左侧边栏顶部）。

### 第二步：选择模式

在 session 创建界面，你会看到两个选项卡：

- **Ask** — 切换到 Ask 模式
- **Agent** — 切换到 Agent 模式

点击你需要的模式。

### 第三步：选择仓库

在仓库选择器中，选择你要 Devin 工作的仓库。

**重要**：只能选择你之前在环境配置中添加过的仓库。如果看不到你的仓库，说明你还没有完成第二章的环境配置。

### 第四步：选择 Agent 类型（仅 Agent 模式）

如果你选择了 Agent 模式，还需要选择 Agent 类型：

- **Devin**（默认）— 通用 AI 软件工程师，适合大多数任务
- **Fast Mode** — 优化过的快速模式，适合简单明确的任务
- **Dana** — 数据分析代理，适合数据库查询和数据可视化

**不确定选哪个？** 用默认的 Devin 就好。

### 第五步：输入任务描述

在底部的输入框中，输入你要 Devin 做的事情。

---

## 3.3 如何写好任务描述（Prompt）

这是使用 Devin 最重要的技能。写得好，Devin 就能高效完成；写得差，Devin 可能做出完全不同的东西。

### 好的任务描述 = 4 个要素

#### 1. 提供上下文
告诉 Devin 你在说什么，背景是什么。

#### 2. 给出具体指令
不要说"改进一下"，要说具体做什么。

#### 3. 定义成功标准
告诉 Devin 怎样才算完成。

#### 4. 提供参考
告诉 Devin 参考哪些文件、哪些现有代码。

### 实际例子

#### 差的写法：
```
帮我加一个用户统计接口。
```

**为什么差？** Devin 不知道要什么统计数据、用什么格式、参考什么代码。

#### 好的写法：
```
在 statsController.js 中创建一个新的 API 端点 /users/stats。

要求：
1. 返回 JSON 格式，包含 user_count（用户总数）和 avg_signup_age（平均注册天数）
2. 使用 PostgreSQL 的 users 表
3. 参考现有的 /orders/stats 端点的代码结构
4. 在 StatsController.test.js 中添加对应的测试用例
5. 确保通过 lint 检查
```

**为什么好？** 具体、有参考、有验证标准。

### 更多例子

#### 添加前端功能：
```
在 UserProfileComponent 中添加一个下拉菜单，显示用户角色列表：
admin、editor、viewer。

要求：
1. 使用 DropdownBase 组件的样式
2. 选择角色后调用现有的 setRole API
3. 验证：选择角色后，数据库中的用户角色是否更新
```

#### 写单元测试：
```
为 AuthService 的 login 和 logout 方法添加 Jest 测试。

要求：
1. 测试覆盖率至少 80%
2. 参考 UserService.test.js 的写法
3. 验证：运行 npm test -- --coverage，确认两个方法覆盖率 >80%
4. 测试用例需包含：有效凭据、无效凭据、logout 清除 session
```

#### 代码迁移：
```
将 logger.js 从 JavaScript 迁移到 TypeScript。

要求：
1. 项目已有 tsconfig.json，不要修改它
2. 已有 LoggerTest.test.js 测试套件
3. 验证步骤：
   - 运行 tsc 确认无类型错误
   - 运行 npm test LoggerTest.test.js 确认测试通过
   - 检查代码库中所有 logger 方法调用是否仍然正常
```

---

## 3.4 使用 @ 提及（@ Mentions）

在输入框中输入 `@`，可以引用具体的资源，让 Devin 更精准地理解你的任务：

- **@Repos** — 引用特定仓库
- **@Files** — 引用特定文件（比如 @src/utils/auth.js）
- **@Macros** — 引用 Knowledge 中的宏
- **@Playbooks** — 引用 Playbook 模板
- **@Secrets** — 引用密钥
- **@Sessions** — 引用之前的 session 作为上下文

**例子**：
```
参考 @src/controllers/orderController.js 的代码结构，
在 @src/controllers/userController.js 中添加一个获取用户订单列表的接口。
```

---

## 3.5 Ask 模式详解

### 什么时候用 Ask 模式？

- 你想了解代码库的某个部分是如何工作的
- 你想让 Devin 帮你规划一个复杂任务
- 你不确定该怎么实现，想先讨论方案
- 你想让 Devin 分析代码中的问题

### 使用步骤

1. 创建新 session，选择 **Ask** 模式
2. 选择仓库
3. 输入你的问题或需求

### Ask 模式的两种用法

#### 用法 1：问答

```
这个项目的认证流程是怎么工作的？
哪些文件处理了用户登录？
```

Devin 会搜索代码库，给出详细的回答，并引用具体的文件和代码行。

#### 用法 2：规划

```
我想给这个项目添加一个文件上传功能，
支持图片和 PDF，最大 10MB。
帮我规划一下实现方案。
```

Devin 会分析代码库，给出详细的实现计划，包括：
- 需要修改哪些文件
- 需要添加哪些新文件
- 具体的实现步骤
- 可能遇到的问题

### 从 Ask 转到 Agent

在 Ask 模式中规划好之后，你可以直接转到 Agent 模式执行：

1. 在 Ask 会话中，Devin 给出了详细的计划
2. 点击 **Send to Devin** 按钮（或类似按钮）
3. Devin 会自动创建一个 Agent session，使用 Ask 中生成的计划作为任务描述
4. Agent session 开始自主执行

---

## 3.6 Agent 模式详解

### 什么时候用 Agent 模式？

- 你已经有了明确的任务描述
- 你需要 Devin 实际修改代码
- 你需要 Devin 创建 PR
- 你需要 Devin 运行测试、调试问题

### Agent 模式的工作流程

当你提交任务后，Devin 会：

1. **分析任务** — 理解你要做什么
2. **制定计划** — 列出具体步骤
3. **执行代码修改** — 编辑文件、运行命令
4. **自测** — 运行 lint、test、build 来验证
5. **创建 PR** — commit + push + 创建 Pull Request
6. **报告结果** — 告诉你做了什么，给你 PR 链接

### 你可以在 Agent 工作时做什么？

Devin 工作时，你可以在右侧边栏看到它的实时进展：

- **Shell 标签页** — 查看 Devin 执行的每一条命令和输出
- **IDE 标签页** — 查看 Devin 编辑的代码，甚至可以直接接管编辑
- **Browser 标签页** — 查看 Devin 浏览的网页

你也可以：
- **暂停 Devin** — 点击暂停按钮，Devin 会停止工作
- **接管 IDE** — 直接在 Devin 的编辑器中修改代码
- **发送消息** — 给 Devin 发送额外的指令或反馈

---

## 3.7 Session 完成后

Devin 完成任务后，你会看到：

1. **任务总结** — Devin 做了什么的简要说明
2. **PR 链接** — Devin 创建的 Pull Request 链接
3. **Session Insights** — 可以点击生成详细分析

### 查看 Session Insights

1. 在 session 页面，点击 **Session Insights** 按钮
2. 点击 **Generate Analysis**
3. Devin 会分析整个 session，给出：
   - 事件时间线
   - 可操作的反馈
   - 改进后的提示模板（下次可以用更好的 prompt）

---

## 3.8 并行运行多个 Session

Devin 支持同时运行多个 session，每个 session 处理不同的任务：

1. 创建第一个 session，提交任务 A
2. 不等它完成，直接创建第二个 session，提交任务 B
3. 两个 session 会并行执行
4. 你可以在左侧边栏的 Sessions 列表中查看所有 session 的状态

**适合并行的任务**：
- 独立的 bug 修复
- 不同模块的功能开发
- 互不依赖的代码迁移

---

## 3.9 小结

现在你已经学会了：

1. Ask 模式和 Agent 模式的区别和用法
2. 如何写好任务描述（上下文 + 指令 + 成功标准 + 参考）
3. 如何使用 @ 提及引用具体资源
4. 如何在 Devin 工作时监控和干预
5. 如何并行运行多个任务

下一步：学习 Devin 完成任务后，如何在 GitHub 上处理 PR。
