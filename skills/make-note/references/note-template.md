# Note Template

Use the user's live template at `/home/brian/Note/Templates/General.md` when available:

```markdown
---
created: <YYYY-MM-DD>
author: Brian
X min read: <N min read>
tags:
  - <tag>
  - <tag>
---
# What will learn from this note?

1. <Concrete learning goal tailored to this note.>
2. <Concrete learning goal tailored to this note.>
... Continue only as needed for the note content.

```

After the learning section, adapt the following structure to fit the topic. Do not add a standalone H1 that only repeats the note title or filename topic:

````markdown
# Original Request

<Briefly capture what the user wanted to understand or accomplish.>

# Context

<Mention the project, codebase, folder, technology, or working area involved.>

Link important related local notes or concepts with Obsidian wiki links when helpful:

```markdown
Related notes: [[Agent Skills Specification]], [[Obsidian Admonitions]], [[Conversation Notes]]
```

# Main Explanation

<Teach the main concept in a structured way. Prefer flow order for boot/process topics.>

Place useful user questions near the related explanation:

```markdown
> [!question] <Cleaned-up version of the user's question>
> **Answer:** <Concise answer from the conversation.>
>
> **Related context:** <Concept, command, file, flow, or decision that makes the answer useful later.>
```

# Key Flow

```text
<Step-by-step flow or lifecycle.>
```

# Important Files and Functions

- `<path>`: <why it matters>
- `<function>`: <what it does>

# Takeaways

- <Important concept>
- <Important concept>

Use Obsidian Admonition callouts sparingly for important concepts or supplementary context:

```markdown
> [!tip] Important Concept
> <Short explanation that deserves emphasis.>

> [!warning] Caveat
> <Risk, gotcha, or limitation to remember.>
```

# Follow-Up

<Include follow-up user requests or next study path if relevant.>

# Learning Recall

1. <Question based on learning goal 1?>
Answer: <Brief answer based on the note.>

2. <Question based on learning goal 2?>
Answer: <Brief answer based on the note.>

... Continue only as needed to match the opening learning-goal list.

# Reference

- `<path or source>`: <why it matters>
````

Metadata rules:

- `created`: current local date in `YYYY-MM-DD`.
- `author`: preserve the template value, usually `Brian`.
- `X min read`: estimate the final note length using about 200 words per minute, rounded up.
- `tags`: use 2-6 relevant lowercase tags as a YAML list.
- Put `# What will learn from this note?` as the first heading after metadata.
- Use a numbered list of concrete learning goals under `# What will learn from this note?`; choose the number of items based on the note content.
- Add `# Learning Recall` before `# Reference`; use question and answer pairs where each numbered item is a question and the next line starts with `Answer:`.
- Keep one blank line between each H1 heading and the following paragraph.
- Use H1 headings for major note sections, but do not add a redundant H1 title that only repeats the file/topic name.
- Use Obsidian wiki links such as `[[Related Note]]` or `[[Related Note|display text]]` for useful local note connections.
- Use normal Markdown links for external URLs.

## User's Original Note Prompt

The user's original reusable prompt was:

```text
can you output our the complete conversation to the folder "Note" and give the title of this file releate to the overall conversation?
```
