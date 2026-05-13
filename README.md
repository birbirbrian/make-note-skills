# Make Note Skills

Agent Skills for turning active conversations into structured Markdown notes.

These skills follow the [Agent Skills specification](https://agentskills.io/specification), so they can be used by skills-compatible agents. The current skill is designed for Codex workflows and produces notes that work well in Obsidian.

# Skills

| Skill | Description |
|-------|-------------|
| [`make-note`](skills/make-note) | Create structured Markdown notes from the current conversation, prepare a project `Note/` folder, capture user questions with answers, embed useful website images, and highlight important concepts with Obsidian callouts. |

# Key Features

- Create or reuse a project-local `Note/` folder.
- Read the live user template from `/home/brian/Note/Templates/General.md`.
- Fall back to `skills/make-note/references/note-template.md` when the live template is unavailable.
- Generate a clear technical title and filesystem-safe Markdown filename.
- Ask whether to write the note in Chinese or English unless the request already specifies a language.
- Preserve important questions, answers, decisions, commands, files, and references from the conversation.
- Support Chinese notes when the source material, user questions, or related notes are mainly Chinese.
- Use Obsidian Admonition callouts for important concepts, caveats, confirmations, and question blocks.
- Use Obsidian wiki links for referenced Markdown notes under `/home/brian/Note/Zettelkasten`.
- Review website reference images, save useful ones into `/home/brian/Note/Files/`, and embed them with Obsidian syntax such as `![[image.png]]`.
- Support note updates by merging new Q&A content into the related section.

# Workflow Details

When creating a note, the skill:

- Reads `/home/brian/Note/Templates/General.md` when available.
- Asks whether the note should be written in Chinese or English unless the request already specifies a language.
- Preserves commands, paths, code identifiers, function names, package names, and source titles exactly.
- Converts referenced Markdown notes under `/home/brian/Note/Zettelkasten` into Obsidian wiki links such as `[[Container - Map]]`.
- When a website is used as a reference, reviews meaningful images, saves useful ones into `/home/brian/Note/Files/`, and embeds them with Obsidian syntax such as `![[yocto-layer-flow.png]]`.

# Vault Assumptions

The skill is tuned for Brian's Obsidian vault layout:

```text
/home/brian/Note/
├── Files/                 # Embedded images and other saved note assets
├── Templates/
│   └── General.md         # Preferred live note template
└── Zettelkasten/          # Existing local notes linked with [[wiki links]]
```

# Installation

## Codex CLI

Copy the skill directory into your Codex skills path:

```sh
cp -R skills/make-note ~/.codex/skills/
```

Restart Codex or start a new session so the skill is discovered.

## npx Skills

If this repository is published to GitHub, install it with:

```sh
npx skills add https://github.com/<owner>/make-note-skills
```

## Claude Plugin Metadata

This repository includes `.claude-plugin/marketplace.json` for plugin-style metadata, following the pattern used by [`kepano/obsidian-skills`](https://github.com/kepano/obsidian-skills).

You do not need `.claude-plugin` for the core Agent Skills specification. The required portable skill content is under:

```text
skills/make-note/SKILL.md
```

# Repository Layout

```text
make-note-skills/
├── .claude-plugin/
│   └── marketplace.json         # Optional: plugin-style marketplace metadata
├── README.md                    # Project overview and installation notes
└── skills/
    └── make-note/
        ├── SKILL.md             # Required: metadata + instructions
        ├── agents/
        │   └── openai.yaml      # Optional: Codex/OpenAI UI metadata
        └── references/
            └── note-template.md # Optional: fallback note template
```

# Reference

- [Agent Skills specification](https://agentskills.io/specification)
- [Obsidian embeds](https://obsidian.md/help/embeds)
- [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)
- [Obsidian Admonition](https://github.com/ebullient/obsidian-admonition)
