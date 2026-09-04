# Titles

An issue title is written like a commit subject. The shared subject style is defined in `.claude/skills/commit-conventions/SKILL.md`; this file adds what is specific to issues.

## Rules

- Lowercase throughout, including the first word.
- One line of at most seventy-two characters, no trailing period.
- No type prefix, tag, or marker of any kind. The type is carried only by the `type:story`, `type:task`, or `type:bug` label.
- No issue numbers, no labels, and no relationship in the title. Relationships are native links.
- No abbreviations.
- Specific nouns from the repository: name the service, page, command, or concept as the codebase names it.

## By type

- Story and Task titles are imperative and say what will be true afterwards: `export the monthly usage report as a spreadsheet`, `add connection pooling to the order service`.
- Bug titles state what is wrong, as observed: `invoice total shows the wrong currency after switching accounts`. They do not prescribe the fix.

## Examples

| Wrong | Why | Corrected |
| --- | --- | --- |
| `[Task] Add connection pooling` | Prefix and capital letter | `add connection pooling to the order service` |
| `Fix the export bug (#42)` | Capital letter, vague, issue number | `retry the report export twice before showing an error` |
| `Invoices broken` | Not specific, not an observation | `invoice total shows the wrong currency after switching accounts` |
| `DB conn setup` | Abbreviations | `set up the PostgreSQL connection for the order service` |
