# site-navigator

English | [简体中文](#简体中文)

OpenClaw-native web browsing and site navigation skill.

`site-navigator` is a strategy-first AgentSkill for web tasks in OpenClaw. It focuses on **how an agent should choose tools, navigate sites, verify sources, and present stable conclusions** rather than merely exposing raw browser automation.

It is designed for tasks such as:
- visiting websites directly
- navigating within platforms instead of relying on generic search snippets
- inspecting rendered UI with OpenClaw browser tools
- handling dynamic or login-gated pages
- distinguishing discovery surfaces from real target pages
- keeping conclusions stable before reporting them to the user

## What it can do

### 1. Tool routing for web tasks
It helps the agent decide between:
- `web_fetch`
- `browser`
- `web_search`
- `sessions_spawn`

based on the actual task shape, source quality, runtime constraints, and whether rendered state matters.

### 2. Browser-first navigation for complex platforms
It is especially useful for platforms where the real target is often behind UI navigation rather than simple page fetching, such as:
- WeChat public articles
- Xiaohongshu
- Zhihu
- GitHub

### 3. Stable-first reporting
It teaches the agent to:
- avoid summarizing from snippets too early
- avoid reporting from discovery/search surfaces as if they were the final target
- separate stable conclusions from progressive enhancement

### 4. Source verification
It introduces a source hierarchy so the agent prefers:
1. first-party sources
2. structured first-party-adjacent evidence
3. reputable secondary sources
4. discovery-only surfaces for navigation, not final verification

### 5. Failure recovery
It includes recovery patterns for cases like:
- incomplete `web_fetch`
- stale browser targets
- login walls
- runtime restrictions
- ambiguous page state

## Technical design

This project is **not** a replacement browser runtime. It is a **strategy layer** for OpenClaw.

### Core idea
Instead of building a parallel browser stack, `site-navigator` is designed around OpenClaw native tools and adds:
- routing logic
- evidence awareness
- platform patterns
- output contracts
- failure recovery rules

### Technical layers

#### 1. Skill layer
- `SKILL.md`
- defines when the skill should trigger
- defines high-level routing logic
- encodes stable-first browsing principles

#### 2. Browser playbook layer
- `references/openclaw-browser-playbook.md`
- explains how to use OpenClaw browser tools safely and effectively
- emphasizes snapshot-first, aria refs, and stable page-state handling

#### 3. Evidence layer
- `references/source-hierarchy.md`
- `references/output-contract.md`
- defines what counts as strong enough evidence and how results should be reported

#### 4. Task-shape layer
- `references/task-patterns.md`
- maps common web-task shapes to default execution paths

#### 5. Recovery layer
- `references/failure-recovery.md`
- describes how to switch strategy when a method fails

#### 6. Site-pattern layer
- `references/site-patterns/*.md`
- accumulates domain-specific knowledge for repeated targets like GitHub, Zhihu, Xiaohongshu, and WeChat

## Repository structure

- `SKILL.md` — main skill definition
- `references/openclaw-browser-playbook.md` — browser operating patterns
- `references/output-contract.md` — how to present browsing results
- `references/source-hierarchy.md` — evidence strength model
- `references/task-patterns.md` — common web task shapes
- `references/failure-recovery.md` — fallback and route-changing guidance
- `references/examples.md` — concrete usage examples
- `references/site-patterns/*.md` — domain-specific notes
- `TESTING.md` — test and iteration notes
- `RELEASE_NOTES.md` — release-oriented notes

## Current status

This repository is in iterative alpha/beta-style development for real OpenClaw usage.
The goal is not to finalize theory first, but to improve through real tasks and repeated refinement.

## Roadmap

- Validate against more real OpenClaw browsing tasks
- Expand site patterns based on repeated use
- Refine trigger boundaries and reporting rules
- Prepare for broader public iteration

---

# 简体中文

OpenClaw 原生网页浏览与站点导航技能。

`site-navigator` 是一个 **策略优先（strategy-first）** 的 OpenClaw AgentSkill。它关注的不是“再造一个浏览器自动化工具”，而是：

- agent 应该如何选工具
- 应该怎样在网站中导航
- 怎样判断证据强弱
- 怎样避免过早下结论
- 怎样把最终结果稳定地呈现给用户

它适合处理这类任务：
- 直接访问网页
- 在平台内部导航，而不是只停留在搜索摘要
- 使用 OpenClaw browser 工具检查渲染后的页面
- 处理动态页面、登录态页面
- 区分 discovery surface（发现页）和 real target page（真实目标页）
- 在对外输出前先让结论稳定下来

## 这个项目能做什么

### 1）网页任务的工具路由
帮助 agent 在这些工具之间做更合理的选择：
- `web_fetch`
- `browser`
- `web_search`
- `sessions_spawn`

选择依据不是单一的“页面类型”，而是综合考虑：
- 任务形态
- 证据强度
- 运行时限制
- 是否依赖真实渲染状态

### 2）复杂平台的 browser-first 导航
这个 skill 特别适合处理这类平台：
- 微信公众号
- 小红书
- 知乎
- GitHub

这些平台的真实目标内容，很多时候并不在搜索摘要里，而在：
- 站内搜索结果之后
- 某个卡片点击之后
- 某个真实页面打开之后
- 某个登录态页面里

### 3）稳定优先（stable-first）的结果输出
这个 skill 强调：
- 不要刚看到一点搜索结果就下结论
- 不要把 discovery/search surface 当成真实目标页
- 主结论先稳定，再补截图、链接和额外信息

### 4）证据分级与来源判断
项目内置了一套 source hierarchy（来源层级）思想，优先级大致是：
1. 一手来源
2. 接近一手的结构化证据
3. 可信二手来源
4. 仅用于发现下一步线索的搜索/聚合页面

### 5）失败恢复策略
项目已经开始沉淀真实恢复策略，例如：
- `web_fetch` 提取不完整怎么办
- browser target 丢失怎么办
- 登录墙怎么办
- runtime 对某些工具有限制怎么办
- 页面状态不明确时怎么办

## 技术实现思路

这个项目**不是一个新的浏览器运行时**，而是一个 **OpenClaw 策略层（strategy layer）**。

### 核心思想
不是在 OpenClaw 外面再造一套平行浏览器系统，
而是基于 OpenClaw 已有能力，补上：
- 路由逻辑
- 证据意识
- 平台模式
- 输出契约
- 失败恢复规则

### 技术结构分层

#### 1）Skill 主体层
- `SKILL.md`
- 定义触发场景
- 定义高层工具路由逻辑
- 定义 stable-first 浏览原则

#### 2）Browser playbook 层
- `references/openclaw-browser-playbook.md`
- 说明怎样更稳定地使用 OpenClaw browser 工具
- 强调 snapshot-first、aria refs、稳定页面状态判断

#### 3）证据层
- `references/source-hierarchy.md`
- `references/output-contract.md`
- 定义什么算足够强的证据，以及结果应该怎样输出

#### 4）任务模式层
- `references/task-patterns.md`
- 把常见网页任务抽象成默认执行模式

#### 5）恢复层
- `references/failure-recovery.md`
- 说明方法失败后应该怎样换路，而不是机械重试

#### 6）站点模式层
- `references/site-patterns/*.md`
- 累积 GitHub、知乎、小红书、微信公众号等平台的已验证经验

## 仓库结构

- `SKILL.md` — 主技能定义
- `references/openclaw-browser-playbook.md` — 浏览器使用模式
- `references/output-contract.md` — 浏览结果的输出规范
- `references/source-hierarchy.md` — 证据强弱模型
- `references/task-patterns.md` — 常见网页任务模式
- `references/failure-recovery.md` — 失败恢复与换路策略
- `references/examples.md` — 典型示例
- `references/site-patterns/*.md` — 站点经验
- `TESTING.md` — 测试与迭代记录
- `RELEASE_NOTES.md` — 发布备注

## 当前状态

这个仓库目前处于面向真实 OpenClaw 使用场景的 alpha/beta 式迭代阶段。
目标不是先把理论写满，而是通过真实任务不断试错、修正、打磨。

## Roadmap / 计划

- 用更多真实 OpenClaw 网页任务继续验证
- 基于重复使用扩展 site patterns
- 继续收敛触发边界和输出规则
- 为更广泛公开迭代做准备
