# 第四章：Devin 完成任务后 — GitHub 上的 PR 操作

> 这是最关键的一章。Devin 帮你写了代码、提交了 PR，然后你该怎么做？

---

## 4.1 Devin 的 Git 工作流程（必须理解）

### Devin 不会直接修改你的仓库主分支

这是一个非常重要的概念，很多新手会搞混：

```
你的远程仓库（GitHub）
  ├── main 分支（受保护，Devin 不会直接改这里）
  ├── dev 分支
  └── ... 其他分支

Devin 的工作流程：
  1. 在云端虚拟机中克隆仓库
  2. 从 main 分支创建一个新分支：devin/<时间戳>-<功能名>
  3. 在新分支上修改代码
  4. 运行 lint 和 test 自测
  5. git add + git commit + git push（推到远程新分支）
  6. 自动创建 Pull Request
```

### 分支命名规则

Devin 创建的分支名格式为：
```
devin/<时间戳>-<功能描述>
```

例如：
- `devin/1717750000-add-user-stats-api`
- `devin/1717750100-fix-login-bug`
- `devin/1717750200-migrate-logger-to-ts`

### 关键点

- Devin **不会** force push（强制推送）
- Devin **不会**直接 push 到 main/master
- Devin **总是**创建新分支，然后通过 PR 合并
- Devin 遵守和人类工程师一样的分支保护规则

> ⚠️ 例外：以上是**默认行为**。如果你手动配置了"直接推送到某分支、不开 PR"，Devin 就会直接 commit + push 到 main 或 init 等分支，而**不会**创建 PR。这种"直接推送模式"以及"在 main 上工作和在 init 上工作有什么区别"，专门在 **[第九章](09-分支策略与直接推送.md)** 详细讲解。本章只讲默认的、最常用的 **PR 工作流**。

---

## 4.2 Devin 创建 PR 后，你在 GitHub 上会看到什么？

### 4.2.0 新手第一视角：从"Devin 说完成了"到"打开 GitHub PR"

很多新手卡在这一步——Devin 说"我创建了 PR"，然后呢？一步步来：

1. **在 Devin 的 session 页面**（你和 Devin 对话的那个页面），Devin 完成后会发一条消息，里面有一个**蓝色的 PR 链接**，长得像：
   ```
   https://github.com/你的用户名/你的仓库/pull/123
   ```
   （`123` 是这个 PR 的编号。）
2. 你也可能收到一封 **GitHub 发来的邮件**（标题类似 "[你的仓库] 新功能 (#123)"），点邮件里的按钮也能直达。
3. **用鼠标点击这个 PR 链接**，浏览器会打开一个新标签页，进入 GitHub 上的 **PR 详情页**。
4. 如果 GitHub 提示你登录，就用你的 GitHub 账号登录（和注册 Devin 用的是同一个账号最方便）。

到这里，你就站在 PR 详情页了。下面解释这个页面长什么样。

### PR 的位置

1. 打开你的 GitHub 仓库页面
2. 点击顶部的 **Pull requests** 标签页
3. 你会看到 Devin 创建的新 PR，状态为 **Open**（打开的）

### PR 的内容

Devin 创建的 PR 包含：

#### PR 标题
通常格式为：`[Devin] <功能描述>`

#### PR 描述
Devin 会自动生成 PR 描述，包含：
- **Summary** — 改动概述
- **Changes** — 具体改了什么文件
- **Testing** — 如何验证这些改动
- **Notes** — 其他说明

如果你在仓库中配置了 PR 模板（`.github/PULL_REQUEST_TEMPLATE.md` 或 `.github/PULL_REQUEST_TEMPLATE/devin_pr_template.md`），Devin 会按照模板格式生成描述。

#### 文件变更
在 **Files changed** 标签页，你可以看到所有代码变更，包括：
- 新增的代码（绿色高亮）
- 删除的代码（红色高亮）
- 修改的代码

#### CI 状态
如果你的仓库配置了 CI/CD（如 GitHub Actions），Devin 的 PR 会自动触发 CI 检查。在 PR 页面底部可以看到检查状态：
- **绿色勾** — 所有检查通过
- **红色叉** — 有检查失败
- **黄色圆圈** — 检查正在进行中

### PR 页面的几个标签页（认清楚再操作）

打开 PR 详情页后，页面**上方有一排标签页**，新手最该认识这几个：

| 标签页 | 里面是什么 | 你什么时候点它 |
|--------|------------|----------------|
| **Conversation**（对话） | PR 描述、所有评论、CI 状态、Merge 按钮都在这 | 默认就在这页；想合并、看讨论时 |
| **Commits**（提交） | Devin 的每一次提交记录 | 想看 Devin 分了几步、每步改了啥 |
| **Checks**（检查） | CI 各项检查的详细日志 | CI 红了，想看哪一项失败、为什么 |
| **Files changed**（文件变更） | 所有代码改动的对比视图（diff） | review 代码、逐行评论、提建议 |

> 📍 记住两个最常用的：**Files changed** 用来看/评代码，**Conversation** 用来合并和讨论。

---

## 4.3 如何审查 Devin 的 PR（详细步骤）

### 第一步：打开 PR

1. 在 GitHub 仓库的 Pull requests 页面
2. 点击 Devin 创建的 PR 标题
3. 进入 PR 详情页

### 第二步：查看 PR 描述

先看 PR 描述，了解 Devin 做了什么。检查：
- 改动是否符合你的需求
- 是否有遗漏的步骤
- 测试是否充分

### 第三步：查看代码变更

1. 点击 **Files changed** 标签页
2. 逐个文件检查 Devin 的代码修改
3. 对于每个文件，你可以：
   - **查看完整文件** — 点击文件名旁边的 **View file** 按钮
   - **添加评论** — 鼠标悬停在某一行代码上，点击出现的 **+** 号，输入你的评论
   - **建议修改** — 在评论框中点击 **Suggestion** 按钮，可以直接建议代码修改

### 第四步：运行本地测试（可选但推荐）

如果你不放心，可以在本地测试 Devin 的代码：

```bash
# 1. 拉取 Devin 的分支
git fetch origin devin/1717750000-add-user-stats-api

# 2. 切换到 Devin 的分支
git checkout devin/1717750000-add-user-stats-api

# 3. 安装依赖（如果有新依赖）
npm install  # 或 pip install -r requirements.txt

# 4. 运行测试
npm test  # 或 pytest

# 5. 运行应用，手动测试
npm run dev

# 6. 测试完成后，切回你的主分支
git checkout main
```

### 第五步：提交 Review

在 **Files changed** 页面，点击右上角的 **Review changes** 按钮，你会看到三个选项：

#### 选项 1：Approve（批准）
- 选择 **Approve**
- 可以添加评论（可选）
- 点击 **Submit review**
- 含义：你认为这个 PR 可以合并

#### 选项 2：Request Changes（请求修改）
- 选择 **Request changes**
- 必须添加评论，说明需要修改什么
- 点击 **Submit review**
- 含义：你发现了一些问题，需要 Devin 修改

#### 选项 3：Comment（评论）
- 选择 **Comment**
- 添加你的评论
- 点击 **Submit review**
- 含义：你有一些想法，但不阻塞合并

---

## 4.4 处理 Devin 对 Review 的响应

### 如果你 Approve 了

1. PR 页面会出现 **Merge pull request** 按钮
2. 点击 **Merge pull request**
3. 选择合并方式：
   - **Create a merge commit** — 保留所有提交历史
   - **Squash and merge** — 将所有提交压缩为一个
   - **Rebase and merge** — 变基合并
4. 点击 **Confirm merge**
5. 合并完成后，Devin 的代码就进入了你的主分支
6. 合并成功后，页面上 **Merge** 按钮的位置会变成一个 **Delete branch**（删除分支）按钮：
   - 点它会删掉 Devin 那条 `devin/xxx` 临时分支（代码已经合并进 main 了，删掉分支不会丢代码）。
   - 这一步**纯粹是打扫卫生**，删不删都不影响功能，只是让分支列表更干净。建议点一下删掉。
   - 即使误删了，将来也能在 PR 页面点 **Restore branch** 恢复。

> ✅ 怎么确认真的合并成功了？PR 顶部状态会从绿色的 "Open" 变成**紫色的 "Merged"**，并显示 "Devin merged 1 commit into main"（或你设的目标分支）。看到紫色 Merged 就说明大功告成。

### 如果你 Request Changes 了

Devin 会自动响应你的 review 评论（前提是 session 还没有被归档）：

1. Devin 收到你的 review 评论
2. Devin 分析你的反馈
3. Devin 在同一个分支上修改代码
4. Devin push 新的 commit 到同一个 PR
5. PR 页面会显示新的 commit
6. 你可以再次 review

**注意**：如果 session 已经被归档（archived），Devin 不会自动响应。你需要：
- 创建一个新的 session
- 告诉 Devin 去处理那个 PR 的 review 评论
- 或者自己手动修改代码

### 如果 CI 检查失败了

Devin 通常会自动处理 CI 失败：

1. Devin 检测到 CI 失败
2. Devin 分析失败原因
3. Devin 修复问题并 push 新 commit
4. CI 重新运行

你也可以手动告诉 Devin 处理 CI 失败：
1. 在 PR 的评论中 @Devin
2. 说明 CI 失败了，让它修复
3. Devin 会处理

---

## 4.5 关于 main 分支 vs 其他分支的说明

### 情况 1：Devin 从 main 分支创建新分支（默认行为）

这是最常见的情况，也是推荐的做法：

```
main ──────●────────────────●────────── (合并 Devin 的 PR)
            \              /
             ●──●──●──●──●  ← Devin 的分支 (devin/xxx-feature)
```

**操作流程**：
1. Devin 创建新分支，修改代码，push，创建 PR
2. 你在 GitHub 上 review PR
3. 你 approve 并 merge
4. Devin 的代码进入 main 分支

### 情况 2：Devin 从其他分支（如 dev）创建新分支

如果你告诉 Devin 从 dev 分支开始工作：

```
dev ────────●────────────────●────────── (合并 Devin 的 PR)
            \              /
             ●──●──●──●──●  ← Devin 的分支
```

**操作流程**：和情况 1 一样，只是 PR 的目标分支是 dev 而不是 main。

### 情况 3：Devin 在 main 分支上直接工作（不推荐）

理论上，Devin 不会直接在 main 分支上工作。但如果你的仓库没有设置分支保护规则，Devin 可能会直接 push 到 main。

> 📖 如果你**故意**想让 Devin "直接推送、不开 PR"（个人项目常见），以及想搞清楚"直接推送到 main 和直接推送到 init 有什么区别"，请看 **[第九章：分支策略与直接推送](09-分支策略与直接推送.md)**。那一章把两种工作模式、两条分支的差异、以及如何安全撤销，都讲透了。

**强烈建议**：在 GitHub 上设置分支保护规则，防止任何人（包括 Devin）直接 push 到 main：

1. 打开 GitHub 仓库页面
2. 点击 **Settings**
3. 在左侧边栏点击 **Branches**
4. 在 **Branch protection rules** 下，点击 **Add rule**
5. 在 **Branch name pattern** 中输入 `main`
6. 勾选以下选项：
   - **Require a pull request before merging** — 要求通过 PR 合并
   - **Require status checks to pass before merging** — 要求 CI 通过
   - **Require branches to be up to date before merging** — 要求分支是最新的
7. 点击 **Create** 保存

这样，Devin（和所有人）都必须通过 PR 来合并代码到 main。

---

## 4.6 Devin Review — 更强大的 PR 审查工具

除了 GitHub 自带的 review 功能，Devin 还提供了一个专门的审查工具：**Devin Review**。

### 什么是 Devin Review？

Devin Review 是一个独立的代码审查平台，比 GitHub 自带的 diff 视图更强大：

- **智能 Diff 整理** — 按逻辑分组变更，而不是按文件名字母顺序
- **Bug 捕捉器** — 自动分析代码中的潜在问题
- **代码库感知聊天** — 可以问 Devin 关于 PR 的问题
- **直接从聊天修改代码** — 让 Devin 提出修复建议并直接应用

### 如何使用 Devin Review

#### 方式 1：通过 Devin Web 应用

1. 打开 https://app.devin.ai/review
2. 你会看到所有相关的 PR，按类别分组：
   - **Assigned to you** — 分配给你审查的
   - **Authored by you** — 你写的
   - **Review requested** — 请求你审查的
3. 点击任何一个 PR，进入 Devin Review 界面

#### 方式 2：URL 快捷方式

对于任何 GitHub PR 链接，把 `github.com` 替换为 `devinreview.com`：

```
GitHub 链接：
https://github.com/owner/repo/pull/123

Devin Review 链接：
https://devinreview.com/owner/repo/pull/123
```

#### 方式 3：CLI 命令

在本地仓库目录中运行：

```bash
npx devin-review https://github.com/owner/repo/pull/123
```

### Devin Review 的功能

#### Bug 捕捉器

Devin Review 会自动分析 PR 中的潜在问题：

- **严重 Bug（红色）** — 高置信度问题，需要立即处理
- **非严重 Bug（橙色）** — 应该检查的问题
- **Investigate 标记（橙色旗）** — 值得深入看看
- **Info 标记（灰色旗）** — 解释性说明，不需要行动

#### 代码库感知聊天

在 Devin Review 界面中，你可以：
1. 选中一段代码
2. 在聊天框中输入问题
3. Devin 会结合代码库的其他部分给出上下文相关的回答

#### 直接修改代码

1. 在聊天框中告诉 Devin 你想要的修改
2. Devin 会生成修复建议
3. 你审查修复建议
4. 点击应用，修改会作为 commit 直接提交到 PR 分支

### Auto-Fix（自动修复）

开启后，Devin Review 发现 bug 时会自动生成修复建议：

1. 在 Devin PR 的 Analysis 侧边栏中找到 **Auto-fix** 部分
2. 点击 **Enable auto-fix** 按钮
3. 之后 Devin Review 发现 bug 时，会自动在 diff 视图中显示修复建议

### Auto-Review（自动审查）

配置后，Devin 会自动审查所有 PR，无需手动触发：

1. 进入 **Settings** → **Preferences**
2. 找到 **Devin Review** 部分
3. 设置 **Review trigger** 为 **Auto-review**

触发时机：
- PR 被创建（非草稿）
- 有新 commit push 到 PR
- 草稿 PR 标记为 ready for review
- 你被添加为 reviewer 或 assignee

---

## 4.7 完整工作流示例

让我们用一个完整的例子来串联所有知识：

### 场景：让 Devin 给项目添加一个用户统计 API

#### 步骤 1：创建 Session

1. 打开 https://app.devin.ai
2. 点击 **New Session**
3. 选择 **Agent** 模式
4. 选择你的仓库
5. 选择默认的 **Devin** Agent

#### 步骤 2：输入任务

```
在 statsController.js 中创建一个新的 API 端点 /users/stats。

要求：
1. 返回 JSON 格式：{ user_count: number, avg_signup_age: number }
2. 使用 PostgreSQL 的 users 表
3. 参考现有的 /orders/stats 端点的代码结构
4. 在 StatsController.test.js 中添加测试用例
5. 确保通过 lint 检查和测试
```

#### 步骤 3：监控 Devin 工作

在右侧边栏的 Progress 标签页中，你可以看到：

1. Devin 分析代码库
2. Devin 制定计划
3. Devin 编辑 statsController.js
4. Devin 编辑 StatsController.test.js
5. Devin 运行 lint 检查
6. Devin 运行测试
7. Devin 创建分支 `devin/1717750000-add-user-stats`
8. Devin commit + push
9. Devin 创建 PR

#### 步骤 4：在 GitHub 上处理 PR

1. Devin 完成后，session 中会显示 PR 链接
2. 点击链接，在 GitHub 上打开 PR
3. 查看 PR 描述，确认改动符合预期
4. 点击 **Files changed** 查看代码变更
5. 检查每个文件的修改是否正确
6. 滚动到页面底部，查看 CI 状态：
   - 绿色勾 = 通过
   - 红色叉 = 失败（需要处理）

#### 步骤 5：审查代码

在 **Files changed** 页面：

1. 逐行检查 Devin 的代码
2. 如果有问题，在代码行上点击 **+** 号添加评论
3. 如果想建议修改，点击 **Suggestion** 按钮
4. 检查完所有文件后，点击右上角的 **Review changes**

#### 步骤 6：提交 Review

- 如果代码没问题：选择 **Approve** → 点击 **Submit review**
- 如果需要修改：选择 **Request changes** → 写清楚要改什么 → 点击 **Submit review**

#### 步骤 7：合并 PR（如果 Approve 了）

1. 点击 **Merge pull request** 按钮
2. 选择合并方式（推荐 **Squash and merge**，保持历史干净）
3. 点击 **Confirm merge**
4. 完成！代码已进入 main 分支

#### 步骤 8：处理 Request Changes（如果需要修改）

1. Devin 会自动收到你的 review 评论
2. Devin 在同一个分支上修改代码
3. Devin push 新的 commit
4. PR 页面显示新的 commit
5. 你再次 review → Approve → Merge

---

## 4.8 常见问题

### Q: Devin 的 PR 能自动合并吗？

可以。如果你的仓库配置了分支保护规则，你可以：
1. 在 PR 页面启用 **Auto-merge**
2. 当所有 CI 检查通过后，PR 会自动合并

### Q: 如果 Devin 的 PR 有冲突怎么办？

Devin 通常会自动处理冲突。如果冲突太大，你可以：
1. 在 PR 评论中告诉 Devin 有冲突
2. Devin 会尝试解决冲突
3. 或者你手动解决冲突，然后合并

### Q: Devin 能回复 PR 评论吗？

能。只要 session 还没有被归档，Devin 会自动响应 PR 评论。

### Q: Devin 能处理 code review 中的建议修改吗？

能。Devin 会：
1. 分析 review 中的评论
2. 在同一个分支上修改代码
3. Push 新的 commit
4. 回复评论说明做了什么修改

### Q: 如果我同时有多个 Devin PR 怎么办？

每个 PR 都是独立的分支，互不影响。你可以：
- 按优先级逐个审查
- 并行审查多个 PR
- 按顺序合并（如果有关联，注意合并顺序）

### Q: Devin 的 commit 会显示谁是作者？

默认情况下，commit 作者是 Devin bot。但你可以在设置中配置：
- **Devin only** — 所有 commit 作者都是 Devin
- **Co-authored** — commit 同时显示你和 Devin
- **User only** — commit 作者显示为你

设置位置：Settings → Profile → Commit authoring

---

## 4.9 小结

现在你已经完全理解了 Devin 的 Git 工作流程：

1. Devin 创建新分支，不会直接改 main
2. Devin 自动 commit + push + 创建 PR
3. 你在 GitHub 上 review PR（可以逐行检查代码）
4. 你可以 Approve（合并）、Request Changes（要求修改）、或 Comment（评论）
5. Devin 会自动响应 review 评论
6. 你最终决定是否合并

> 想让 Devin"直接推送、不开 PR"，或想弄清楚"在 main 上工作 vs 在 init 上工作"的区别？请看 **[第九章：分支策略与直接推送](09-分支策略与直接推送.md)**。

下一步：学习 Knowledge 与 Playbook，让 Devin 记住你的团队规范。
