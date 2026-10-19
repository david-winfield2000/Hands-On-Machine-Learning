---
name: define
description: Add a definition for a word to DEFINITIONS.md following the project's definition rules. Use when the user asks to define, add, or explain a term for the definitions file.
model: haiku
---

# Define

Add an entry for the word given in `$ARGUMENTS` to `DEFINITIONS.md` in the project root.

## Rules

- Format the entry as `**Word** = definition`, with the word bolded.
- Use one or two plain sentences that explain what the thing is or does. Skip technical detail unless needed to understand the term.
- Place the entry so fundamental terms come before terms that depend on them. Put it in the section where it fits best; create a new `##` section only if none fits, and add it to the Contents list if the file has one.
- If the range or units are non-obvious, say so briefly (e.g., "It is a non-negative number, not a percentage.").
- Add an example only when it helps, using `Example: ...` in the same line.
- Maintain a table of contents for the broader sections

## Steps

1. Read `DEFINITIONS.md`.
2. If the word already has an entry, update it in place instead of adding a duplicate.
3. Write the entry following the rules above.
4. Edit the file, then reply with the entry you added and its section.
