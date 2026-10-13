# Guide for agents

This file explains how to change Humanizer-cn without breaking its package or prompt.

## What this repo contains

Humanizer-cn is the Chinese edition of the Humanizer agent skill, written in Markdown. `SKILL.md` is the prompt that agents read. The repo has no build step. The rules and examples are written in Chinese and target Chinese prose; keep them in Chinese.

Keep the skill portable. Do not write instructions that limit it to one or two agent tools.

## Key files

- `SKILL.md` is the source of truth and the repo's only full skill file. It contains portable YAML metadata, the editing constraints in priority order, and 31 numbered patterns grouped in six sections (A-F), with section F holding the Chinese-specific checks.
- `.dskills/` does not exist; the DeepSeek Harness entry is `.dsh/skills/humanizer-cn.md`, a self-contained condensed skill. It defers to the root `SKILL.md` when both are present. Keep its rule summary in sync with `SKILL.md`.
- `README.md` explains installation, use, and patterns.
- `CHANGELOG.md` holds the release notes, newest first. Old notes keep the pattern numbers their release used.
- `.claude-plugin/plugin.json` describes the Claude plugin and points its skill loader at the root `SKILL.md`.
- `.claude-plugin/marketplace.json` lets users add this repo as a Claude marketplace.
- `.cursor-plugin/plugin.json` describes the Cursor plugin. Omit a `skills` path so Cursor loads the root `SKILL.md`.
- `agents/openai.yaml` holds the display name, short description, and default prompt for OpenAI-compatible agents. `agents/deepseek.yaml` does the same for DeepSeek-compatible agents.
- `scripts/validate-package.py` checks package files and shared values.

## Rules for changes

Keep `SKILL.md` and `README.md` in sync.

- **Patterns:** Patterns are numbered from 1 without gaps, strongest and most frequent first. A new tell earns a pattern only when no existing pattern already implies it; prefer folding it into an existing pattern. If you add, remove, or renumber a pattern, update the README tables, the README section title, and every §reference. The validator derives the count from the headings and checks that README pattern names match them.
- **Version:** Keep the same version in `SKILL.md` under `metadata.version`, the first `CHANGELOG.md` heading, `.claude-plugin/plugin.json`, and `.cursor-plugin/plugin.json`. Do not add a top-level `version` field to the skill.
- **README tables:** The validator derives the pattern count from SKILL.md headings and checks that the README pattern names match them. The README pattern section must be titled `全部 N 条模式`.
- **Compatibility:** Keep install and use instructions neutral across agents. Names such as Claude Code, Cursor, OpenCode, and Codex are examples, not limits.
- **Description:** The plugin manifests use the first sentence of the `SKILL.md` description.
- **Length:** Every word of `SKILL.md` is read on each use. The validator caps it at 5,500 words; a change that adds words should earn them.
- **History:** Add a short `CHANGELOG.md` note for any behavior change or non-obvious fix.
- **Checks:** Before publishing, run `python3 scripts/validate-package.py`, `npx skills add . --list`, and `claude plugin validate .`.

## Writing style

Use Plain Language in code comments, prompts, documentation, descriptions, validation messages, and progress reports.

- Lead with the main point.
- Use common words and active voice.
- Keep sentences and paragraphs short.
- Use one term for the same item.
- Use `must` for requirements.
- Use headings, lists, and tables when they help the reader.
- Remove repeated or unnecessary words.
- Limit acronyms and explain technical terms.
- Avoid double negatives.
- Keep exact identifiers, commands, paths, schema fields, quotations, watched phrases, and behavior-bearing examples.
- Keep the full technical meaning.

## Editing the skill

- Keep the YAML metadata valid.
- Treat the prompt below the metadata as the product.
- Prefer a short, clear instruction over another exception or repeated explanation.
