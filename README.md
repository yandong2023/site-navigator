# site-navigator

English | [简体中文](#简体中文)

OpenClaw-native browsing skill for hard-to-access web content.

`site-navigator` is an OpenClaw AgentSkill focused on a very practical pain point:

> many real-world links are not easy to read or verify with ordinary search/fetch flows.

In practice, users often want to send a link and have the agent **open the real page, read the actual content, navigate inside the site if needed, and continue learning how to handle that platform better over time**.

This is especially important for sites like:
- Xiaohongshu
- Zhihu
- WeChat public articles
- Bilibili
- GitHub
- other dynamic, platform-style sites where “just fetch the page” is often not enough

## Why this skill exists

A common pain point in real OpenClaw usage is:
- the user already has a real link
- the content exists on the real platform
- but generic search/fetch paths are incomplete, blocked, or too weak
- the agent cannot reliably reach the actual target page and reason from it

`site-navigator` exists to improve exactly that.

Its goal is simple:

> if the user gives a real link, the agent should be much better at opening it, understanding whether it is a discovery surface or the real target page, reading the actual content, and interacting with the site when needed.

That means the skill is not just about “web access” in the abstract.
It is about **practical access to hard-to-handle websites and the gradual accumulation of platform-specific operating knowledge**.

## What problem it solves

This skill is designed around these real problems:

### 1. Link-first access to real content
If the user sends:
- a WeChat article link
- a Zhihu column/article link
- a Xiaohongshu page link
- a GitHub repo/release/issues page
- a Bilibili page link

then the skill is meant to help the agent do more than just search around it.
It should help the agent:
- open the actual page
- determine whether it is readable now
- distinguish between discovery surfaces and real target pages
- extract the useful content or navigate further if needed

### 2. Better handling of Chinese content platforms
Many Chinese content platforms are not well served by naive search/fetch behavior.
This skill is specifically meant to improve OpenClaw’s practical handling of:
- Xiaohongshu
- Zhihu
- WeChat public content
- Bilibili

### 3. Browser-backed access when static extraction is weak
When a static read path is weak or incomplete, the skill helps the agent move to a browser-backed approach.
That makes it possible to:
- inspect rendered UI
- follow the real navigation path
- verify what the page actually shows now
- work from first-party pages instead of vague snippets

### 4. Capability growth over time
This project is also about **compounding capability**.
Each time the agent successfully handles a platform better, that knowledge can be refined into:
- site patterns
- routing guidance
- recovery rules
- output rules

So the skill is meant to get better with repeated real-world use.

## What it can do

### Link-first site access
Given a real link, it helps the agent:
- open it directly
- check whether it is really reachable
- determine whether it is the real target page
- read the visible content or continue navigation

### Platform-aware browsing
It adds platform-sensitive guidance for sites like:
- WeChat
- Xiaohongshu
- Zhihu
- GitHub

### Stable-first conclusions
It teaches the agent not to summarize too early from:
- search snippets
- discovery surfaces
- landing pages
- incomplete renders

### Source-aware verification
It teaches the agent to prefer:
- first-party pages
- official rendered UI state
- stronger source chains over secondary summaries

### Recovery when the first method fails
It includes rules for switching methods when:
- fetch is incomplete
- runtime blocks a path
- browser targets go stale
- login is required
- the current page is not the real target yet

## Technical approach

This project does **not** try to replace OpenClaw’s native tools.
Instead, it works as a **strategy layer** on top of them.

It is built around the idea that access to difficult websites is not just a tooling problem. It is also a problem of:
- routing
- target-page judgment
- source judgment
- recovery
- platform memory

### Core technical components

#### 1. Skill layer
`SKILL.md`
- when the skill should trigger
- how to choose an execution path
- when to treat a page as stable enough to summarize

#### 2. Browser playbook layer
`references/openclaw-browser-playbook.md`
- how to use OpenClaw browser flows safely and effectively
- snapshot-first patterns
- stable page-state handling
- runtime-aware routing

#### 3. Evidence and reporting layer
- `references/source-hierarchy.md`
- `references/output-contract.md`

These define:
- which evidence is strong enough
- how to avoid false certainty
- how to report findings clearly

#### 4. Task-shape layer
`references/task-patterns.md`
- maps common task shapes to browsing strategies
- includes the distinction between discovery surfaces and real target pages

#### 5. Failure-recovery layer
`references/failure-recovery.md`
- teaches the agent how to change route when the first attempt is weak or blocked

#### 6. Site-pattern layer
`references/site-patterns/*.md`
- accumulates repeated knowledge about specific platforms
- this is where long-term practical capability grows

## Why this matters for OpenClaw

This skill is meant to close a real gap:

> before this, OpenClaw was not strong enough at reliably handling some real-world platform links and dynamic content pages that users actually care about.

If this skill works well, OpenClaw becomes much more useful for:
- opening user-sent links directly
- reading Chinese platform content
- navigating difficult platform pages
- verifying real content instead of relying on weak indirect signals
- gradually improving through repeated platform-specific experience


## Another key benefit: less dependence on paid search APIs

A second pain point behind this project is over-dependence on paid search APIs such as Brave Search for tasks that do not actually need generic search as the primary path.

For many real tasks, the user already provides:
- a real URL
- a known platform
- or a concrete target that is better reached through direct navigation

In those cases, forcing the workflow through a paid search layer can add:
- unnecessary API cost
- weaker source quality
- more indirection
- more chances to stop at snippets instead of the real target page

`site-navigator` is designed to reduce that dependency by preferring:
- direct URLs
- first-party pages
- browser-backed site navigation
- platform-aware routing

This is not only about saving money. It is also about choosing a more direct and reliable path to the real content.

## Installation

This repository is currently structured as an OpenClaw-style skill project.

### Current installation approach

If you are testing locally, clone the repository into a skills directory that your OpenClaw workflow can read from:

```bash
git clone https://github.com/yandong2023/site-navigator.git
```

Then make sure the skill files are available to the OpenClaw environment where you want to use them.

At minimum, the important files are:
- `SKILL.md`
- `references/`

### Recommended usage model

Use this skill as a strategy layer when tasks involve:
- user-sent links
- hard-to-access content platforms
- first-party verification
- browser-backed navigation
- reducing unnecessary paid-search dependence

### Runtime note

This skill works best in an OpenClaw environment that already has:
- `browser` available for rendered-page access
- `web_fetch` available for lightweight reading when possible
- the ability to reuse browser state when login-dependent access matters

## Quick usage examples

Example tasks this skill is meant to help with:
- “Read this WeChat article and summarize the real content.”
- “Open this Zhihu link and tell me whether it is the actual article page.”
- “Go to this Xiaohongshu page and verify whether this is the real account/post.”
- “Inspect this GitHub repository page directly instead of relying on search snippets.”
- “Use direct navigation first so we do not waste paid search API calls unless discovery is truly necessary.”


## Quick Start

### Minimal local test

```bash
git clone https://github.com/yandong2023/site-navigator.git
cd site-navigator
```

Then make the skill available to your OpenClaw workflow or skills directory.

At minimum, keep:
- `SKILL.md`
- `references/`

### What to try first

Try it with a real link that used to be hard to handle:
- a WeChat article link
- a Zhihu column/article link
- a Xiaohongshu page link
- a Bilibili page link
- a GitHub repo/release/issues page link

The intended improvement is that the agent should be more willing to:
- open the real page directly
- verify whether it is the real target page
- navigate further with browser-backed flows if needed
- avoid wasting paid search calls unless discovery is truly necessary

## Before / After

### Before
A typical workflow might be:
- start from generic search
- depend on paid search APIs too early
- stop at snippets or discovery surfaces
- fail to reach the real target page reliably

### After
With `site-navigator`, the intended workflow becomes:
- start from the real link when available
- prefer first-party pages and direct navigation
- switch to browser-backed access when static reading is weak
- summarize only after the real target page is reached or ruled out

## Minimal example prompts

- “Read this WeChat article link and summarize the real content.”
- “Open this Zhihu link and tell me whether it is the actual article page.”
- “Go to this Xiaohongshu page and verify whether this is the real account.”
- “Open this Bilibili page and tell me what the current visible page is.”
- “Inspect this GitHub repo page directly instead of relying on search snippets.”

## Repository structure

- `SKILL.md` — main skill definition
- `references/openclaw-browser-playbook.md` — browser operating patterns
- `references/output-contract.md` — how browsing results should be reported
- `references/source-hierarchy.md` — evidence strength model
- `references/task-patterns.md` — common browsing task shapes
- `references/failure-recovery.md` — fallback and route-changing guidance
- `references/examples.md` — concrete examples
- `references/site-patterns/*.md` — site-specific notes
- `TESTING.md` — real testing notes
- `RELEASE_NOTES.md` — release-oriented notes

## Current status

Iterative early-stage development for real OpenClaw use.
The project is being shaped by real browsing pain points, not just theory.

---

# 简体中文

OpenClaw 原生的“困难网页访问 / 平台导航”技能。

`site-navigator` 这个项目其实是围绕一个非常真实的痛点来的：

> 很多真实世界里的链接，普通搜索 / 普通抓取根本不够用。

用户真正想要的是：

> 给你一个真实链接，你就能把这个页面真正打开、读到内容、必要时继续在站内导航，而且随着使用次数增加，对这些平台越来越熟。

这件事在这些网站上尤其重要：
- 小红书
- 知乎
- 微信公众号文章
- B站
- GitHub
- 以及其他动态平台型网站

## 为什么会做这个 skill

在真实 OpenClaw 使用里，一个很常见的问题是：
- 用户已经给了真实链接
- 内容明明就在真实平台上
- 但普通 search/fetch 路径不是提取不完整，就是拿不到真正页面状态
- agent 很难稳定地到达“真实目标页”，更别说基于它做判断

`site-navigator` 要补的，就是这一块。

它的目标很简单：

> 当用户给出一个真实链接时，agent 应该更擅长把它打开、判断这是不是 discovery surface（发现页）还是 real target page（真实目标页）、读到真实内容、必要时继续在站内操作。

所以它不是抽象意义上的“web access”。
它更像是：

## **面向困难网站的实用访问能力 + 持续积累的平台操作经验**

## 它要解决的真实问题

### 1）链接优先（link-first）的真实内容访问
如果用户发来的是：
- 一篇公众号文章链接
- 一篇知乎专栏链接
- 一个小红书页面链接
- 一个 GitHub repo / release / issue 链接
- 一个 B站页面链接

这个 skill 的目标不是只在外面搜一圈，
而是让 agent 更有能力：
- 直接打开真实页面
- 判断它现在能不能读
- 判断它到底是不是“真实目标页”
- 读取内容，或者继续在站内导航

### 2）更好地处理中文内容平台
很多中文平台并不适合靠朴素的 search/fetch 来解决。
这个 skill 就是专门针对这些平台的实际可访问性问题来设计的：
- 小红书
- 知乎
- 微信公众号文章
- B站

### 3）当静态提取不够时，切换到 browser-backed 路径
如果静态提取不完整，或者根本拿不到用户真正关心的页面状态，
这个 skill 会引导 agent 切换到 browser-backed 的路径。

这样 agent 才能：
- 看渲染后的 UI
- 沿着真实页面路径继续点进去
- 确认页面现在到底显示了什么
- 基于一手页面，而不是摘要碎片做判断

### 4）能力会随着使用不断提升
这个项目另一个核心点是：

## **能力是可以积累的**

每次 agent 成功处理某个平台，都可以把经验沉淀成：
- site patterns
- routing guidance
- failure recovery rules
- output rules

所以这个 skill 不是“一次性写完”的，
而是会随着真实任务反复使用，变得越来越强。

## 它有哪些能力

### 链接优先的站点访问能力
给一个真实链接时，它会帮助 agent：
- 直接打开
- 判断是否真的可访问
- 判断是否已经到达真实目标页
- 读取当前可见内容，或者继续导航

### 平台感知的浏览能力
它会给这些平台提供更有针对性的处理方式：
- 微信公众号
- 小红书
- 知乎
- GitHub
- 后续也可以扩展到 B站等平台

### 稳定优先（stable-first）的结论能力
它会教 agent 避免从这些地方过早下结论：
- 搜索摘要
- 发现页 / 搜索页
- landing page
- 不完整渲染页

### 来源意识 / 一手证据优先
它会让 agent 尽量优先：
- 一手页面
- 官方页面的真实渲染状态
- 更强的来源链路
而不是依赖二手转述或弱信号

### 方法失败后的换路能力
它已经开始沉淀这类恢复规则：
- `web_fetch` 不完整怎么办
- runtime 限制某种方法怎么办
- browser target 丢失怎么办
- 需要登录怎么办
- 当前页面还不是目标页怎么办

## 技术实现思路

这个项目**不是重新造一个浏览器运行时**，
而是一个建立在 OpenClaw 原生能力之上的 **策略层（strategy layer）**。

它的核心判断是：

> 困难网站的访问问题，不只是工具问题，更是路由问题、目标页判断问题、来源判断问题、恢复问题，以及平台记忆问题。

### 技术结构分层

#### 1）Skill 主体层
`SKILL.md`
负责定义：
- 什么任务触发这个 skill
- 怎么选择执行路径
- 什么时候页面状态足够稳定，可以开始总结

#### 2）Browser playbook 层
`references/openclaw-browser-playbook.md`
负责说明：
- 怎样更稳定地使用 OpenClaw 的 browser 能力
- snapshot-first 的操作方式
- stable page-state handling
- runtime-aware routing

#### 3）证据与输出层
- `references/source-hierarchy.md`
- `references/output-contract.md`

这一层定义：
- 什么样的证据足够强
- 怎样避免假确定性
- 结果应该怎么输出给用户

#### 4）任务模式层
`references/task-patterns.md`
负责把常见任务抽象成执行模式，
包括：
- discovery surface 和 real target page 的区分

#### 5）失败恢复层
`references/failure-recovery.md`
负责告诉 agent：
- 第一种方法失败之后怎么换路
- 什么时候该切 browser
- 什么时候该承认当前还不能稳定下结论

#### 6）站点模式层
`references/site-patterns/*.md`
这一层是长期最有价值的部分之一：
- 把知乎、小红书、GitHub、微信公众号等平台的经验沉淀下来
- 让能力随着真实使用不断增长

## 为什么这对 OpenClaw 很重要

这个 skill 的意义在于补一个真实缺口：

> 之前 OpenClaw 对某些真实世界平台链接和动态内容页的处理，还不够强。

如果这个 skill 做得好，OpenClaw 会明显更适合：
- 直接打开用户发来的链接
- 读取中文平台内容
- 进入困难平台的真实页面
- 基于真实内容做验证，而不是停留在弱信号层
- 通过重复任务不断提升平台处理能力


## 另一个重要价值：减少对付费搜索 API 的依赖

这个项目背后还有一个很现实的痛点：
很多原本不该优先走通用搜索的任务，过去却很容易默认依赖 Brave Search 这类付费搜索 API。

但很多真实任务里，用户其实已经给了：
- 真实链接
- 明确平台
- 或者非常具体的目标

这时候如果还强行先走付费搜索层，往往会带来：
- 额外 API 成本
- 更弱的来源质量
- 更多中间跳转
- 更容易停留在搜索摘要，而不是真实目标页

`site-navigator` 的一个核心价值，就是尽量把这些任务改造成：
- direct URL
- 一手页面优先
- browser-backed 站内导航
- 平台感知的路由

所以它不只是为了省钱，
也是为了让 agent 走一条**更直接、更可靠、更接近真实内容**的路径。

## 安装方式

目前这个仓库已经按 OpenClaw skill 项目的结构组织好了。

### 当前安装方式

如果你要本地测试，可以先把仓库 clone 下来：

```bash
git clone https://github.com/yandong2023/site-navigator.git
```

然后把这个 skill 放到你的 OpenClaw 可读取的 skills 路径中，或者在你自己的 OpenClaw workflow 中直接引用它。

最关键的文件是：
- `SKILL.md`
- `references/`

### 推荐使用方式

这个 skill 最适合放在这些任务上：
- 用户直接发链接
- 难访问的平台内容
- 一手页面验证
- 依赖 browser 的站内导航
- 希望减少 Brave API 这类付费搜索依赖的任务

### 运行环境说明

这个 skill 最适合运行在已经具备这些能力的 OpenClaw 环境里：
- 有 `browser`，能访问渲染后的真实页面
- 有 `web_fetch`，能在轻量阅读时快速提取正文
- 必要时能复用浏览器状态，处理登录态页面

## 快速使用示例

这个 skill 适合帮助 agent 处理这类任务：
- “读一下这篇公众号文章，给我总结真实内容。”
- “打开这个知乎链接，告诉我这是不是文章真实页。”
- “去这个小红书页面看一下，确认是不是目标账号/帖子。”
- “直接看这个 GitHub repo 页面，不要只依赖搜索摘要。”
- “优先用 direct navigation，避免不必要地消耗 Brave API。”


## Quick Start / 快速开始

### 最小本地测试方式

```bash
git clone https://github.com/yandong2023/site-navigator.git
cd site-navigator
```

然后把这个 skill 放到你的 OpenClaw skills 路径中，或者让你的 OpenClaw workflow 能读取到它。

最关键的文件至少包括：
- `SKILL.md`
- `references/`

### 最适合先拿什么测试

建议先拿这些“过去比较难处理”的真实链接来试：
- 一篇公众号文章链接
- 一篇知乎专栏 / 文章链接
- 一个小红书页面链接
- 一个 B 站页面链接
- 一个 GitHub repo / release / issue 页面链接

这个 skill 想带来的改进是：
- 更愿意直接打开真实页面
- 更会判断当前是不是目标页
- 静态读取不够时，能切到 browser-backed 路径继续走
- 不是一上来就消耗付费搜索 API

## Before / After

### Before
以前很多流程容易变成：
- 先走通用搜索
- 很早就依赖付费搜索 API
- 停留在摘要或发现页
- 迟迟到不了真实目标页

### After
有了 `site-navigator` 之后，理想路径会变成：
- 有真实链接时先直达真实页面
- 优先一手页面和站内导航
- 静态读取不够时切到 browser-backed 路径
- 到达真实目标页后再总结，或者明确说明还没到达

## 最小示例任务

- “读一下这篇公众号文章链接，给我总结真实内容。”
- “打开这个知乎链接，告诉我这是不是文章真实页。”
- “去这个小红书页面看一下，确认是不是目标账号。”
- “打开这个 B 站页面，告诉我当前真实可见页面是什么。”
- “直接看这个 GitHub repo 页面，不要只依赖搜索摘要。”

## 仓库结构

- `SKILL.md` — 主 skill 定义
- `references/openclaw-browser-playbook.md` — browser 使用模式
- `references/output-contract.md` — 浏览结果输出规范
- `references/source-hierarchy.md` — 证据强弱模型
- `references/task-patterns.md` — 常见网页任务模式
- `references/failure-recovery.md` — 失败恢复 / 换路策略
- `references/examples.md` — 典型案例
- `references/site-patterns/*.md` — 站点经验
- `TESTING.md` — 真实测试记录
- `RELEASE_NOTES.md` — 发布说明

## 当前状态

目前是一个面向真实 OpenClaw 使用的早期迭代项目。
它的方向不是先把理论写满，而是围绕真实网页访问痛点，一边用、一边修、一边积累能力。
