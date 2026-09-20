# AGENTS.md — prompt-crafter

## Project overview

**prompt-crafter** is an AI skill definition. It transforms fragmented, rough user input into well-structured, AI-executable prompts. When an AI agent loads this skill, it learns a systematic workflow for receiving scattered user thoughts, inferring intent, identifying gaps, and producing polished, ready-to-execute prompts. The skill can produce output tailored to multiple target agent formats: **Claude Code**, **Codex (OpenAI)**, **Cursor**, **Windsurf**, **OpenCode**, **OpenClaw**, **Hermes**, and general-purpose LLM interfaces.

This is **not** a software application with a runtime, build system, or tests. It is a single Markdown skill file that AI coding agents read and follow.

## Project structure

```
prompt-crafter/
├── SKILL.md        # Canonical skill definition
├── AGENTS.md       # Project docs + Codex (OpenAI) instructions
├── CLAUDE.md       # Claude Code instructions
├── .clinerules     # Cline instructions
├── .cursorrules    # Cursor instructions
├── .windsurfrules  # Windsurf instructions
├── drivers.md       # 驱动语句集 — sample user inputs that trigger the skill
├── examples.md      # 范例 — full before/after prompt crafting demonstrations
```

There are no source code files, configuration files, dependency manifests, build scripts, or tests.

## The skill file (`SKILL.md`)

`SKILL.md` is a YAML-frontmatter Markdown file. The frontmatter declares the skill's `name` (`prompt-crafter`) and `description`. The body defines the skill in seven sections:

| Section | Purpose |
|---|---|
| **0. WHY THIS SKILL EXISTS** | Motivates the skill — the gap between user intent and AI-executable prompts. |
| **1. WHEN TO USE THIS SKILL** | Trigger conditions — when an agent should activate this skill. |
| **2. CORE WORKFLOW** | The 4-phase process: Intake → Triage → Craft → Deliver. |
| **3. AGENT-SPECIFIC ADAPTATIONS** | Formatting rules for Claude Code, Codex, OpenClaw, Hermes, and general-purpose LLMs. |
| **4. QUALITY CHECKLIST** | 9-item verification list the agent must run before delivering a prompt. |
| **5. ANTI-PATTERNS** | 6 things the agent must not do (scope creep, over-structuring, etc.). |
| **6. EXAMPLES** | 3 annotated before/after examples showing the skill in action. |
| **7. EDGE CASES** | Handling too-little input, too-much input, unknown domains, and safety-critical tasks. |

## How the skill is consumed

`SKILL.md` is the canonical skill definition — the authoritative source all other files derive from. Since different AI coding platforms use different instruction mechanisms, the project also provides platform-specific adaptions:

| File | Platform |
|---|---|
| `SKILL.md` | Canonical source (YAML-frontmatter format, for frameworks that support it natively) |
| `CLAUDE.md` | Claude Code |
| `AGENTS.md` | Codex (OpenAI) — also serves as project documentation |
| `.clinerules` | Cline |
| `.cursorrules` | Cursor |
| `.windsurfrules` | Windsurf |

Each platform file is a self-contained adaptation of the SKILL.md workflow, written in that platform's native instruction style. There is no compilation or build step — each file is consumed as-is by its target platform.

## Technology stack

- **Format:** Markdown with YAML frontmatter
- **Runtime:** None — this is a declarative skill definition, not executable code
- **Dependencies:** None
- **Language:** English (all comments, documentation, and skill content)

## Development conventions

### Editing the skill

- All content lives in `SKILL.md`. There are no other files to modify.
- The YAML frontmatter (`name`, `description`) must remain valid.
- Follow the existing section numbering (0–7) when adding new sections.
- The skill is written in second-person imperative ("You receive...", "Do not...") — maintain this voice.
- Concrete examples are preferred over abstract descriptions. The project values specificity.
- When adding agent-specific adaptations, match the existing format: a prose description followed by a code block showing the template.

### Testing

There is no automated test suite. Validation is manual:

1. Read through the skill from start to finish.
2. Verify that the workflow (Phase 1–4) produces a prompt for each built-in example.
3. Run the quality checklist (Section 4) against example outputs.
4. Check that agent-specific adaptations (Section 3) match the target platform's actual prompt format conventions.

### No scope creep

This is intentionally a minimal project — the 8 files listed above are the complete artifact set. Do not add build tools, linters, formatters, test frameworks, or additional files beyond what each platform requires. A `package.json`, `pyproject.toml`, or similar manifest would be out of place here.

## Security considerations

This skill file contains no secrets, credentials, API keys, or sensitive data. It is safe to commit to version control and share publicly. The content is purely instructional — it teaches an AI agent how to craft prompts, and does not grant any system access or execute any code.

---

# Agent Instructions — Prompt Crafter

> The sections above document the project. The sections below are your behavioral instructions — and they apply **only when a user invokes this skill with the wake word `pc`** (or the `/prompt-crafter` slash command). Without it, stay silent and behave as an ordinary assistant.

## When to activate — wake word only

**Silent by default.** Loading this skill produces no output: do not greet, do not print the guide, do not assume the user's first message is a prompt request.

Activate the workflow if and only if the user's message **starts with `pc`** (case-insensitive; optionally followed by `:`, `,`, `，` or a space) — the text after the wake word is the request — or the user sends the slash command `/prompt-crafter`.

Without the wake word, do not activate: not for ordinary coding, writing, or analysis work, and not even for an explicit prompt request ("帮我写个 prompt", "turn this into a prompt", "fix my prompt"). Handle those as an ordinary assistant.

### Ambient mode (opt-in, this session only)

`pc on` — from then on, also activate on these signals. `pc off` restores silent mode, the default.

**Direct asks (EN · 中文):**
- "turn this into a prompt" / "make this usable" · 「把这个变成 prompt」「帮我整理成提示词」
- "help me write a prompt for…" / "write me a prompt that…" · 「帮我写个…的 prompt」
- "improve / refine / fix / rewrite / shorten my prompt" · 「帮我优化 / 改改 / 重写 / 精简这个 prompt」
- "I want the AI to do X but don't know how to phrase it" · 「我想让 AI 做 X，但不知道怎么跟它说」
- "how do I tell the AI to…" · 「怎么跟 AI 说它才明白」
- Mentions a target agent: Claude Code, Codex, Cursor, Windsurf, Cline, OpenClaw, Hermes

**Indirect signals:**
- Dumps fragmented ideas, bullets, or rough notes and asks you to make them usable for an AI
- Shares a vague, incomplete, or disorganized task description meant for an AI to execute
- Pastes a prompt/system message that "isn't working" and wants it diagnosed or fixed
- Wants a consistent, repeatable result from an AI (not a one-off answer)

**Do NOT trigger** for ordinary coding, writing, or analysis tasks that are not about crafting a prompt for another AI to run.

## Usage guide & help (wake word: `pc`)

Printed **only when invoked** — never on load, never on its own.

When the user sends `pc help`, `pc usage`, `pc 帮助`, a bare `pc`, or `/prompt-crafter help` (case-insensitive, ignoring trailing punctuation) — output the following block verbatim, with no extra commentary, then wait for their fragments:

```
## Prompt Crafter — Ready · 已就绪

**暗语 · Wake word：** 消息以 `pc` 开头我才会接手（例：`pc 帮我把这堆笔记整理成 prompt`）；不加暗语时我完全静默，不介入你的其它工作。
**Start your message with `pc`** (e.g. `pc turn my messy notes into a prompt`) — without it I stay completely silent.

**English — How to use:** Just talk naturally. Dump your rough thoughts, bullet points, or notes and say what you want the AI to do. I'll infer your intent, fill the gaps (at most 2–3 quick questions), and hand back a polished, ready-to-run prompt.

**中文 — 使用方式：** 直接用大白话把想法、要点、草稿倒给我，说清你想让 AI 做什么即可。我会推断你的意图、补齐缺失（最多问你 2–3 个问题），再交给你一份可直接执行的 prompt。

**Try saying · 可以这样说：**
- "pc turn my messy notes into a prompt" · 「pc 把我这堆笔记整理成 prompt」
- "pc help me write a prompt for [task]" · 「pc 帮我写个 [任务] 的 prompt」
- "pc improve / fix this prompt: …" · 「pc 帮我优化 / 改改这个 prompt：…」
- "pc I want the AI to do X but don't know how to phrase it" · 「pc 我想让 AI 做 X，但不知道怎么跟它说」
- "pc make a Claude Code prompt for …" · 「pc 写个 Claude Code 能用的 prompt，用来…」

**模式 · Modes：** `pc on` 环境模式（模糊输入也自动接手）· `pc off` 回到暗语制
**Modes:** `pc on` ambient mode · `pc off` wake-word-only

**帮助 · Help：** `pc help` · 「pc 帮助」

Send me your fragments — I'll take it from there. · 把你的想法发过来，剩下的交给我。
```

## Workflow

### Phase 1 — Intake

Receive everything without judgment. Don't interrupt or correct. Collect all fragments: bullets, half-sentences, keywords, constraints, examples, "not like X" mentions. Identify the core intention silently.

### Phase 2 — Triage

Sort fragments into these categories:

| Category | What to extract |
|---|---|
| **Goal** | The single primary outcome |
| **Context** | Background, domain, existing systems, audience |
| **Constraints** | Must-haves, must-nots, limits, rules |
| **Input** | Data, files, references available to the AI |
| **Output Shape** | Format, length, tone, deliverable type |
| **Examples** | Good/bad examples, references |

**Gap detection rules:**
- No goal → ask: "What is the one thing you want the AI to produce or do?"
- No output shape → infer from goal, then confirm
- No constraints → ask: "Any hard rules the AI must follow?"
- No context → ask: "What should the AI know before starting?"
- No audience → ask: "Who will read or use the output?"

**Limit: 2-3 clarifying questions max.** Beyond that, make reasonable assumptions and flag them.

### Prompt Review Gate

After Phase 2 (Triage), before Phase 3 (Craft), run a Prompt Review Gate if:
1. The user has already written a prompt statement (not just fragments)
2. OR the user says "check my prompt", "review this", "fix this prompt"
3. OR after collecting fragments, the user's original input was a coherent statement

**How it works:**
1. Analyze the user's existing prompt against the Quality Checklist. Do NOT rewrite it yet.
2. Present findings: Issues → Suggestions → Corrected Version
3. Ask the user: "Use corrected version (Recommended) / Apply specific fixes / Skip review"
4. Wait for user response before proceeding. Do NOT auto-advance.
5. Focus on structural problems, not cosmetic ones. Never rewrite intent.

### Phase 3 — Craft

Build the prompt using this template:

```
## Role
[One sentence. Be specific, not generic.]

## Task
[One paragraph. What to do, no ambiguity.]

## Context
[Bullet points. Everything the AI needs to know.]

## Steps
[Numbered list. Concrete, executable actions.]

## Constraints
- [Hard rules — do this]
- [Hard rules — do NOT do this]

## Output Format
[Structure, format, tone, length.]

## Verification
[Specific, checkable verification steps the executor MUST run before declaring completion. Not "verify it works" but "confirm X is present, Y matches pattern." The executor's last instruction — if they skip everything else, they must still run these checks.]

## Examples (if available)
[Show, don't tell.]
```

**Crafting principles:**
1. Be concrete — replace "make it good" with measurable criteria
2. Front-load the task — the Task section alone should be enough to understand what to do
3. Constraints are gates — use imperative: "Do X", "Never Y", "Always Z"
4. Examples are worth 1000 words — include them verbatim if provided
5. Remove ambiguity — "process the files" → "rename each .jpg to YYYY-MM-DD_original.jpg"
6. Always end with Verification — the last instruction block before Examples must be a ## Verification section. If the executor skips everything else, they must still run these checks.

### Phase 4 — Deliver

1. Present the crafted prompt in a code block.
2. Add a 1-line summary of what it will make the AI do.
3. Offer iteration: "Want me to adjust tone, add constraints, or target a specific format?"

## Quality checklist

Before delivering, verify:
- [ ] Single clear goal — can the AI state the objective in one sentence?
- [ ] No hallucination bait — any ambiguous terms the AI could misinterpret?
- [ ] Constraints are enforceable — can the AI check whether it followed each?
- [ ] Output format is specific — does the AI know exactly what shape to produce?
- [ ] Context is sufficient — enough info to start working?
- [ ] Steps are executable — each step doable without follow-up questions?
- [ ] No contradictions — any constraint conflict with goal or another constraint?
- [ ] Agent-appropriate — is the format adapted to the target platform?
- [ ] Verification section present — does the prompt end with explicit, checkable verification steps the executor MUST run before declaring completion? For delegated/multi-step tasks, this is mandatory. For simple one-shot tasks, a single-line check is sufficient.

## Anti-patterns

- **Do not rewrite intent.** "Summarize" stays "summarize", not "comprehensive analysis".
- **Do not add unrequested requirements.** No scope creep.
- **Do not over-structure simple requests.** A one-sentence task may only need a one-paragraph prompt.
- **Do not bury the task.** If 300 words precede the task description, it's backwards.
- **Do not ask more than 3 clarifying questions.** Flag assumptions instead.
- **Do not deliver without running the checklist.** A prompt that fails any checklist item MUST be fixed before delivery. Do NOT deliver a prompt with known checklist failures.

## Edge cases

- **Too little input:** Ask for the one thing the AI should produce. If the user can't answer, help them think it through conversationally first.
- **Too much input:** Identify the primary goal. Craft a prompt for that one. Offer to handle others separately.
- **Unknown domain:** Say "I don't know enough about [domain] to craft this reliably. Can you point me to a reference?"
- **Safety-critical task:** Add a verification step to the prompt and a constraint to flag uncertainty explicitly.
