# create-mental-model

A Claude Code skill that converts aha moments from conversations or thinking sessions into structured mental model notes for Obsidian. Tuned for cryptography and mathematics writing.

This skill is opinionated. The voice, structure, and quality standards are calibrated for a specific writing style: technical precision with casual delivery, the way you'd explain an insight to your future self who might have forgotten it. If that resonates, read on.

## Install

```bash
claude plugin add siv2r/create-mental-model-skill
```

### Prerequisites

This skill invokes other Obsidian skills for markdown syntax and diagram generation. Install these first:

```bash
claude plugin add kepano/obsidian-skills
claude plugin add axton/obsidian-visual-skills
```

The `/humanizer` skill is recommended for voice verification but not required. The skill will still work without it.

## Usage

Invoke with `/create-mental-model` or just describe what you want:

**From a pasted summary:**
> /create-mental-model
>
> Aha moment: if two Schnorr signatures use the same nonce k but different messages, you can extract the secret key by subtracting the equations. s1 - s2 = (c1 - c2)*x. The whole thing reduces to: same k means k cancels and x is exposed.

**From a conversation export:**
> /create-mental-model from conversation.md -- the key insight was understanding why index calculus fails for elliptic curve groups (ring structure vs pure group)

**Rewriting an existing note:**
> Rewrite knowledge/random-variables.md as a mental model note. The aha moment was the XOR washing property: XOR with a uniform key is a permutation, addition is a convolution.

## How it works

The skill follows a 4-step workflow:

1. **Extract** -- identify the single reducible insight (one question, trick, or concept)
2. **Confirm** -- one quick exchange to verify the angle, not a brainstorming session
3. **Write** -- generate the note using one of two structural templates, with Excalidraw diagrams where the insight has a visual dimension
4. **Verify** -- run a humanizer detection pass to catch AI-tone markers, rewrite only the flagged spots

### Two structural templates

**Punchline upfront** -- for clean facts or properties. Opens with a `> [!info]` callout containing the core insight, followed by a derivation that pivots on a conceptual trick (not algebra grinding), then optional application and contrast case sections.

**Stuck-point-to-resolution** (default) -- for insights that resolve a confusion. Opens with a motivated question, names the exact epistemic gap ("Where I Got Stuck"), then resolves it directly ("The Key Move"), followed by verification. The author prefers this structure because it mirrors how understanding actually develops.

### Voice

The target voice is "past you explaining to future you" -- technical precision with casual delivery. No textbook-neutral phrasing ("Consider the set..."), no performative casualness ("Pretty cool, huh?"), no em dashes, no sophisticated-sounding words ("load-bearing", "elegant", "crucially").

Four bundled example notes in `references/examples/` calibrate the voice:
- `birthday-attack-analysis.md` -- purely author-written blog, most authentic voice sample
- `lagrange-offset-property.md` -- gold-standard punchline-upfront structure
- `otp-security-proof.md` -- gold-standard stuck-point-to-resolution structure
- `strauss-calibration-mental-model.md` -- reasoning voice woven through rich scaffolding

### Visuals

Diagrams are not optional. When the insight has a spatial, structural, or comparative dimension, the skill creates Excalidraw diagrams (requires `axton/obsidian-visual-skills`). Joint distribution tables, function curve comparisons, protocol round structures, and geometric properties all get diagrams.

## Domain

The skill is calibrated for cryptography and mathematics: elliptic curves, threshold signatures (FROST, MuSig2), provable security, probability, and abstract algebra. The structural templates and failure modes are general enough for any technical domain, but the voice and examples are from this field.
