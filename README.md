# Make Note Skills

Agent Skills for turning active conversations into structured Markdown notes.

These skills follow the [Agent Skills specification](https://agentskills.io/specification), so they can be used by skills-compatible agents. The current skill is designed for Codex workflows and produces notes that work well in Obsidian.

# Skills

| Skill | Description |
|-------|-------------|
| [`make-note`](skills/make-note) | Create structured Markdown notes from the current conversation, prepare a project `Note/` folder, capture user questions with answers, and highlight important concepts with Obsidian callouts. |

# Key Features

- Create or reuse a project-local `Note/` folder.
- Read the live user template from `/home/brian/Note/Templates/General.md`.
- Fall back to `skills/make-note/references/note-template.md` when the live template is unavailable.
- Generate a clear technical title and filesystem-safe Markdown filename.
- Preserve important questions, answers, decisions, commands, files, and references from the conversation.
- Use Obsidian Admonition callouts for important concepts, caveats, confirmations, and question blocks.
- Support note updates by merging new Q&A content into the related section.

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
- [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)
- [Obsidian Admonition](https://github.com/ebullient/obsidian-admonition)
