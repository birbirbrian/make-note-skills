---
name: make-note
description: Create structured Markdown notes from the current conversation or selected prior discussion, and prepare a project Note folder for later note capture. Use when the user asks phrases like "help me make note", "make a note", "save this conversation as a note", "output our conversation to Note", "summarize this into my notes", "prepare note-taking for this project", or asks to write a note using a note template.
---

# Make Note

## Project Preparation

When the user opens a project folder and asks to prepare note-taking support, or says they want the project ready so they can later say "make a note for me using the above conversation":

1. Create the workspace `Note/` folder if it does not already exist.
2. Do not create generic placeholder notes.
3. Check that `/home/brian/Note/Templates/General.md` is readable. If it is not readable, rely on `references/note-template.md` when making notes.
4. Tell the user the project is ready and that future requests like "make a note for me using the above conversation" will write into `Note/`.

## Workflow

When the user asks to make a note from the conversation:

1. Read the user's note template at `/home/brian/Note/Templates/General.md` before writing the note. If that file is unavailable, read `references/note-template.md` as the fallback.
2. Determine the note topic from the conversation. Use a clear technical title, not a generic title.
3. Create or reuse the workspace `Note/` folder unless the user specifies another location.
4. Write a Markdown file with a filesystem-safe title, for example `OakStream_BIOS_Boot_Flow_SEC_to_DXE_Conversation.md`.
5. Start the note by filling the template metadata:
   - `created`: current local date in `YYYY-MM-DD` format.
   - `author`: preserve the template author unless the user asks to change it.
   - `X min read`: estimate from the final note length, rounded up, using about 200 words per minute.
   - `tags`: add 2-6 relevant lowercase tags as a YAML list.
6. Keep the template's opening learning section as the first heading after metadata.
   - Always leave one blank line between an H1 heading and the paragraph below it.
   - Do not add a standalone H1 that only repeats the note title or filename topic; the file title already carries the topic.
   - Use H1 headings for major note sections, not only for `# What will learn from this note?`.
   - Under `# What will learn from this note?`, write a numbered list of concrete learning goals tailored to the conversation, not a generic paragraph. Choose the number of items based on the note content; usually 2-5 items is enough, but use more when the conversation genuinely covers more distinct learning goals.
7. Include enough conversation context that the note is useful later:
   - User's original goal or question.
   - Important user questions, especially repeated questions, clarification questions, and questions that changed the direction of the explanation.
   - Important assistant findings or explanation.
   - Key commands, files, functions, code paths, and decisions.
   - Follow-up requests if relevant.
8. Preserve code paths and function names exactly. Use fenced code blocks for flows or snippets.
9. Keep the note readable as a learning artifact. Prefer concise sections over a raw transcript unless the user explicitly asks for a verbatim transcript.
10. Use Obsidian wiki links for related notes and reusable concepts, following the rules below.
11. Use Obsidian Admonition sections sparingly for important concepts or supplementary information, following the rules below.
12. Add a closing `# Learning Recall` section before `# Reference`, following the rules below.
13. Fill the `# Reference` section with relevant local file paths, function names, note links, or source links used in the conversation, following the reference rules below.
14. After writing, tell the user the created file path and the note title.

## Note Language

- Before making a note, ask the user whether to write the note in Chinese or English, unless the user already specified the note language in the current request.
- Write notes in English or Chinese based on the reference information and conversation context.
- Chinese is allowed and preferred when the source material, user questions, or existing related notes are mainly Chinese.
- Keep technical identifiers, code, commands, paths, function names, and source titles in their original form.

## Website Images

When the user provides a website as reference material for a note:

- Review the website content and consider all meaningful images on the page, including diagrams, screenshots, tables exported as images, and architecture figures.
- Include an image only when it improves the learning value of the note; skip decorative, logo-only, tracking, avatar, ad, or unrelated images.
- Save useful images into `/home/brian/Note/Files/`. Create the folder if needed.
- Use clear filenames based on the note topic and image purpose, keeping the original extension when possible.
- Embed saved images in the note with Obsidian embed syntax, for example `![[yocto-layer-flow.png]]`.
- Add image dimensions only when it improves readability, for example `![[yocto-layer-flow.png|640]]` or `![[yocto-layer-flow.png|640x480]]`.
- If the image comes from a website, include the source page URL in `# Reference`.
- If image download is blocked or the image license/source is unclear, do not invent a replacement; mention the source image in the note or reference section instead.

## Reference Rules

- In `# Reference`, if a referenced local Markdown note is under `/home/brian/Note/Zettelkasten`, link it with Obsidian wiki-link syntax instead of a raw file path.
- Use the note filename without the `.md` extension as the wiki link target, for example `/home/brian/Note/Zettelkasten/Cpp/Container - Map.md` becomes `[[Container - Map]]`.
- Keep raw paths for non-note files, files outside `Zettelkasten`, code paths, and generated workspace files.

## Learning Recall

Near the end of each note, before `# Reference`, add a `# Learning Recall` section that answers the opening `# What will learn from this note?` list.

Recall rules:

- Use the same item order as the opening learning-goal list.
- Format each item as a question and answer pair:

```markdown
1. Question based on learning goal?
Answer: Brief answer based on the note.
```

- The numbered line must be the question. The next line must start with `Answer:`.
- Give each answer 1-2 sentences.
- Keep the recall content concrete and based on the note, not generic.
- Do not introduce new topics in the recall section.
- If the note has been updated and the learning-goal list changed, update `# Learning Recall` to match.

## Question Capture

When the conversation contains user questions that are useful for future study, capture them in the note near the related content instead of collecting them only at the end.

Use `question` admonitions for these question-and-answer blocks:

```markdown
> [!question] Why did the build fail after changing `<file>`?
> **Answer:** <Concise answer from the conversation.>
>
> **Related context:** <Short explanation, command, file path, decision, or concept that makes the answer understandable later.>
```

Question capture rules:

- Preserve the user's question meaning, but clean up wording for readability.
- Place the question block directly under the related section, for example under `Main Explanation`, `Key Flow`, or `Important Files and Functions`.
- Include the answer and the related concept explanation together so the note is useful without rereading the chat.
- If several questions belong to the same topic, group them under a short subsection such as `## Questions About Build Flow`.
- If the user asks to update an existing note, append or merge the new question block into the related section of that note instead of creating an unrelated note.
- Use `question` for unresolved or learning questions. If the question reveals a caveat, add a nearby `warning`; if it confirms a result, add a nearby `success`.

## Obsidian Note Links

Use Obsidian wiki links to connect notes when the link improves future navigation or study.

Preferred syntax:

```markdown
[[Related Note Title]]
[[Related Note Title|display text]]
```

Linking rules:

- Use `[[...]]` for related local notes, reusable concepts, project topics, and future notes the user may want to create later.
- It is okay to link to a note that does not exist yet when the concept is likely to become its own note.
- Use an alias with `|` when the sentence needs natural wording, for example `[[Agent Skills Specification|Agent Skills spec]]`.
- Do not wrap code paths, commands, function names, filenames, URLs, or package names in wiki links unless they are also note titles.
- Keep normal Markdown links for external sources: `[Agent Skills specification](https://agentskills.io/specification)`.
- Prefer a few useful links over linking every repeated term.

## Obsidian Admonitions

Use admonitions only when they make the note easier to study. Do not wrap ordinary paragraphs, every takeaway, or whole sections in admonitions.

Prefer Obsidian callout syntax because it stays readable in plain Markdown:

```markdown
> [!tip] Why This Matters
> The key explanation goes here.
```

Use the code-block Admonition syntax only when the note needs a longer plugin-specific block:

````markdown
```ad-tip
title: Why This Matters

The key explanation goes here.
```
````

Choose admonition types by intent:

- `tip`: important concepts, mental models, or practical guidance.
- `info`: supplementary context that helps later understanding.
- `warning`: caveats, risks, gotchas, or constraints that can cause mistakes.
- `question`: unresolved questions, assumptions, or things to verify later.
- `example`: concrete examples that clarify an abstract idea.
- `quote`: short quoted conversation excerpts or source excerpts.
- `success`: confirmed outcomes, working commands, or decisions that are settled.
- `failure`: failed attempts, rejected approaches, or known non-working paths.
- `danger`: high-impact warnings such as destructive commands, data loss, security, or production risk.
- `bug`: defects, regressions, or suspicious behavior discovered in the conversation.
- `abstract`: compact summaries, TL;DR sections, or compressed concept maps.
- `note`: neutral highlighted notes when none of the more specific types fit.

When using a callout:

- Give it a short, useful title after the type, for example `> [!warning] Firmware Update Risk`.
- Keep the body focused: usually 1-3 short paragraphs or bullets.
- Preserve technical names, commands, paths, and function names exactly.
- If a callout contains code, use nested quoted fences:

````markdown
> [!example] Command Pattern
> ```bash
> make test
> ```
````

## Title Rules

- Base the title on the overall conversation topic.
- Use Title Case inside the note heading.
- Use underscores or hyphens in the filename.
- Avoid vague names like `note.md`, `conversation.md`, or `summary.md`.
- If a file with the same name exists, choose a safe variant such as `_2` rather than overwriting unless the user asks to update it.

## Template Requirement

Always reference `/home/brian/Note/Templates/General.md` while making notes. If that file cannot be read, use `references/note-template.md` as the fallback. If the template conflicts with a direct user instruction, follow the direct user instruction and keep the template structure where possible.
