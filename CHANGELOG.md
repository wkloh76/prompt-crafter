# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- **`npx skills add` installation path** — the README documents installing the skill with the [skills](https://github.com/vercel-labs/skills) CLI for Claude Code, Codex, Cursor, and Kimi Code CLI, including the project and global directory each agent scans (Codex, Cursor and Kimi Code CLI share one copy under `.agents/skills/`; Claude Code is symlinked to it). Completed on 2026-09-21

## [1.0.0] - 2026-09-21

First public release.

### Added

- **Canonical skill (`SKILL.md`)** — a YAML-frontmatter skill that turns fragmented input into a structured, AI-executable prompt through a 4-phase workflow: **Intake → Triage → Craft → Deliver**. Completed on 2026-09-21
- **Wake-word activation** — silent by default; the skill activates only when a message begins with the wake word `pc` (e.g. `pc 帮我把这堆笔记整理成 prompt`) or on the slash command `/prompt-crafter`. `pc help` re-displays the usage guide, `pc on` enables ambient mode (vague input auto-activates), and `pc off` restores silent mode. Completed on 2026-09-21
- **Bilingual usage guide** (English / 中文), printed only when the skill is invoked. Completed on 2026-09-21
- **Mandatory `## Verification` section** — every crafted prompt ends with explicit, checkable verification steps the executor must run before declaring completion. Completed on 2026-09-21
- **9-item quality checklist** and **6 anti-patterns** to catch vague goals, unenforceable constraints, contradictions, and scope creep. Completed on 2026-09-21
- **Prompt Review Gate** — diagnoses an existing prompt (Issues → Suggestions → Corrected Version) before crafting, without rewriting the user's intent. Completed on 2026-09-21
- **Platform adaptations** — self-contained instruction files for Claude Code (`CLAUDE.md`), Codex / OpenAI (`AGENTS.md`), Cursor (`.cursorrules`), Windsurf (`.windsurfrules`), and Cline (`.clinerules`), plus OpenClaw, Hermes, and general-purpose LLM formats inside `SKILL.md`. Completed on 2026-09-21
- **`drivers.md`** — 8 categories of trigger phrases (English + 中文) for testing activation. Completed on 2026-09-21
- **`examples.md`** — 9 bilingual (EN/ZH) before/after demonstrations, each showing the raw user input, the inference, and the crafted prompt. Completed on 2026-09-21

### Fixed

- The YAML frontmatter `description` contained an unquoted colon-space (`self-activate:`), which broke frontmatter parsing and caused skill discovery (e.g. kimi-code) to skip `SKILL.md` entirely. The colon was replaced with a semicolon so the frontmatter parses and the skill loads.

[Unreleased]: https://github.com/wkloh76/prompt-crafter/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/wkloh76/prompt-crafter/releases/tag/v1.0.0
