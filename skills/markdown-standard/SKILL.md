---
name: markdown-standard
description: "This skill should be used when agente create .md files, this guide how to build and structure .md files"
---

# Markdown Standard (markdownlint)

This document defines Markdown formatting standards to ensure all documents are consistent, easy to read, and
compatible with popular linting tools.

> [!NOTE]
> These guidelines are based on the [markdownlint](https://github.com/DavidAnson/markdownlint) library by
> [David Anson](https://github.com/DavidAnson).

## 1. Headings

* **Sequential Hierarchy (MD001):** Heading levels should only increment by one at a time (e.g., do not jump from # to
  ###).
* **Surrounding Blank Lines (MD022):** Headings must be surrounded by blank lines. A common pitfall is placing a list item immediately after a heading without a blank line in between. Always insert a blank line between a heading and a list.
* **Heading Start (MD023):** Headings must start at the beginning of the line (no indentation).
* **Unique Content (MD024):** Avoid duplicate headings with the same text. By default, duplicate headings are globally forbidden across the entire document (not just among siblings). Make each heading globally unique by appending context (e.g., use `### O Problema: Comunicação Entre Pods` instead of repeating `### O Problema` across lessons).
* **Single H1 Title (MD025):** Each file should have only one level 1 heading (#), preferably on the first line.
* **No Trailing Punctuation (MD026):** Do not use punctuation (., ;, :, !) at the end of a heading, except for a
  question mark (?).
* **Space After Hash (MD018/MD019):** Use exactly one space after the `#` (e.g., `# Title`).

## 2. Lists

* **Marker Style (MD004):** Use a consistent symbol for unordered lists (`*`, `-`, or `+`). The default for this repository is `-` (dashes). Mixed markers within the same document are not allowed. Always use dashes (`-`) for unordered lists.
* **List Indentation (MD005/MD007):** Items at the same level must have the same indentation (MD005). Nested list items
  must be indented by exactly 2 spaces relative to their parent list item (MD007). For instance, if the parent starts at column 0, the nested bullet must start at column 2 (2 spaces), and a sub-nested bullet must start at column 4 (4 spaces).
  * **Critical ordered list rule:** When nesting unordered bullets under an ordered list item (e.g., under `1.`), the nested bullet must be indented by exactly 3 spaces (starting at column 3) to align with the text of the parent item, rather than 2 spaces. This allows the parser to recognize it as a nested item. The child bullets under it must then be indented by exactly 5 spaces (column 5) to maintain the 2-space relative indentation step.
* **Ordered Lists (MD029):** Use the `1.` prefix for lists where order matters, or maintain a consistent sequence like
  `1.`, `2.`, `3.`.
  * **Critical list interruption rule:** If a list contains block elements (like tables, code blocks, or paragraphs), these elements **must be indented** to match the indentation of the list item text (typically 3 spaces for top-level ordered items). Failing to indent these blocks interrupts the list context, causing subsequent items to be parsed as a new list. This will trigger an MD029 lint warning because the new list starts with a number other than `1.`.
* **Space After Marker (MD030 / list-marker-space):** Use exactly **one space** after any list marker (`-`, `*`, `1.`, `2.`, etc.). Never use multiple spaces or tabs after a marker.
  * **Critical spacing rule:** A common violation is `MD030/list-marker-space: Spaces after list markers [Expected: 1; Actual: 2]`. This frequently happens when typing two spaces after a number or bullet, particularly when followed by bold markdown text (e.g., writing `1.  **Title:**` or `-  **Title:**` instead of `1. **Title:**` or `- **Title:**`). Always ensure there is precisely one single space between the marker and the item content.
  * **Violation Example:**

    ```markdown
    1.  **Pipeline ETL:** Lógica de extração...
    -  **Outro item:** Detalhes...
    ```

  * **Correct Example:**

    ```markdown
    1. **Pipeline ETL:** Lógica de extração...
    - **Outro item:** Detalhes...
    ```
* **Surrounding Blank Lines (MD032 / blanks-around-lists):** Top-level lists (both ordered `1.` and unordered `-`) must be preceded and followed by a blank line. Never start a list immediately on the line after a paragraph (e.g., an introductory sentence ending with a colon `:` or period), heading, blockquote, or horizontal rule without inserting an empty line. Nested sub-lists, however, must be placed directly inside the parent list item without blank lines between parent and child items to avoid MD007 indentation issues.
  * **Critical Pitfall:** Writing an introductory explanation sentence and starting list item `1.` or `-` immediately on the next line without an empty line in between.
  * **Violation Example (Top-level):**

    ```markdown
    This creates two critical operational problems:
    1. **False Positives:** Legitimate queries are rejected.
    2. **False Negatives:** Complex queries bypass heuristics.
    ```

  * **Correct Example (Top-level):**

    ```markdown
    This creates two critical operational problems:

    1. **False Positives:** Legitimate queries are rejected.
    2. **False Negatives:** Complex queries bypass heuristics.
    ```

  * **Rationale:** Ensures compatibility with standard Markdown AST parsers, avoids accidental paragraph-continuation parsing, and maintains structural consistency.

## 3. Code

* **Language Specification (MD040/fenced-code-language):** Fenced code blocks should have a language specified (e.g., ```typescript).
* **Surrounding Blank Lines (MD031 / blanks-around-fences):** Fenced code blocks must be surrounded by blank lines (both preceding and following).
  * **Critical nested list pitfall:** When embedding code blocks inside lists or sub-bullets (such as task steps, scenario descriptions, or documentation examples), **always** insert a blank line before opening the code fence and after closing it. In addition, indent the fence and its content to match the list item's indentation to avoid interrupting the list structure.
  * **Violation Example (Inside list):**

    `````markdown
    * **Exemplo de Código:**
      ```python
      def hello():
          return "world"
      ```
    * **Próximo item:** Detalhes...
    `````

  * **Correct Example (Inside list):**

    `````markdown
    * **Exemplo de Código:**

      ```python
      def hello():
          return "world"
      ```

    * **Próximo item:** Detalhes...
    `````

* **Fence Style (MD048):** Consistently use backticks (` ` `) instead of tildes (~ ~ ~).

## 4. Links and Images

* **No Bare URLs or Emails (MD034 / no-bare-urls):** URLs and email addresses must never appear as bare plain text (even within regular quotes like `"`user@empresa.com`"`). They must always be explicitly formatted:
  * **As code/examples:** Wrap in backticks (e.g., ` `user@empresa.com` ` or ` `https://api.example.com` `). Always use this when presenting sample payload data, mock inputs, or test parameters.
  * **As clickable markdown links:** Use standard link syntax (e.g., `[Documentação](https://example.com)` or `[carlos@empresa.com](mailto:carlos@empresa.com)`).
  * **As autolinks:** Wrap in angle brackets (e.g., `<https://example.com>` or `<carlos@empresa.com>`).
  * **Common Pitfall:** Writing email addresses or URLs in plain prose, scenario descriptions, or tables without backticks (e.g., writing `e-mail "user@empresa.com"` in plain text triggers MD034; format as `user@empresa.com` or `<user@empresa.com>` instead).
* **Alternative Text (MD045):** Images must always have descriptive `alt text`.
* **Descriptive Link Text (MD059):** Avoid generic text like "click here". Use clear descriptions of the destination.
* **No Internal Spaces (MD039):** Do not leave spaces inside link brackets (e.g., `[ Text ]` is incorrect).

## 5. Spacing and General Style

* **No Inline HTML (MD033 / no-inline-html):** Raw HTML tags (e.g., `<br>`, `<span>`, `<div>`, `<b>`, `<i>`, `<p>`) are forbidden. Always use native Markdown syntax.
  * **Line breaks in tables & lists:** Never use `<br>` inside Markdown table cells or lists. Instead, format multiple items linearly using inline numbering (e.g., `(1) first item; (2) second item`) or separate the content into individual rows/bullets.
* **No Trailing Spaces (MD009):** Remove trailing whitespace at the end of lines. Lines must have either 0 or 2 trailing spaces (where 2 spaces are used explicitly for a line break). A single trailing space (or more than 2) is invalid and will trigger lint warnings.
* **Hard Tabs (MD010):** Never use TABs; use only spaces (2 spaces is the standard).
* **Multiple Blank Lines (MD012):** Avoid more than one consecutive blank line.
* **Final Newline (MD047):** Files should end with a single newline character.
* **Emphasis Style (MD049/MD050):** Be consistent in using `*` or `_` for italics and bold. `*` for italics and `**` for
  bold is recommended.

## 6. Tables

* **Surrounding Blank Lines (MD058):** Tables must be preceded and followed by a blank line.
* **Pipe Alignment (MD055):** Using "pipes" (|) at the beginning and end of each table line is recommended for clarity.
* **Column Consistency (MD056):** All table rows must have the same number of columns.
* **Table Column Style (MD060 / table-column-style):** Ensures consistent use of column separator pipe characters (`|`).
  Consistent formatting makes it easier to understand a document.
  * **Critical compact style rule:** If the style is `compact`, every pipe character (`|`), including the leading pipe of a row and the pipes inside the delimiter row (e.g., `| --- | --- |`), **must** have exactly one space to its right. Failing to put a space after a pipe (like `|----|`) causes lint errors.
  * **Parameters:** `aligned_delimiter` (boolean, default `false`), `style` (string, default `any`, values: `aligned` /
    `any` / `compact` / `tight`).
  * **Styles:**
    * `aligned`: Pipes are vertically aligned (e.g., `| Character | Meaning |`).
    * `compact`: Single space padding around content (e.g., `| Character | Meaning |`).
    * `tight`: No padding around content (e.g., `|Character|Meaning|`).
  * **`aligned_delimiter`:** Requires pipe characters in the delimiter row to align with the header row, even for
    `compact` or `tight` styles.
  * **Note:** Alignment for `aligned` style is visual (accounts for emoji/CJK width). Leading/trailing pipes are
    optional.

---

### Best Practices

1. **Accessibility First:** Use headings to structure content, not to style text.
2. **Be Concise:** Keep lines to a maximum of 80-120 characters for easier reading in the editor.
3. **Markdown is Text:** The goal is to be readable both rendered and in raw format.

## References

* **Library:** [markdownlint](https://github.com/DavidAnson/markdownlint)
* **Repository:** `https://github.com/DavidAnson/markdownlint`
* **Author:** [David Anson](https://github.com/DavidAnson)
