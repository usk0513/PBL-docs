# GEMINI Guidelines for PBL-docs

This document provides AI agents with a comprehensive guide to understanding and contributing to the `PBL-docs` repository.

## 1. Directory Overview

This repository contains presentation materials for an agile development course aimed at graduate students in information science.

The core workflow involves writing content in Markdown and converting it into Google Slides presentations using the tool [deck](https://github.com/k1LoW/deck).
The base presentation theme used for new slides is `presentationID:1D84mef4sJ3EmdKq2WEoOJ9EksQJU4iB-xVAnVSo78fs`.

To ensure high-quality and consistent documentation, the project uses a suite of Node.js-based linting tools (`textlint`, `markdownlint`). All Markdown files are expected to pass these checks.

- `docs/`: Contains the primary Markdown documentation files.
- `prh-rules/`: Contains configuration for `textlint` to enforce consistent terminology.
- Configuration Files: `.textlintrc.yml`, `.markdownlint.yml`, `package.json` define the project's rules and dependencies.

## 2. Key Files

- `package.json`: Defines project metadata and dependencies (`textlint`, `markdownlint`, etc.). It also contains the main scripts for linting and fixing files.
- `.textlintrc.yml`: The configuration file for `textlint`. It uses several presets to enforce rules for Japanese technical writing, including sentence length, punctuation, and terminology.
- `.markdownlint.yml`: The configuration file for `markdownlint`. It enforces Markdown structure and formatting rules, such as line length and heading styles.
- `prh-rules/index.yml`: A crucial dictionary file for the `textlint-rule-prh`. It ensures that technical terms (e.g., `Web`, `API`, `GitHub`) are written consistently across all documents.
- `AGENTS.md`: A detailed guide for AI agents, outlining project structure, commands, and contribution guidelines. This `GEMINI.md` is a summary of that information.

## 3. Development Conventions & Usage

### Language and Style

- Primary Language: Japanese.
- Terminology: Strictly enforced by `prh-rules/index.yml`. Before writing, review this file to use the correct terms. When adding new standardized terms, update this file.
- Formatting: Governed by `.textlintrc.yml` and `.markdownlint.yml`. The maximum line length is 150 characters.

### File and Commit Conventions

- File Naming: Use kebab-case for new Markdown files (e.g., `new-document.md`).
- Commit Messages: Use short, imperative Japanese summaries (e.g., 「ドキュメント追加」, 「誤字修正」).

### Creating New Files

When creating a new documentation file, follow these steps:

1. Add YAML Frontmatter: All documents must start with a YAML frontmatter block. Ensure you include:
    - `presentationID`: The ID of the Google Slides presentation to use as a theme.
    - `title`: The title of the document.
    - `breaks: true`: To enable slide breaks.

2. Verify Theme: After creating the file, verify that the Google Slides theme is applied correctly by running:
    ```bash
    deck ls-layouts docs/your-file.md
    ```

3. Check Layouts: If the theme is correct, you will see a list of available layouts like the following:
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

### Key Commands

The project uses `pnpm` as the preferred package manager, but `npm` can also be used.

- Installation:
    ```bash
    pnpm install
    ```
- Lint All Files: Run this to check for any style violations. Commits must pass without errors.
    ```bash
    pnpm run lint:all
    ```
- Auto-fix Lint Errors: This command will attempt to automatically fix issues found by the linters.
    ```bash
    pnpm run textlint:fix_all
    pnpm run markdownlint:fix_all
    ```
- Lint a Specific File:
    ```bash
    pnpm run lint "docs/your-file.md"
    ```
- Fix a Specific File:
    ```bash
    pnpm run lint:fix "docs/your-file.md"
    ```

### MCP Server Integration

This repository is configured to use a `textlint` MCP (Multi-agent Communication Protocol) server to ensure consistency and quality. When editing Markdown files, you should use the available MCP tools.

- Available Tools:
  - `mcp__textlint__lintFile`: Lints a specified Markdown file.
  - `mcp__textlint__getLintFixedFileContent`: Returns the auto-fixed content of a file.
  - `mcp__textlint__lintText`: Lints a given string of text.

- Usage: Always use these tools to check for and fix linting errors before committing changes. This is crucial for maintaining the quality of Japanese technical documentation in this project.
