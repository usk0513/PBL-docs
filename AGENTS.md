# Repository Guidelines

## Project Structure & Module Organization
- Docs live in `docs/` (e.g., `docs/environment.md`); overview in `README.md`.
- Each doc uses YAML frontmatter: `presentationID`, `title`, `breaks: true`.
- Slide theme (deck): `presentationID: 1D84mef4sJ3EmdKq2WEoOJ9EksQJU4iB-xVAnVSo78fs`.
- Lint configs: `.markdownlint.yml`, `.textlintrc.yml`; term rules in `prh-rules/`.
- MCP: `.mcp.json` exposes a textlint MCP server for agents.

### Creating New Files (Frontmatter & Deck)
- Add YAML frontmatter and confirm both `presentationID` (deck Google Slides ID) and `title` as described in `CLAUDE.md`.
- Then verify the theme with: `deck ls-layouts docs/<file>.md`.
- If the theme is correct, available layouts will include:

```text
タイトル スライド
セクション ヘッダー
タイトルと本文
タイトルと本文ヘディングと本文
タイトルと本文(2列)
タイトルと本文ヘディング(2列)と本文(2列)
タイトルと本文(3列)
タイトルと本文ヘディング(3列)と本文(3列)
タイトルと画像(1枚)
タイトルと画像(2枚)
タイトルと左半分テキスト・右半分画像
要点と画像
本文のみ
セクションタイトルとサブタイトル・右半分本文
タイトルと画像(1枚)と説明
タイトルと画像(2枚)と説明
空白
```

## Build, Test, and Development Commands
- Install: `pnpm i` (or `npm ci`).
- Lint all: `pnpm run textlint:all` and `pnpm run markdownlint:all`.
- Auto-fix: `pnpm run textlint:fix_all` and `pnpm run markdownlint:fix_all`.
- Per-file lint: `pnpm run lint -- <path>` / `pnpm run lint:fix -- <path>`.
- Deck check layouts: `deck ls-layouts docs/<file>.md` (verify expected layouts appear).

## Coding Style & Naming Conventions
- Language: Japanese; normalize terms via PRH (`prh-rules/index.yml`).
- Files: kebab-case `.md` (e.g., `docs/setup-guide.md`).
- Frontmatter required: `presentationID`, `title`, `breaks: true`.
- Headings: single `#` title, then increase depth stepwise; lists use 2-space indents (MD007).
- Soft limit ~150 chars/line (MD013 excludes code/tables). Use fenced code blocks with language tags.

## Testing Guidelines
- Treat linting as tests; commits must pass textlint and markdownlint with zero errors.
- Prefer fix flows, then review diffs: `textlint:fix_all` + `markdownlint:fix_all`.
- For slide docs, confirm standard deck layouts (例: タイトル スライド、セクション ヘッダー) via `deck ls-layouts`.

## Commit & Pull Request Guidelines
- Commit style: short, imperative Japanese summaries (例: 「設定微修正」「ファイル追加」).
- Scope commits narrowly; group related doc edits.
- PRs include purpose, affected paths, before/after notes (structure/terminology), and screenshots when slide layout changes.
- All linters must pass; document any rule exceptions and reasoning.

## Agent-Specific Instructions
- Use MCP textlint tools for consistency:
  - `mcp__textlint__lintFile`, `mcp__textlint__getLintFixedFileContent`, `mcp__textlint__lintText`.
- Do not relax `.markdownlint.yml`/`.textlintrc.yml` without discussion.
- Add standardized terms to `prh-rules/index.yml` when aligning wording.
- Place new docs under `docs/`; do not commit generated artifacts or `node_modules/`.

Note: `package.json` script `lint:fix_all` references a non-existent `markdownlint:all_fix`. Use the individual fix commands above until corrected.
