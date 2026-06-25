# obsidian-writing-skills

Opinionated writing skills for Obsidian, tuned for cryptography and mathematics. The target voice is "past you explaining to future you": technical precision with casual delivery, the way you'd explain an insight to your future self who might have forgotten it.

## Install

**Marketplace:**

```
/plugin marketplace add siv2r/obsidian-writing-skills
/plugin install writing@obsidian-writing-skills
```

**npx:**

```bash
npx skills add git@github.com:siv2r/obsidian-writing-skills.git
```

### Prerequisites

These skills invoke other Obsidian skills for markdown syntax and diagram generation. Install these first:

```
/plugin marketplace add kepano/obsidian-skills
/plugin install obsidian@obsidian-skills

/plugin marketplace add axtonliu/axton-obsidian-visual-skills
/plugin install obsidian-visual-skills
```

The `/humanizer` skill is recommended for voice verification but not required.

## Skills

| Skill | Description |
|-------|-------------|
| [create-mental-model](skills/create-mental-model) | Extract the single aha moment from a conversation or thinking session and write it up so future-you can re-create the insight months later, even if you've forgotten the details. Generates LaTeX equations and Excalidraw diagrams where the insight needs them, written in clear technical prose that skips the textbook tone. |
| [create-concept-notes](skills/create-concept-notes) | Recap a study or Socratic session from a `cc-export` transcript into a clear concept note (or two) under `knowledge/` in your Obsidian vault. The breadth companion to create-mental-model: where that captures one deep aha, this captures the spread of what a session covered and explains it plainly, in 60% your own voice and 40% Brilliant-wiki / 3Blue1Brown clarity. |

## Voice & Domain

The shared voice across all skills is "past you explaining to future you." Short declarative sentences, first-person reasoning at stuck points, no textbook-neutral phrasing ("Consider the set..."), no performative casualness ("Pretty cool, huh?"). Each skill's SKILL.md has the full voice spec, with curated examples in `references/`.

The skills are calibrated for cryptography and mathematics: elliptic curves, provable security, probability, and abstract algebra. The structural templates and failure modes are general enough for any technical domain, but the voice and examples are from this field.
