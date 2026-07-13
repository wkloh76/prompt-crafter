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
| **4. QUALITY CHECKLIST** | 8-item verification list the agent must run before delivering a prompt. |
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

> The sections above document the project. The sections below are your behavioral instructions. Follow them when users ask you to craft, refine, or improve prompts.

## When to activate

Trigger this workflow when the user:
- Dumps fragmented ideas and says "turn this into a prompt" or "make this usable"
- Says "I want to ask an AI to do X but don't know how to phrase it"
- Provides bullet points, notes, or rough thoughts and asks for a prompt
- Says "help me write a better prompt for..."
- Asks you to "refine", "improve", "structure", or "craft" a prompt
- Mentions they need a prompt for Claude Code, Codex, Cursor, Windsurf, OpenClaw, Hermes, or any specific agent

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

## Examples (if available)
[Show, don't tell.]
```

**Crafting principles:**
1. Be concrete — replace "make it good" with measurable criteria
2. Front-load the task — the Task section alone should be enough to understand what to do
3. Constraints are gates — use imperative: "Do X", "Never Y", "Always Z"
4. Examples are worth 1000 words — include them verbatim if provided
5. Remove ambiguity — "process the files" → "rename each .jpg to YYYY-MM-DD_original.jpg"

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

## Anti-patterns

- **Do not rewrite intent.** "Summarize" stays "summarize", not "comprehensive analysis".
- **Do not add unrequested requirements.** No scope creep.
- **Do not over-structure simple requests.** A one-sentence task may only need a one-paragraph prompt.
- **Do not bury the task.** If 300 words precede the task description, it's backwards.
- **Do not ask more than 3 clarifying questions.** Flag assumptions instead.
- **Do not deliver without running the checklist.**

## Edge cases

- **Too little input:** Ask for the one thing the AI should produce. If the user can't answer, help them think it through conversationally first.
- **Too much input:** Identify the primary goal. Craft a prompt for that one. Offer to handle others separately.
- **Unknown domain:** Say "I don't know enough about [domain] to craft this reliably. Can you point me to a reference?"
- **Safety-critical task:** Add a verification step to the prompt and a constraint to flag uncertainty explicitly.
