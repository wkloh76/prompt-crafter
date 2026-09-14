# Prompt Crafter

> You receive scattered thoughts. You ship a battle-ready prompt.

**Prompt Crafter** is an AI skill that transforms fragmented, half-formed ideas into well-structured prompts that any AI agent can execute reliably. Drop in bullet points, rough notes, or vague wishes — it infers your intent, fills in the gaps, and hands back a polished prompt ready for Claude Code, Codex, Cursor, Windsurf, Cline, OpenClaw, Hermes, or any general-purpose LLM.

> **Disclaimer:** This project is developed entirely in my personal time, using my own equipment and resources. It is not affiliated with, endorsed by, or related to my employer. No proprietary company information, code, or resources were used in the creation of this project.

---

## The Problem

Most people know what they want an AI to do but can't articulate it. They write "make it good" when they mean "validate every input field and return a 400 with a machine-readable error code". They say "analyze the data" when they mean "for each row, flag columns where the 7-day moving average deviates by more than 2 standard deviations".

The gap between human intent and AI-executable instruction is where prompts die. Prompt Crafter closes that gap.

---

## Quick Example

**You say:**
> i need something for my team's code review. we use github, PRs are messy, people don't leave good comments. want a checklist or something that reviewers can follow. maybe also for the author before they submit. nothing too long.

**Prompt Crafter produces:**
```markdown
## Role
You are a code review quality specialist helping a software engineering team
improve their pull request process.

## Task
Create a concise code review checklist for both PR authors and reviewers.
The checklist should fit on one printed page and be easy to follow during
real review sessions.

## Context
- The team uses GitHub for pull requests.
- Current problem: reviews are inconsistent, comments lack substance,
  PR descriptions are often incomplete.
- Used by both authors (before submitting) and reviewers (during review).

## Steps
1. Design two sections: "Before You Submit" and "During Review".
2. For each section, list 5-8 concrete yes/no checklist items.
3. Under each item, add one line explaining why it matters.
4. Add a "Review Quality Guidelines" section at the end.

## Constraints
- Keep the entire document under 500 words.
- No abstract advice — every item must be checkable.
- Use plain language. No unexplained jargon.

## Output Format
A markdown document: # PR Checklist → ## Before You Submit →
## During Review → ## Review Quality Guidelines
```

See [`examples.md`](examples.md) for 9 bilingual (EN/ZH) before/after demonstrations.

---

## How It Works

Prompt Crafter follows a 4-phase workflow:

| Phase | What Happens |
|---|---|
| **1. Intake** | Absorb everything the user throws at you — no judgment, no interruption. Collect fragments, keywords, constraints, and "not like X" mentions. |
| **2. Triage** | Sort fragments into Goal, Context, Constraints, Input, and Output Shape. Identify gaps with at most 2-3 clarifying questions. |
| **3. Craft** | Build the prompt from a universal template: Role → Task → Context → Steps → Constraints → Output Format → Examples. |
| **4. Deliver** | Present the prompt in a copyable code block, add a one-line summary, and offer iteration. |

Every output is verified against a 9-item quality checklist (clarity, enforceability, ambiguity, contradictions, platform fit, etc.).

---

## Supported Platforms

Prompt Crafter is a skill definition at its core. Since AI coding platforms don't share a universal instruction format, the project provides self-contained adaptations for each:

| File | Platform | Type |
|---|---|---|
| [`SKILL.md`](SKILL.md) | Frameworks that support YAML-frontmatter skills | Canonical source |
| [`CLAUDE.md`](CLAUDE.md) | [Claude Code](https://claude.ai) | Project instructions |
| [`AGENTS.md`](AGENTS.md) | [Codex (OpenAI)](https://github.com/openai/codex) | Project instructions |
| [`.cursorrules`](.cursorrules) | [Cursor](https://cursor.sh) | Project rules |
| [`.windsurfrules`](.windsurfrules) | [Windsurf](https://windsurf.com) | Project rules |
| [`.clinerules`](.clinerules) | [Cline](https://github.com/cline/cline) | Project rules |
| — | [OpenClaw](https://openclaw.ai), Hermes, ChatGPT, etc. | Use `SKILL.md` as system prompt or reference |

Each file is a standalone, drop-in instruction set. Copy the relevant file into your project root and the platform's AI will follow the prompt-crafting workflow automatically.

---

## Project Structure

```
prompt-crafter/
├── SKILL.md          # Canonical skill definition (YAML-frontmatter)
├── AGENTS.md         # Project documentation + Codex instructions
├── CLAUDE.md         # Claude Code instructions
├── .clinerules       # Cline instructions
├── .cursorrules      # Cursor instructions
├── .windsurfrules    # Windsurf instructions
├── drivers.md       # Collection of trigger phrases (EN/ZH) for testing
├── examples.md      # 9 full before/after examples (bilingual EN/ZH)
├── README.md         # This file
└── License           # License
```

---

## Installation

### Native skill support (recommended)

Clone this repository into your skills directory:

```bash
git clone https://github.com/YOUR_USERNAME/prompt-crafter.git ~/.agents/skills/prompt-crafter
```

Or download and extract manually:

```bash
mkdir -p ~/.agents/skills/prompt-crafter
cp SKILL.md ~/.agents/skills/prompt-crafter/
```

Then activate the skill in your AI coding tool:

```
/prompt-crafter
```

### Per-project platform files

If your AI coding tool doesn't support native skills, copy the corresponding instruction file into your project root:

```bash
# Claude Code
cp CLAUDE.md /path/to/your-project/CLAUDE.md

# Cursor
cp .cursorrules /path/to/your-project/.cursorrules

# Windsurf
cp .windsurfrules /path/to/your-project/.windsurfrules

# Cline
cp .clinerules /path/to/your-project/.clinerules

# Codex
cp AGENTS.md /path/to/your-project/AGENTS.md
```

The AI will read the file automatically — no activation needed. It will follow the prompt-crafting workflow whenever you ask it to write or refine a prompt.

---

## Usage

Once installed, just talk naturally. The AI recognizes trigger patterns and enters the workflow automatically. On load, the skill prints a short bilingual (English / 中文) usage guide with example prompts you can copy. To see that guide again at any time, send the keyword **`pc help`** (aliases: `pc usage`, `/prompt-crafter help`, `pc 帮助`, `prompt-crafter 用法`).

Examples:

```
/prompt-crafter
i need a prompt for my team's code review checklist

帮我写个 prompt，让它根据用户调研提炼核心痛点

write a claude code prompt for generating commit messages

pc help        # re-display the usage guide
```

See [`drivers.md`](drivers.md) for a full collection of trigger phrases to test with.

## Testing

Use [`drivers.md`](drivers.md) to verify the skill is working. Pick any line, paste it into your AI coding tool, and confirm it follows the 4-phase workflow and produces a structured prompt.

---

## Design Principles

- **Concrete over abstract.** "Make it good" → specific, measurable criteria.
- **Front-load the task.** The AI should know what to do within the first paragraph.
- **Constraints are gates.** Imperative language: "Do X", "Never Y", "Always Z".
- **Examples over explanations.** One concrete example is worth a thousand words of description.
- **No scope creep.** Refine structure — don't rewrite intent or add unrequested features.
- **Deliberate minimalism.** This is a single-skill project. No build tools, no dependencies, no runtime.

---

## Contributing

Improvements to the skill workflow, new platform adaptations, or additional examples are welcome. Keep changes scoped:

- **To improve the skill:** Edit [`SKILL.md`](SKILL.md) first, then propagate changes to platform files.
- **To add a platform:** Create the appropriate instruction file (e.g., `.aiderules` for Aide) using the existing files as templates.
- **To add examples:** Append to [`examples.md`](examples.md) following the existing format.
- **To add trigger phrases:** Append to [`drivers.md`](drivers.md).

No build step required. Changes are effective immediately — the files are consumed as-is by the target platforms.

---

## License

See [`License`](License).
