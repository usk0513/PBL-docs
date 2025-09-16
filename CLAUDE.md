# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository manages documentation for an agile development course for graduate students in information science.
The documentation is written in Markdown and converted to Google Slides using [deck](https://github.com/k1LoW/deck).

Base presentation theme: `presentationID:1D84mef4sJ3EmdKq2WEoOJ9EksQJU4iB-xVAnVSo78fs`

## Document Structure

Markdown files in `/docs/` use YAML frontmatter with:

- `presentationID`: Google Slides presentation ID for deck tool
- `title`: Document title
- `breaks: true`: Enable slide breaks (recommended for proper line formatting)

### Creating New Files

When creating new Markdown files:

1. Always include required YAML frontmatter with `presentationID` and `title`
2. Verify the Google Slides theme is correctly set by running:
   ```bash
   deck ls-layouts <file_path>
   ```
3. Confirm the expected layouts are available (see below)
4. Consider content type and select appropriate slide layouts for each slide
5. Add layout specification using HTML comments:
   ```markdown
   <!-- {"layout": "タイトルと本文"} -->
   ```

### Expected Slide Layouts

When using the correct theme, the following layouts should be available:

- タイトル スライド
- セクション ヘッダー
- タイトルと本文
- タイトルと本文ヘディングと本文
- タイトルと本文(2列)
- タイトルと本文ヘディング(2列)と本文(2列)
- タイトルと本文(3列)
- タイトルと本文ヘディング(3列)と本文(3列)
- タイトルと画像(1枚)
- タイトルと画像(2枚)
- タイトルと左半分テキスト・右半分画像
- 要点と画像
- 本文のみ
- セクションタイトルとサブタイトル・右半分本文
- タイトルと画像(1枚)と説明
- タイトルと画像(2枚)と説明
- 空白

## Deck Tool Usage

### Basic Commands

```bash
# Create new presentation
deck new <filename>.md --title "プレゼンテーション名"

# Apply Markdown content to Google Slides
deck apply <filename>.md

# Open presentation in browser
deck open <filename>.md

# List available layouts
deck ls-layouts <filename>.md
```

### Markdown Formatting Rules

1. **Slide Breaks**: Use `---` (three or more consecutive hyphens) to separate slides
2. **Headings**:
   - Shallowest heading level becomes slide title
   - Next heading level becomes subtitle
   - Deeper headings become content
3. **Layout Specification**: Add layout comments before slide content:
   ```markdown
   <!-- {"layout": "タイトルと本文"} -->
   ```

### Advanced Features

- **Code Block Conversion**: Code blocks can be automatically converted to images
- **Conditional Settings**: Use CEL expressions for dynamic page settings
- **Text Styling**: Create "style" layouts for text formatting (bold, italic, underline)

### Configuration Priority

Settings are applied in this order (highest to lowest priority):
1. Command line options
2. YAML frontmatter in Markdown files
3. Configuration files
4. Default values

## Common Commands

### Linting and Quality Checks

```bash
# Lint specific files
pnpm run lint -- <file>
pnpm run lint:fix -- <file>

# Lint all files
pnpm run lint:all
pnpm run lint:fix_all

# Individual tools
pnpm run textlint -- <file>
pnpm run textlint:fix -- <file>
pnpm run markdownlint -- <file>
pnpm run markdownlint:fix -- <file>
```

## Text Quality Configuration

This repository uses textlint and markdownlint for Japanese technical documentation quality control.

**After modifying any file, always check and fix linter errors:**

1. Use MCP textlint tools to automatically fix textlint errors
2. Address any remaining markdownlint warnings
3. Ensure consistent terminology using the configured prh rules

## MCP Integration

This repository uses textlint MCP server for enhanced linting capabilities:

- `mcp__textlint__lintFile`: Lint markdown files
- `mcp__textlint__getLintFixedFileContent`: Get auto-fixed content
- `mcp__textlint__lintText`: Lint text content directly

**Important**: Always use MCP textlint tools for consistent Japanese technical documentation quality.
When modifying any Markdown file, you MUST run the MCP textlint server to check and fix formatting issues automatically.
