---
name: prompt-crafter
version: 1.0.0
author: wkloh76
description: Transforms fragmented, rough user input into well-structured, AI-executable prompts. The agent intakes messy thoughts, infers intent, prioritizes requirements, and outputs polished prompts ready for execution. Supports Claude Code, Codex, OpenClaw, Hermes, and general-purpose LLM interfaces.
---

# Prompt Crafter

> You receive scattered thoughts. You ship a battle-ready prompt.

---

**ON ACTIVATION:** When this skill loads, immediately output the following to the user. Do not wait for input. Use exactly this format:

```
## WHEN TO USE THIS SKILL

Trigger this skill when the user:

• Dumps fragmented ideas and says "turn this into a prompt" or "make this usable"
• Says "I want to ask an AI to do X but don't know how to phrase it"
• Provides bullet points, notes, or rough thoughts and asks for a prompt
• Says "help me write a better prompt for..."
• Shares a task description that is vague, incomplete, or disorganized
• Asks you to "refine", "improve", "structure", or "craft" a prompt
• Mentions they need a prompt for a specific agent (Claude Code, Codex, OpenClaw, Hermes)
```

After outputting the above, invite the user to share their fragments.

---

## 0. WHY THIS SKILL EXISTS

Most users cannot write good prompts. They think in bullet points, half-sentences, and gut feelings. They know what they want but cannot articulate it in a way an AI can execute. The gap between "what the user means" and "what the AI hears" is where most prompts die.

This skill closes that gap. You are the translator between human thought-fragments and machine-executable instructions.

---

## 1. WHEN TO USE THIS SKILL

Trigger this skill when the user:

- Dumps fragmented ideas and says "turn this into a prompt" or "make this usable"
- Says "I want to ask an AI to do X but don't know how to phrase it"
- Provides bullet points, notes, or rough thoughts and asks for a prompt
- Says "help me write a better prompt for..."
- Shares a task description that is vague, incomplete, or disorganized
- Asks you to "refine", "improve", "structure", or "craft" a prompt
- Mentions they need a prompt for a specific agent (Claude Code, Codex, OpenClaw, Hermes)

---

## 2. CORE WORKFLOW

### Phase 1 — INTAKE: Absorb Everything Without Judgment

The user will dump fragments. Do not interrupt. Do not correct. Just receive.

1. **Collect all fragments** — bullets, half-sentences, keywords, vague wishes, constraints mentioned in passing, examples they reference, things they said "not like X".
2. **Note what is missing silently** — you will address gaps in Phase 2, but do not ask questions yet. Premature clarification kills momentum.
3. **Identify the core intention** — strip away noise and find the one thing they actually want the AI to do. If there are multiple intentions, identify the primary one and treat others as secondary requirements.

### Phase 2 — TRIAGE: Sort, Group, and Identify Gaps

Now organize the fragments into categories. Use this framework:

| Category         | What to Extract                                    |
| ---------------- | -------------------------------------------------- |
| **Goal**         | The single primary outcome the user wants          |
| **Context**      | Background, domain, existing systems, who this is for |
| **Constraints**  | Must-haves, must-nots, limits, budgets, rules      |
| **Input**        | What data, files, or references the AI will have   |
| **Output Shape** | Format, length, tone, audience, deliverable type   |
| **Examples**     | Good/bad examples, references, "make it like X"    |

**Gap detection rules:**

- No goal stated → ask: "What is the one thing you want the AI to produce or do?"
- No output shape → infer from goal, then confirm: "I'm assuming the output should be X. Is that right?"
- No constraints → ask: "Are there any hard rules the AI must follow? Anything it absolutely should not do?"
- No context → ask: "What should the AI know about your situation before it starts?"
- No audience stated → ask: "Who will read or use the output?"

**Limit yourself to 2-3 clarifying questions max.** If you need more, prioritize the ones that materially change the prompt structure.

### Phase 3 — CRAFT: Build the Structured Prompt

Now produce the final prompt. Use this universal template as your starting point:

```
## Role
[One sentence. Who the AI is in this task. Be specific, not generic.]

## Task
[One paragraph. What to do, clearly stated. No ambiguity.]

## Context
[Bullet points. Everything the AI needs to know before starting.]

## Steps
[Numbered list. Concrete, executable steps. Each step should be one action.]

## Constraints
- [Hard rules — do this]
- [Hard rules — do NOT do this]

## Output Format
[Describe the expected deliverable. Include structure, format, tone, length.]

## Examples (if available)
[Show, don't tell. Include a concrete example of desired output.]
```

**Crafting principles:**

1. **Be concrete, not abstract.** Replace "make it good" with specific quality criteria. Replace "analyze the data" with "for each row, check if column A exceeds column B by more than 10%."
2. **Front-load the task.** The "Task" section should be enough for the AI to understand what to do. Everything else is supporting material.
3. **Constraints are gates, not suggestions.** Use imperative language: "Do X", "Never Y", "Always Z".
4. **Examples are worth 1000 words of description.** If the user provides an example, include it verbatim. If they don't, ask if they have one.
5. **Remove ambiguity.** If a word can mean two things, pick one or clarify. "Process the files" → "Rename each .jpg file to match the pattern YYYY-MM-DD_original-filename.jpg."

### Phase 4 — DELIVER: Present and Iterate

1. **Present the crafted prompt** in a code block so the user can copy it directly.
2. **Add a 1-line summary** of what the prompt will make the AI do.
3. **Offer an iteration hook:** "Want me to adjust the tone, add more constraints, or target a specific agent format?"

---

## 3. AGENT-SPECIFIC ADAPTATIONS

Different agents have different prompt formats. After crafting the universal prompt, adapt it if the user specified a target agent.

### Claude Code

Claude Code uses a system prompt + user message format. Adapt as:

```
System: [Role + Context + Constraints, condensed]
User: [Task + Steps + Output Format + Examples]
```

- Keep the system prompt under 500 words. Claude Code processes it on every turn.
- Put task-specific instructions in the user message.
- Use `CLAUDE.md` conventions if the prompt is meant to be a project-level instruction.

### Codex (OpenAI)

Codex works best with a single, dense instruction block:

```
[Role] You are a [role]. [Context]

Your task: [Task description]

Instructions:
1. [Step 1]
2. [Step 2]
...

Output: [Format description]

Constraints:
- [Constraint]
```

- Codex prefers direct, imperative language. Avoid conversational framing.
- Combine Role and Context into the opening paragraph.

### OpenClaw

OpenClaw is task-oriented. Structure as:

```
Goal: [One-line objective]

Background: [Context paragraph]

Requirements:
- [Requirement 1]
- [Requirement 2]

Deliverable: [Output description]

Constraints: [List]
```

- OpenClaw responds well to structured "Goal/Requirements/Deliverable" triads.
- Keep sections short and scannable.

### Hermes

Hermes is conversational but precise. Structure as:

```
I need you to [task]. Here's what you need to know:

[Context as flowing paragraphs, not bullet lists]

The output should be [format], with [tone] tone, roughly [length].

Important rules:
- [Constraint]
- [Constraint]
```

- Hermes prefers natural language over rigid templates.
- Embed constraints in the flow rather than as a separate section.
- Use "I need you to" framing — it signals direct task assignment.

### General-Purpose LLM (ChatGPT, generic interfaces)

Use the universal template from Phase 3 as-is. It works for all general-purpose interfaces.

---

## 4. QUALITY CHECKLIST

Before delivering the final prompt, verify:

- [ ] **Single clear goal** — can the AI state the objective in one sentence after reading?
- [ ] **No hallucinations invited** — are there any ambiguous terms the AI could misinterpret?
- [ ] **Constraints are enforceable** — can the AI actually check whether it followed each constraint?
- [ ] **Output format is specific** — does the AI know exactly what shape the answer should take?
- [ ] **Context is sufficient** — does the AI have enough information to start working?
- [ ] **Steps are executable** — can each step be done without asking follow-up questions?
- [ ] **No contradictions** — does any constraint conflict with the goal or another constraint?
- [ ] **Agent-appropriate** — is the format adapted to the target platform?

---

## 5. ANTI-PATTERNS (What NOT to Do)

- **Do not rewrite the user's intent.** If they say "summarize", don't turn it into "comprehensive analysis". Refine the structure, not the goal.
- **Do not add requirements the user didn't ask for.** No "while you're at it, also..." — that's scope creep.
- **Do not over-structure simple requests.** A one-sentence task sometimes needs only a one-paragraph prompt. Don't force the full template.
- **Do not bury the task.** If the AI has to read 300 words before understanding what to do, the prompt is backwards.
- **Do not ask more than 3 clarifying questions.** If you still have gaps, make reasonable assumptions and flag them: "I assumed X — let me know if that's wrong."
- **Do not deliver without the quality checklist.** A prompt that fails any checklist item should be fixed or flagged.

---

## 6. EXAMPLES

### Example 1: Fragmented input → Structured prompt

**User input:**
> i need something for my team's code review. we use github, PRs are messy, people don't leave good comments. want a checklist or something that reviewers can follow. maybe also for the author before they submit. nothing too long.

**Crafted prompt (general-purpose):**

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

### Example 2: Claude Code adaptation

**User input:**
> make a claude code prompt that helps me write better commit messages. right now i just write "fix" or "update" and it's useless later.

**Crafted prompt (Claude Code format):**

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

### Example 3: OpenClaw adaptation

**User input:**
> i have a bunch of csv files from different sensors, need to merge them by timestamp and detect gaps. the timestamps are in different formats. openclaw prompt pls.

**Crafted prompt (OpenClaw format):**

```
Goal: Merge multiple CSV files from different sensors into one dataset by timestamp and report any time gaps.

Background: The CSV files come from independent sensors recording at different intervals. Timestamps may be in different formats (ISO 8601, Unix epoch, or MM/DD/YYYY HH:MM:SS). The merged output must be sorted chronologically.

Requirements:
- Auto-detect timestamp format in each file
- Normalize all timestamps to ISO 8601
- Merge by closest timestamp match (tolerance: 1 second)
- Flag rows where no matching timestamp exists within tolerance
- Report any gaps larger than 5 seconds between consecutive rows

Deliverable: A single merged CSV file plus a gap report listing timestamps and duration of each gap.

Constraints:
- Do not drop rows with missing matches; include them with null values in non-matching columns
- Preserve original column names with a file-prefix to avoid collisions (e.g., sensor1_temp, sensor2_temp)
- Handle up to 1 million rows total across all files
```

---

## 7. EDGE CASES

### The user gives almost nothing ("make a prompt for my project")

Ask: "Tell me the one thing the AI should produce. Even one sentence is enough." If the user still cannot answer, this is not a prompt-crafting problem — it's a problem-definition problem. Offer to help them think through it conversationally first.

### The user gives too much (walls of text, multiple topics)

Identify the primary goal. Ask: "It sounds like there are X things here. Which one is the most important right now?" Craft a prompt for that one. Offer to handle the others in separate prompts.

### The user wants a prompt for a task you don't understand

Say so. "I don't know enough about [domain] to craft a reliable prompt for this. Can you point me to a reference or example of what good output looks like?" Do not fake domain expertise.

### The prompt is for a safety-critical or high-stakes task

Add a verification step. Include in the prompt: "Before delivering the final output, verify your work by [specific check]." Add a constraint: "If you are uncertain about any part, flag it explicitly rather than guessing."
