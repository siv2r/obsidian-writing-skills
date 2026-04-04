# README Restructure: Single-Skill to Plugin Collection

## Goal

Restructure the README from a single-skill document into a plugin-level README that introduces the `obsidian-writing-skills` collection, following Kepano's `obsidian-skills` pattern.

## Design

### Section 1: Opening

One-liner description: "Opinionated writing skills for Obsidian, tuned for cryptography and mathematics." Then 1-2 sentences about the shared philosophy ("past you explaining to future you" voice, technical precision with casual delivery). No more than a short paragraph.

### Section 2: Installation

Keep as-is. Already updated with correct Marketplace and npx commands, plus prerequisites for `kepano/obsidian-skills` and `axton/obsidian-visual-skills`. The `/humanizer` recommendation stays.

### Section 3: Skills table

A table listing each skill with a link to its folder and a description:

| Skill | Description |
|-------|-------------|
| [create-mental-model](skills/create-mental-model) | Extract the single aha moment from a conversation or thinking session and write it up so future-you can re-create the insight months later, even if you've forgotten the details. Generates LaTeX equations and Excalidraw diagrams where the insight needs them, written in clear technical prose that skips the textbook tone. |

New skills get new rows as they're added.

### Section 4: Voice & Domain (brief)

3-4 sentences covering:
- The shared voice: "past you explaining to future you", technical precision, casual delivery
- The domain calibration: cryptography and mathematics (elliptic curves, threshold signatures, provable security, probability, abstract algebra)
- Note that the structural templates and failure modes are general enough for any technical domain

This is a summary only. Full voice spec lives in each skill's SKILL.md and `references/voice-calibration.md`.

## What gets removed from README

All of the following currently in the README moves to (or already lives in) SKILL.md:
- 4-step workflow (Extract, Confirm, Write, Verify)
- Two structural templates (Punchline upfront, Stuck-point-to-resolution)
- Detailed voice do's and don'ts
- Visuals criteria
- Usage examples (these are skill-specific)

## Other changes

- `plugin.json` description: update from "Convert aha moments into re-derivable mental model notes for Obsidian" to "Opinionated writing skills for Obsidian, tuned for cryptography and mathematics"
