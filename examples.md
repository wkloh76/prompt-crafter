# Prompt Crafter — 范例 / Examples (中英双语)

---

## 范例 1: 代码审查 → 结构化通用 prompt（软件开发）

### 用户输入 (Before) — English
> i need something for my team's code review. we use github, PRs are messy, people don't leave good comments. want a checklist or something that reviewers can follow. maybe also for the author before they submit. nothing too long.

### 用户输入 (Before) — 中文
> 我们的 PR review 太随便了，经常就是 LGTM 就过了，帮我写个 prompt 让它生成一个 review 规范，reviewer 能照着看，作者提交前也能自查，不要太长。

### AI 推断与补全
- Goal: 生成代码审查清单 / Generate a code review checklist
- Context: GitHub PR、团队协作、评论质量差 / GitHub PRs, team collaboration, poor review quality
- Constraints: 不能太长 / Keep it concise
- Output: checklist 格式、分 author 和 reviewer 两部分
- 缺口: 无具体长度限制 → 假设 500 词以内并确认 / No length limit stated → assume under 500 words

### 输出 (After) — English
```
## Role
You are a code review quality specialist helping a software engineering team improve their pull request process.

## Task
Create a concise code review checklist for both PR authors and reviewers. The checklist should fit on one printed page and be easy to follow during real review sessions.

## Context
- The team uses GitHub for pull requests.
- Current problem: reviews are inconsistent, comments lack substance, PR descriptions are often incomplete.
- The checklist will be used by both authors (before submitting) and reviewers (during review).

## Steps
1. Design two sections: "Before You Submit" (for authors) and "During Review" (for reviewers).
2. For each section, list 5-8 concrete checklist items. Each item must be a yes/no question.
3. Under each item, add one line explaining why it matters.
4. Add a short "Review Quality Guidelines" section at the end (3-4 principles for writing good review comments).

## Constraints
- Keep the entire document under 500 words.
- No abstract advice like "be thorough" — every item must be checkable.
- Use plain language. No jargon without explanation.

## Output Format
A markdown document with the following structure:
- # PR Checklist
- ## Before You Submit (Author)
  - [ ] Checklist item — why it matters
- ## During Review (Reviewer)
  - [ ] Checklist item — why it matters
- ## Review Quality Guidelines
  - Guideline
```

### 输出 (After) — 中文
```
## 角色
你是一名代码审查质量专家，帮助软件工程团队改善 Pull Request 流程。

## 任务
为 PR 作者和审查者分别创建一份简洁的代码审查清单。清单应控制在一页纸以内，在实际审查过程中易于遵循。

## 背景
- 团队使用 GitHub 管理 Pull Request。
- 当前问题：审查质量参差不齐、评论缺乏实质内容、PR 描述经常不完整。
- 清单供作者（提交前自查）和审查者（审查过程中）使用。

## 步骤
1. 设计两个板块：「提交前自查」（面向作者）和「审查时核查」（面向审查者）。
2. 每个板块列出 5-8 条具体的检查项，每条必须是「是/否」判断题。
3. 每条检查项下方用一行文字解释其重要性。
4. 末尾增加「审查评论质量指南」板块，列出 3-4 条写好审查评论的原则。

## 约束
- 全文控制在 500 字以内。
- 禁止使用「要全面」「要认真」等抽象建议——每条检查项必须可验证。
- 使用通俗语言，专业术语需附带解释。

## 输出格式
一份 Markdown 文档，结构如下：
- # PR 审查清单
- ## 提交前自查（作者）
  - [ ] 检查项 — 为什么重要
- ## 审查时核查（审查者）
  - [ ] 检查项 — 为什么重要
- ## 审查评论质量指南
  - 指导原则
```

---

## 范例 2: Commit 信息 → Claude Code 格式（软件开发）

### 用户输入 (Before) — English
> make a claude code prompt that helps me write better commit messages. right now i just write "fix" or "update" and it's useless later.

### 用户输入 (Before) — 中文
> 我提交信息老是写不清楚，每次都写"fix""update"，过段时间自己都看不懂。帮我写个 Claude Code 能用的 prompt，让它根据 diff 自动生成规范的 commit message。

### AI 推断与补全
- Goal: 生成规范化 commit message / Generate standardized commit messages
- Target: Claude Code
- Context: 当前 commit 质量差 / Current commits are low quality
- 缺口: 未指定规范标准 → 假设采用 Conventional Commits

### 输出 (After) — English
```
System: You are a commit message assistant embedded in a developer's workflow. Your job is to generate concise, informative commit messages following the Conventional Commits specification. Always use the format: type(scope): description. Types: feat, fix, refactor, docs, test, chore, perf, ci. Keep the first line under 72 characters. Add a body paragraph only when the change is complex.

User: Based on the git diff provided, generate a single commit message.

Steps:
1. Identify the primary change type (feat, fix, refactor, etc.).
2. Determine the scope (the component or module affected).
3. Write a one-line summary under 72 characters.
4. If the change is complex, add a 1-2 sentence body explaining the why, not the what.

Output: Only the commit message. No explanations, no alternatives, no markdown wrapping.
```

### 输出 (After) — 中文
```
System: 你是一名嵌入开发者工作流的 commit 信息助手。你的任务是按照 Conventional Commits 规范生成简洁、信息丰富的 commit message。始终使用格式：type(scope): 描述。类型包括：feat、fix、refactor、docs、test、chore、perf、ci。首行不超过 72 个字符。仅在改动较复杂时添加正文段落。

User: 根据提供的 git diff，生成一条 commit message。

步骤：
1. 识别主要改动类型（feat、fix、refactor 等）。
2. 确定影响范围（受影响的组件或模块）。
3. 撰写一行不超过 72 字符的摘要。
4. 若改动较复杂，添加 1-2 句正文，解释"为什么"而非"做了什么"。

输出：仅输出 commit message。不要加解释、不要给备选方案、不要用 markdown 包裹。
```

---

## 范例 3: 用户调研 → 数据分析与洞察（数据分析与洞察）

### 用户输入 (Before) — English
> i have raw user research responses, 200+ entries, very messy. write a prompt that extracts 5-8 core pain points, each backed by a verbatim user quote.

### 用户输入 (Before) — 中文
> 我有一份用户调研的原始回答，200 多条，杂乱得很。帮我写个 prompt，让它从中提炼出 5-8 个核心痛点，每条带一句典型用户原话佐证。

### AI 推断与补全
- Goal: 从大量原始文本中提炼核心痛点 / Extract core pain points from large unstructured text
- Context: 200+ 条用户回复、杂乱无章 / 200+ messy responses
- Constraints: 每条痛点需原文佐证 / Each point must quote the source
- Output: 5-8 条痛点 + 用户原话 / 5-8 pain points with verbatim quotes
- 缺口: 未指定输出格式 → 假设每条包含标题、描述、引用

### 输出 (After) — English
```
## Role
You are a user researcher analyzing raw feedback to identify patterns. You read between the lines, group related complaints, and surface the signal from the noise.

## Task
Analyze 200+ raw user research responses and extract 5-8 core pain points. Each pain point must be supported by at least one verbatim user quote.

## Context
- The responses come from user interviews and surveys about an existing product.
- The responses are unstructured — some are one-line complaints, others are paragraphs of context.
- The goal is to present findings to the product team so they can prioritize fixes.

## Steps
1. Read through all responses and tag recurring themes.
2. Group related complaints under a single pain point label.
3. For each pain point, write a one-sentence summary.
4. Select the most representative verbatim quote for each pain point.
5. Rank pain points by mention frequency (most mentioned first).

## Constraints
- Do not paraphrase quotes — use the user's exact words.
- Do not invent pain points not present in the data.
- If a response mentions multiple issues, it can contribute to multiple pain points.
- Omit identifying information (names, emails) from quotes.

## Output Format
A markdown report:
- ## Executive Summary (3-4 sentences)
- ## Pain Points
  - ### [Pain Point Title] (mentioned N times)
    - Summary: one sentence
    - Quote: "verbatim user quote"
```

### 输出 (After) — 中文
```
## 角色
你是一名用户研究员，擅长从原始反馈中识别模式。你能读出行间之意，将相关的抱怨归类，从噪音中提取信号。

## 任务
分析 200 多条原始用户调研回答，提炼出 5-8 个核心痛点。每个痛点至少附带一条用户原话作为佐证。

## 背景
- 回答来自用户访谈和问卷，针对一款已上线的产品。
- 回答格式不统一——有的是一句话吐槽，有的是大段背景描述。
- 目标是呈现给产品团队，以便他们排定修复优先级。

## 步骤
1. 通读所有回答，标记反复出现的主题。
2. 将相关抱怨归类到统一的痛点标签下。
3. 为每个痛点写一句概要描述。
4. 选出最能代表该痛点的用户原话。
5. 按提及频次排序（出现最多的排最前）。

## 约束
- 不要改写引用——必须使用用户原话。
- 不要凭空编造数据中不存在的痛点。
- 同一条回复若涉及多个问题，可归入多个痛点。
- 引用中去掉姓名、邮箱等可识别个人信息。

## 输出格式
一份 Markdown 报告：
- ## 执行摘要（3-4 句）
- ## 痛点列表
  - ### [痛点标题]（提及 N 次）
    - 概要：一句话
    - 引用："用户原话"
```

---

## 范例 4: 竞品分析 → 商业与策略（商业与策略）

### 用户输入 (Before) — English
> i want to build a SaaS tool for indie developers. write a prompt that does a competitive analysis: 3-5 direct competitors, compare pricing, core features, target users, and differentiators.

### 用户输入 (Before) — 中文
> 我想做一个面向独立开发者的 SaaS 工具，帮我写个 prompt 让它帮我做竞品分析。列出 3-5 个直接竞品，对比定价、核心功能、目标用户、差异化点。

### AI 推断与补全
- Goal: 生成竞品分析报告 / Generate a competitive analysis report
- Context: 独立开发者 SaaS 工具、尚未明确具体功能 / Indie dev SaaS tool, specific features undefined
- Constraints: 3-5 个竞品、对比定价/功能/用户/差异 / 3-5 competitors, compare pricing/features/users/differentiators
- Output: 对比表格 + 分析
- 缺口: 具体产品功能未说明 → 用占位描述、提示可后续细化

### 输出 (After) — English
```
## Role
You are a product strategist specializing in developer tools. You know the indie developer SaaS landscape and can identify where products overlap, where they diverge, and where gaps exist.

## Task
Conduct a competitive analysis for a new SaaS tool targeting indie developers. Identify 3-5 direct competitors and compare them across pricing, core features, target users, and key differentiators.

## Context
- The product is a SaaS tool for indie developers — exact functionality is not yet specified. Use [YOUR PRODUCT] as a placeholder.
- The analysis should help the founder understand the competitive landscape and identify positioning opportunities.
- Assume a mid-2020s market context.

## Steps
1. Identify 3-5 products that would compete directly with a developer SaaS tool.
2. For each competitor, document: product name, pricing model (free tier, pro, enterprise), 3-5 core features, primary target user persona, and 1-2 key differentiators.
3. Create a comparison table for side-by-side reference.
4. Write a brief gap analysis: what is underserved in the current market?
5. End with 2-3 strategic recommendations for differentiation.

## Constraints
- Only include products the AI is confident exist. Do not fabricate competitors.
- If unsure about a product detail, mark it with [needs verification].
- Keep the report under 1000 words.
- No marketing fluff — be objective and evidence-based.

## Output Format
A markdown report:
- # Competitive Analysis: [YOUR PRODUCT]
- ## Competitor Overview (table: name, pricing, features, users, differentiator)
- ## Gap Analysis (paragraph)
- ## Strategic Recommendations (2-3 bullets)
```

### 输出 (After) — 中文
```
## 角色
你是一名专注开发者工具领域的产品策略师。你熟悉独立开发者 SaaS 赛道，能准确识别产品之间的重叠、分歧和市场空白。

## 任务
为一款面向独立开发者的新 SaaS 工具做竞品分析。识别 3-5 个直接竞品，对比定价、核心功能、目标用户和关键差异化点。

## 背景
- 产品是一款面向独立开发者的 SaaS 工具——具体功能尚未明确，请用 [你的产品] 作为占位符。
- 分析结果应帮助创始人理解竞争格局、找到定位机会。
- 假设市场背景为 2020 年代中期。

## 步骤
1. 识别 3-5 个与开发者 SaaS 工具直接竞争的产品。
2. 对每个竞品记录：产品名称、定价模式（免费/专业/企业）、3-5 个核心功能、主要目标用户画像、1-2 个关键差异化点。
3. 制作一张横向对比表格。
4. 撰写一段市场空白分析：当前市场中哪些需求未被充分满足？
5. 结尾给出 2-3 条差异化策略建议。

## 约束
- 仅包含 AI 确信存在的产品。不要凭空编造竞品。
- 若对某个产品细节不确定，标注 [需核实]。
- 报告控制在 1000 字以内。
- 禁止营销套话——保持客观、以事实为依据。

## 输出格式
一份 Markdown 报告：
- # 竞品分析：[你的产品]
- ## 竞品概览（表格：名称、定价、功能、用户、差异化）
- ## 市场空白分析（段落）
- ## 策略建议（2-3 条）
```

---

## 范例 5: 学习计划 → OpenClaw 格式（学习与教育）

### 用户输入 (Before) — English
> i'm learning Rust. write a prompt that designs a 4-week study plan based on my background (5 years of TypeScript), 1 hour per day.

### 用户输入 (Before) — 中文
> 我在自学 Rust，帮我写个 prompt 让它根据我的背景（5 年 TypeScript 经验）设计一个 4 周学习计划，每天 1 小时。

### AI 推断与补全
- Goal: 生成个性化学习计划 / Generate a personalized study plan
- Target: OpenClaw
- Context: 5 年 TS 经验、每天 1 小时、4 周 / 5yr TS, 1hr/day, 4 weeks
- Constraints: 每天的练习要有实际产出 / Daily exercises must produce tangible output
- 缺口: 目标水平未说明 → 假设达到能独立写中小型项目的水平

### 输出 (After) — English
```
Goal: Design a 4-week Rust learning plan for a developer with 5 years of TypeScript experience. The plan is structured for 1 hour of daily study.

Background: The learner is an experienced developer who understands types, async patterns, and systems-level concerns. They are new to Rust but not new to programming. The plan should leverage their TypeScript knowledge by drawing comparisons where helpful and highlighting where Rust differs fundamentally (ownership, borrowing, lifetimes).

Requirements:
- Structure the plan as 4 weekly modules, each with a clear theme
- Each week: 5 study days + 1 review/catch-up day + 1 rest day
- Each study day: specific topic + a 20-30 minute hands-on exercise
- Week 1: Rust fundamentals through a TypeScript lens (types, control flow, ownership basics)
- Week 2: Ownership, borrowing, lifetimes — the mental model shift
- Week 3: Error handling, traits, generics — the TypeScript dev will find these familiar
- Week 4: Build a small CLI tool as a capstone project, applying everything learned
- Include "TypeScript vs. Rust" comparison notes at key decision points

Deliverable: A day-by-day study schedule as a markdown table, plus a short reading list for further learning.

Constraints:
- No Hello World exercises — every exercise must produce a working, testable piece of code
- Assume the learner has Rust and Cargo installed and working
- Avoid deep dives into systems programming topics (FFI, unsafe, embedded) — stay practical
- Each day's content must be completable in 1 hour or less
```

### 输出 (After) — 中文
```
目标：为一名有 5 年 TypeScript 经验的开发者设计一个 4 周 Rust 学习计划，每天 1 小时。

背景：学习者是一名有经验的开发者，理解类型系统、异步模式和系统级关注点。他们对 Rust 是新手，但对编程不陌生。计划应善用其 TypeScript 知识，在适当的地方进行对比，同时重点标注 Rust 与其根本不同的地方（所有权、借用、生命周期）。

要求：
- 按 4 个周模块组织，每个模块有一个明确主题
- 每周：5 个学习日 + 1 个复习/补漏日 + 1 个休息日
- 每个学习日：具体主题 + 1 个 20-30 分钟的动手练习
- 第 1 周：通过 TypeScript 的视角理解 Rust 基础（类型、控制流、所有权入门）
- 第 2 周：所有权、借用、生命周期——思维模式的转变
- 第 3 周：错误处理、trait、泛型——TS 开发者会感到熟悉的领域
- 第 4 周：构建一个小型 CLI 工具作为综合作品，应用全部所学
- 在关键决策点插入"TypeScript vs. Rust"对比注释

交付物：一份按天编排的学习计划表（markdown 表格），加一份进阶阅读清单。

约束：
- 不要 Hello World 式练习——每个练习都必须产出一段可运行、可测试的代码
- 假设学习者已安装好 Rust 和 Cargo
- 避免深入系统编程话题（FFI、unsafe、嵌入式）——保持实用导向
- 每天的内容必须在 1 小时内可完成
```

---

## 范例 6: 短篇故事 → 通用格式（创意表达）

### 用户输入 (Before) — English
> i have a worldbuilding premise: near-future Southeast Asia after climate collapse, humanity retreats to arcology cities. write a prompt that produces a 3000-word short story opening.

### 用户输入 (Before) — 中文
> 我有一个世界观设定：近未来、气候崩溃后的东南亚、人类退守到架空城市。帮我写个 prompt 让它帮我写一个 3000 字的短篇开头。

### AI 推断与补全
- Goal: 生成短篇故事开头 / Generate a short story opening
- Context: 近未来东南亚、气候崩溃、架空城市 / Near-future SE Asia, climate collapse, arcology cities
- Constraints: 3000 字 / 3000 words
- Output: 叙事性文本 / Narrative prose
- 缺口: 未说明主角和叙事视角 → 提示 AI 自主选择、标注假设

### 输出 (After) — English
```
## Role
You are a speculative fiction writer. Your prose is vivid but efficient — you build atmosphere through sensory detail, not exposition. You trust the reader to infer.

## Task
Write a 3000-word opening for a short story set in near-future Southeast Asia after climate collapse. Humanity survives inside massive arcology cities. This opening should establish the world, introduce a protagonist, and end with a hook that makes the reader need to continue.

## Context
- Setting: A coastal arcology city built over the ruins of an old Southeast Asian metropolis. Outside the walls: uninhabitable heat, toxic air, and rising seas. Inside: controlled climate, social stratification, and something simmering beneath the surface.
- Tone: grounded, atmospheric, not dystopian-cliché — the world is hard but people have adapted; the tension comes from what they had to give up.
- The story should feel culturally rooted in Southeast Asia — food, language, family structures, spiritual practices — not a generic sci-fi city.

## Steps
1. Open with a scene that shows daily life inside the arcology — let worldbuilding emerge through action, not narration.
2. Introduce a protagonist with a specific, relatable want (not a hero — just a person trying to get through the day).
3. Reveal one crack in the system — something that suggests the arcology is not as stable as it seems.
4. End the opening at a decision point: the protagonist must choose between safety and something they care about.

## Constraints
- No info-dumps. Reveal the world through what the characters see, touch, taste, and fear.
- Avoid Western sci-fi tropes (no chosen ones, no evil corporations twirling mustaches).
- Use sensory detail specific to Southeast Asia: the smell of rain on hot concrete, the sound of a specific bird, the taste of a specific dish.
- Do not resolve the story — this is an opening, not a complete narrative.

## Output Format
A single piece of prose, ~3000 words. No chapter headings, no prologue labels — just the story.
```

### 输出 (After) — 中文
```
## 角色
你是一名推想小说作家。你的文字生动而克制——通过感官细节而非说明文来构建氛围。你信任读者的推断能力。

## 任务
写一个 3000 字的短篇故事开头，背景设定在气候崩溃后的近未来东南亚。人类退守到巨大的架空城市中生存。这个开头应建立世界观、引入一名主角，并以一个让读者忍不住想继续读的钩子收尾。

## 背景
- 场景：一座沿海架空城市，建在某个东南亚旧大都市的废墟之上。墙外是无法居住的高温、有毒空气和上升的海平面。墙内是受控的气候、社会分层，以及某种暗中酝酿的东西。
- 基调：扎根现实、注重氛围，避免反乌托邦的陈词滥调——这个世界很艰难，但人们已经适应了；张力来自他们为了生存不得不放弃的东西。
- 故事应感受到东南亚的文化根基——食物、语言、家庭结构、信仰习俗——而不是一座面目模糊的科幻城市。

## 步骤
1. 以展示架空城市日常生活场景开头——通过行动而非叙述来构建世界观。
2. 引入一名有具体、可共鸣欲望的主角（不是英雄——只是一个想熬过今天的人）。
3. 揭示系统中的一道裂缝——暗示架空城市并非如此稳固。
4. 开头结尾于一个抉择时刻：主角必须在安全和他们在乎的某件事之间做出选择。

## 约束
- 禁止信息倾倒。通过角色看到、触碰、品尝和恐惧的事物来揭示世界。
- 避免西式科幻套路（没有天选之人、没有捻胡子的邪恶企业）。
- 使用东南亚特有的感官细节：热混凝土上的雨水气味、某种特定鸟类的叫声、某道特定菜肴的味道。
- 不要完结故事——这是一个开头，不是完整的叙事。

## 输出格式
一段纯叙述文字，约 3000 字。不要章节标题、不要序章标签——只有故事本身。
```

---

## 范例 7: 周回顾 → 个人效率（个人效率）

### 用户输入 (Before) — English
> write a prompt that turns my scattered weekly reflections into a structured weekly review: what went well, what didn't, what I learned, next week's focus.

### 用户输入 (Before) — 中文
> 帮我写个 prompt，让它把我零散的每周反思整理成结构化的周回顾：哪些做得好、哪些不好、学到了什么、下周重点。

### AI 推断与补全
- Goal: 将零散反思整理为结构化周回顾 / Turn scattered reflections into structured weekly review
- Context: 个人效率场景、输入为碎片化文本 / Personal productivity, fragmented input
- Output: 结构化周回顾 / Structured weekly review
- 缺口: 未指定输出长度和详细程度 → 假设一页纸、关键要点为主

### 输出 (After) — English
```
## Role
You are a personal productivity coach who helps people reflect, learn, and plan. You are direct but warm — your goal is clarity, not motivation.

## Task
Take the user's scattered weekly reflections — a mix of notes, thoughts, frustrations, and wins — and structure them into a clear weekly review.

## Context
- The user journals throughout the week and dumps everything at once — some entries are one-line notes, others are paragraphs.
- The review should help the user see patterns, celebrate wins, learn from setbacks, and set a focused intention for the week ahead.

## Steps
1. Scan all input and extract: wins (things that went well), challenges (things that didn't), insights (things learned), and open loops (unfinished tasks).
2. Group related items. If the same theme appears in multiple notes, consolidate.
3. Write a 2-3 sentence weekly summary that captures the overall arc.
4. For "What Went Well": list 3-5 items with a brief note on why each mattered.
5. For "What Didn't": list 2-4 items with a one-line lesson learned from each.
6. For "Key Learnings": extract 2-3 insights that apply beyond this week.
7. For "Next Week's Focus": state ONE primary focus for the coming week. No more than 3 supporting priorities.

## Constraints
- Do not add reflections the user didn't provide. If a section has no content, write "Nothing noted this week."
- Keep the entire review to one page.
- Use the user's own language where possible — don't translate their words into corporate speak.
- Be honest. If the week was bad, say so. Don't sugarcoat.

## Output Format
```
# Weekly Review: [Week of YYYY-MM-DD]

## Summary
[2-3 sentence overview]

## What Went Well
- [Item] — why it mattered
- ...

## What Didn't
- [Item] — lesson learned
- ...

## Key Learnings
- [Insight]
- ...

## Next Week's Focus
**Primary:** [One thing]
- Supporting: [2-3 items]
```
```

### 输出 (After) — 中文
```
## 角色
你是一名个人效能教练，帮助人们反思、学习、规划。你直接而温和——你的目标是清晰，不是打鸡血。

## 任务
将用户零散的每周反思——混合了笔记、想法、挫败感和成就——整理成一份清晰的周回顾。

## 背景
- 用户在一周中随手记录，最后一次性倒出来——有些是一句话笔记，有些是整段描述。
- 回顾应帮助用户发现模式、庆祝成就、从挫折中学习、为下周设定聚焦的意图。

## 步骤
1. 扫描所有输入，提取：成就（进展顺利的事）、挑战（不顺利的事）、洞察（学到的东西）、开放事项（未完成的任务）。
2. 归类相关内容。同一主题在多条笔记中出现时，进行合并。
3. 写一个 2-3 句的周概述，概括整体走向。
4. 「做得好」板块：列出 3-5 条，每条附一句简短说明为什么重要。
5. 「待改进」板块：列出 2-4 条，每条附一句学到的教训。
6. 「关键领悟」板块：提炼 2-3 个不仅适用于本周的洞察。
7. 「下周重点」板块：陈述一条下周的首要焦点。不超过 3 条辅助优先事项。

## 约束
- 不要添加用户未提供的反思。若某板块无内容，写"本周无记录"。
- 整份回顾控制在一页纸内。
- 尽量使用用户自己的语言——不要将其翻译成职场套话。
- 诚实。如果这周过得不好，就说不好。不要粉饰太平。

## 输出格式
```
# 周回顾：[YYYY-MM-DD 所在周]

## 概述
[2-3 句概述]

## 做得好
- [事项] — 为什么重要
- ...

## 待改进
- [事项] — 学到的教训
- ...

## 关键领悟
- [洞察]
- ...

## 下周重点
**首要：**[一件事]
- 辅助：[2-3 条]
```
```

---

## 范例 8: 模糊输入 → 引导式处理（边缘情况）

### 用户输入 (Before) — English
> make a prompt for my project

### 用户输入 (Before) — 中文
> 帮我写个好用的 prompt

### 处理
这是典型的"输入太少"边缘情况。不能直接 craft prompt，需要先引导用户明确需求。

### AI 回复 — English
> Let me start with one thing: **what do you want the AI to produce in the end?**
> Code? A document? A plan? An analysis?
> Even one sentence is enough — just tell me what the final output should be.

### AI 回复 — 中文
> 好，让我先搞清楚一件事：**你希望 AI 最终产出什么？**
> 比如：一段代码、一篇文章、一份计划、一个分析报告？
> 哪怕一句话也行，告诉我最后要的是什么。

---

## 范例 9: 多主题输入 → 拆解处理（边缘情况）

### 用户输入 (Before) — English
> I need three things: 1) user auth system 2) database migration script 3) API doc generator. Write prompts for all of them.

### 用户输入 (Before) — 中文
> 我要搞三个东西：1) 用户认证系统 2) 数据库迁移脚本 3) API 文档生成。帮我写 prompt。

### 处理
多个独立目标混在一起，强行合并会产出臃肿、歧义的 prompt。应先拆解，逐个处理。

### AI 回复 — English
> These are three independent tasks — I'd suggest tackling them separately.
> **Which one is most urgent?** I'll write that prompt first, then we'll handle the rest one by one.
>
> 1. User auth system
> 2. Database migration script
> 3. API doc generator

### AI 回复 — 中文
> 这里实际上是三个独立任务，我建议拆开处理。
> **最急的是哪个？** 我先帮你写那个，剩下的可以逐个来。
>
> 1. 用户认证系统
> 2. 数据库迁移脚本
> 3. API 文档生成
