---
name: markdown-standard
description: "Professional Markdown formatting guidelines based on DavidAnson/markdownlint rules. Ensures consistency, accessibility, and readability in .md files."
---

# Markdown Standard (markdownlint)

This document defines Markdown formatting standards to ensure all documents are consistent, easy to read, and compatible with popular linting tools.

> [!NOTE]
> These guidelines are based on the [markdownlint](https://github.com/DavidAnson/markdownlint) library by [David Anson](https://github.com/DavidAnson).

## 1. Headings

* **Sequential Hierarchy (MD001):** Heading levels should only increment by one at a time (e.g., do not jump from # to ###).
* **Surrounding Blank Lines (MD022):** Headings must be surrounded by blank lines.
* **Heading Start (MD023):** Headings must start at the beginning of the line (no indentation).
* **Unique Content (MD024):** Avoid duplicate headings with the same text at the same level.
* **Single H1 Title (MD025):** Each file should have only one level 1 heading (#), preferably on the first line.
* **No Trailing Punctuation (MD026):** Do not use punctuation (., ;, :, !) at the end of a heading, except for a question mark (?).
* **Space After Hash (MD018/MD019):** Use exactly one space after the `#` (e.g., `# Title`).

## 2. Lists

* **Marker Style (MD004):** Maintain consistency in unordered list markers (`*`, `-`, or `+`). The recommended default is `-`.
* **List Indentation (MD005/MD007):** Items at the same level must have the same indentation. Use 2 spaces for each indentation level.
* **Ordered Lists (MD029):** Use the `1.` prefix for lists where order matters, or maintain a consistent sequence like `1.`, `2.`, `3.`.
* **Space After Marker (MD030):** Use exactly one space after the list marker.

## 3. Code

* **Language Specification (MD040):** Fenced code blocks must always specify the language (e.g., ```typescript).
* **Surrounding Blank Lines (MD031):** Fenced code blocks must be surrounded by blank lines.
* **Fence Style (MD048):** Consistently use backticks (` ` `) instead of tildes (~ ~ ~).

## 4. Links and Images

* **No Bare URLs (MD034):** URLs must be wrapped in brackets or converted into actual links (e.g., `[https://google.com](https://google.com)`).
* **Alternative Text (MD045):** Images must always have descriptive `alt text`.
* **Descriptive Link Text (MD059):** Avoid generic text like "click here". Use clear descriptions of the destination.
* **No Internal Spaces (MD039):** Do not leave spaces inside link brackets (e.g., `[ Text ]` is incorrect).

## 5. Spacing and General Style

* **No Trailing Spaces (MD009):** Remove whitespace at the end of lines.
* **Hard Tabs (MD010):** Never use TABs; use only spaces (2 spaces is the standard).
* **Multiple Blank Lines (MD012):** Avoid more than one consecutive blank line.
* **Final Newline (MD047):** Files should end with a single newline character.
* **Emphasis Style (MD049/MD050):** Be consistent in using `*` or `_` for italics and bold. `*` for italics and `**` for bold is recommended.

## 6. Tables

* **Surrounding Blank Lines (MD058):** Tables must be preceded and followed by a blank line.
* **Pipe Alignment (MD055):** Using "pipes" (|) at the beginning and end of each table line is recommended for clarity.
* **Column Consistency (MD056):** All table rows must have the same number of columns.
* **Table Column Style (table-column-style):** Ensures consistent use of column separator pipe characters (`|`). Consistent formatting makes it easier to understand a document.
    - **Parameters:** `aligned_delimiter` (boolean, default `false`), `style` (string, default `any`, values: `aligned` / `any` / `compact` / `tight`).
    - **Styles:**
        - `aligned`: Pipes are vertically aligned (e.g., `| Character | Meaning |`).
        - `compact`: Single space padding around content (e.g., `| Character | Meaning |`).
        - `tight`: No padding around content (e.g., `|Character|Meaning|`).
    - **`aligned_delimiter`:** Requires pipe characters in the delimiter row to align with the header row, even for `compact` or `tight` styles.
    - **Note:** Alignment for `aligned` style is visual (accounts for emoji/CJK width). Leading/trailing pipes are optional.


---

### Best Practices

1. **Accessibility First:** Use headings to structure content, not to style text.
2. **Be Concise:** Keep lines to a maximum of 80-120 characters for easier reading in the editor.
3. **Markdown is Text:** The goal is to be readable both rendered and in raw format.

## References

* **Library:** [markdownlint](https://github.com/DavidAnson/markdownlint)
* **Repository:** `https://github.com/DavidAnson/markdownlint`
* **Author:** [David Anson](https://github.com/DavidAnson)
