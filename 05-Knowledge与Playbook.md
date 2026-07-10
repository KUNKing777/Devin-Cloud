# 第五章：Knowledge 与 Playbook — 让 Devin 学习你的团队规范

> Knowledge 和 Playbook 是 Devin 团队协作的核心。它们让 Devin 记住你的团队规范，而不是每次都从零开始。

---

## 5.1 Knowledge（知识库）— 给 Devin 做"入职培训"

### 什么是 Knowledge？

Knowledge 就是你告诉 Devin 的"公司规矩"。比如：
- 我们用 Conventional Commits 规范
- 我们的 API 返回格式是 `{ code: 0, data: null, msg: "" }`
- 我们的测试框架是 Jest，不用 Mocha
- 部署流程是先 staging 再 production

Devin 会在所有 session 中自动回忆相关的 Knowledge，不需要你每次都重复说。

### 如何创建 Knowledge

#### 第一步：进入 Knowledge 页面

1. 进入 **Settings & Library** → **Knowledge**
2. 你会看到已有的知识条目列表

#### 第二步：创建新条目

1. 点击右上角 **Create knowledge**
2. 填写两个字段：

**Trigger Description（触发描述）**
- 告诉 Devin 什么时候应该使用这条知识
- 例如："当处理 API 响应时"
- 或者："当编写测试时"

**Content（内容）**
- 具体的知识内容
- 例如："所有 API 响应必须使用统一格式：{ code: 0, data: null, msg: '' }"
- 例如："测试文件放在 __tests__ 目录下，命名格式为 xxx.test.js"

3. 可选：设置 **Macro（宏）**
   - 一个快捷标识符，格式为 `!名称`
   - 例如：`!api-format`
   - 以后在 prompt 中输入 `!api-format` 就能快速引用这条知识
   - 宏只能包含字母、数字和连字符，并且在组织内不能重名

4. Knowledge 默认属于当前组织，组织成员都可以使用
   - 每位成员可以单独启用或禁用某条 Knowledge，不会影响其他人
   - Enterprise 用户还可以创建跨组织共享的 Enterprise Knowledge

5. 点击 **Save** 保存

### 如何管理 Knowledge

#### 文件夹组织

- 点击 **New Folder** 创建文件夹
- 拖拽知识条目到文件夹中
- 按项目/团队/工作流分组

#### 绑定仓库

你可以将知识条目绑定到特定仓库：

1. 点击知识条目进入编辑
2. 找到 **Repository binding** 选项
3. 选择：
   - **不绑定** — 仅在相关时检索
   - **绑定特定仓库** — 在该仓库工作时始终使用
   - **绑定所有仓库** — 所有 session 自动应用

#### 启用/禁用

每个知识条目都可以单独启用或禁用，不影响其他条目。

### Knowledge 的最佳实践

1. **每条知识聚焦单一工作流** — 不要把所有规矩写在一条里
2. **保持更新** — 过时的知识比没有知识更糟糕
3. **拆分大条目** — Devin 可以同时访问多条知识
4. **使用文件夹** — 按项目/团队/工作流分组
5. **持续积累** — 每次 Devin 做得不好时，添加一条知识让它下次做得更好

### Devin 自动建议知识

Devin 会根据你在 session 中的反馈自动建议要记住的知识：

1. 在 session 中，如果 Devin 做了你不满意的事，你告诉它正确的做法
2. Devin 会建议："要我把这个记住吗？"
3. 你可以：
   - **Accept** — 接受建议，保存为知识
   - **Edit** — 编辑后再保存
   - **Reject** — 拒绝

---

## 5.2 Playbook（剧本）— 标准化任务流程

### 什么是 Playbook？

Playbook 是可复用的任务模板。当你有一个经常重复的任务时，把它写成 Playbook，以后每次只需要引用 Playbook，不用重新写 prompt。

**Playbook vs Knowledge 的区别**：
- **Knowledge** = 通用知识（编码规范、架构指南）
- **Playbook** = 特定任务流程（创建 PR、修复 bug、写测试）

### 什么时候用 Playbook？

- 你发现自己经常给 Devin 写类似的 prompt
- 团队中多个人需要让 Devin 做同样的事情
- 你有一个成功的 session，想把这个方法保存下来复用

### 如何创建 Playbook

#### 第一步：进入 Playbooks 页面

1. 进入 **Settings & Library** → **Playbooks**
2. 点击 **Create Playbook** 按钮

#### 第二步：编写 Playbook 内容

先写清楚两个最重要的内容：

1. 最终要达到什么结果
2. 为了达到结果，需要按什么步骤执行

下面 5 个章节是官方推荐的可选结构，不要求每个 Playbook 全部包含：

**1. Procedure（流程）**

这是 Playbook 的核心，列出每一步要做什么：

```markdown
## Procedure

### 准备阶段
1. 切换到 main 分支，拉取最新代码
2. 创建新分支：devin/<时间戳>-<功能名>
3. 研究相关代码，理解现有架构

### 执行阶段
4. 实现功能（参考 xxx 文件的写法）
5. 运行 lint 检查
6. 运行测试

### 交付阶段
7. commit 并 push
8. 创建 PR
9. 发送 PR 链接给用户
```

**2. Specifications（规格）**

完成后应满足的条件：

```markdown
## Specifications
- PR 不包含无关的改动
- 所有测试通过
- lint 检查通过
- PR 描述包含改动摘要
```

**3. Advice（建议）**

纠正 Devin 的默认倾向：

```markdown
## Advice
- 使用 git diff 检查改动再 commit
- 不要修改没有被要求修改的文件
- 如果不确定，先问用户
```

**4. Forbidden Actions（禁止操作）**

绝对不能做的事：

```markdown
## Forbidden Actions
- 禁止 force push
- 禁止直接 push 到 main
- 禁止在浏览器中访问 github.com
```

**5. Required from User（用户需提供）**

需要用户输入的信息：

```markdown
## Required from User
- 要工作的仓库
- 具体的功能需求
```

#### 第三步：保存 Playbook

点击 **Save** 保存。Playbook 会出现在你的 Playbooks 列表中。

### 如何使用 Playbook

#### 方式 1：从 Playbook 列表选择

创建 session 时，从 Team 或 Community Playbook 列表中选择一个。看到输入框附近出现蓝色 Playbook 标签，说明已经附加成功；开始前还可以临时编辑内容。

#### 方式 2：使用宏（Macro）

如果 Playbook 设置了宏（如 `!quick-pr`），可以直接写：

```
!quick-pr
```

#### 方式 3：附加 `.devin.md` 文件

你也可以把 Playbook 保存成 `任务名.devin.md`，新建 session 时拖入输入框。适合先在本地或仓库中 review，再交给 Devin 使用。

### Playbook 的最佳实践

1. **从成功的 session 中提取** — 如果某个 session 效果很好，把过程写成 Playbook
2. **并行运行 2+ 个 Devin 来测试** — 快速发现 Playbook 中的问题
3. **明确"完成"的标准** — 不要含糊
4. **包含具体命令** — 比如 `git checkout -b devin/$(date +%s)-feature`
5. **版本迭代** — 每次使用后如果发现问题，及时修改 Playbook

### 版本历史

Playbook 每次编辑保存都会自动创建版本。如果改坏了，可以回退到之前的版本。

---

## 5.3 团队协作中的 Knowledge 和 Playbook

### 组织级 vs 企业级

- **组织级 Knowledge/Playbook** — 当前组织内所有成员可见
- **企业级 Knowledge/Playbook** — 跨企业所有组织共享

### 典型的团队 Knowledge 清单

```
📁 编码规范
  ├── API 响应格式
  ├── 命名规范
  ├── 错误处理规范
  └── TypeScript 类型规范

📁 项目架构
  ├── 目录结构说明
  ├── 模块依赖关系
  └── 数据库 Schema

📁 部署流程
  ├── Staging 部署步骤
  ├── Production 部署步骤
  └── 回滚流程

📁 测试规范
  ├── 测试文件命名
  ├── 测试覆盖率要求
  └── Mock 规范
```

### 典型的团队 Playbook 清单

```
📋 快速 PR
📋 Bug 修复流程
📋 新功能开发流程
📋 代码迁移流程
📋 依赖更新流程
📋 文档更新流程
```

---

## 5.4 小结

1. **Knowledge** = 给 Devin 做入职培训，让它记住团队规范
2. **Playbook** = 标准化任务流程，让重复任务一键执行
3. 两者结合使用，Devin 就能像一个经验丰富的团队成员一样工作
4. 持续积累和迭代是关键 — 每次 Devin 做得不好，就添加 Knowledge 或改进 Playbook

---

## 官方参考

- Knowledge：https://docs.devin.ai/product-guides/knowledge
- Creating Playbooks：https://docs.devin.ai/product-guides/creating-playbooks
- Using Playbooks：https://docs.devin.ai/product-guides/using-playbooks
