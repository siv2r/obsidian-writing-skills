---
name: write-concept-note
description: Converts source material (AI conversations, blog posts, textbook excerpts, PR reviews, explainer docs) into a short reference concept note in Sivaram's Obsidian vault under `knowledge/`. Use this skill whenever the user asks to "write a concept note", invokes `/write-concept-note`, says "capture this concept", "add this to knowledge", or otherwise wants a polished 300-800 word reference explanation of a technical concept written in explanatory-clarity voice (Brilliant-wiki / 3Blue1Brown register). Do NOT trigger for aha-moment / insight notes (that's `/create-mental-model`), for meeting or conference notes, for blog drafts or other long-form writing, or for task tracking.
---

# Write Concept Note

Produce a short (300-800 word) reference explanation of a technical concept and save it as a note under `knowledge/` in Sivaram's Obsidian vault. The output is a standalone reference — the kind of entry you'd find in a Brilliant wiki or a 3Blue1Brown-style explainer — not a personal insight, meeting log, or blog draft.

## When to invoke
- The user asks to write a concept note, run `/write-concept-note`, or says "capture this concept".
- The user provides source material (conversation, blog excerpt, textbook passage, PR review, explainer doc) where a concept is explained clearly.

## When NOT to invoke
- The user wants to capture an aha moment or personal stuck-point resolution → use `/create-mental-model` instead.
- The user wants meeting notes, blog drafts, task tracking, or reading clippings — those go to `log/`, `writing/`, `tasks/`, and `clippings/` respectively.

## Boundary guard (flag and re-confirm)
If the source material contains a named stuck point or confusion that resolved into an insight, flag to the user and point to `/create-mental-model` as a possibly better fit. Do NOT bail silently or force the redirect. If the user confirms they still want a concept note, proceed.

Flag test: does the note's value come from *the resolution of confusion* or from *the explanation of a concept*?
- "I couldn't figure out how to assign probabilities, then I realized you condition on the key" → flag (mental-model territory).
- "Here's how Fermat's Little Theorem works via a bijection argument" → proceed as concept note.

When the boundary is blurry, default to whichever framing matches the source material's energy.

## Properties of a good concept note

A good concept note:
- Reduces to a single {concept, property, technique, or theorem} that everything else serves.
- Builds understanding, not just states facts. The reader walks away with a re-derivable chain of reasoning, not a memorized result.
- Has concrete examples or applications that ground the abstract.
- Reads in explanatory-clarity voice: the concept is the star, author voice is near-invisible but not absent (register of Brilliant wiki / 3Blue1Brown transcripts).
- Every section earns its place. Contrast cases and generalizations are welcome; satellite sections answering different questions belong in separate notes.
- Has rich structural scaffolding (named sections, numbered lists when appropriate) for scannability.

A concept note FAILS when it has:
- Topic tour without a unifying thread.
- Proof-transcript without upfront "why this proof works" framing.
- Stated facts instead of built understanding.
- Satellite sections that dilute the core.
- Coverage-driven writing (trying to be comprehensive rather than essence-capturing).
- Textbook-neutral voice at the note level ("Consider...", "Define a map...", "One observes that...").

## Structural templates

Default to Punchline Upfront when the fit is not obvious. The Confirm step presents the choice to the user.

### Punchline Upfront (default)

For clean properties, theorems, or techniques where the result is the star.

Structure:
1. `> [!info]` callout with the core statement/property.
2. Bridge paragraph: why this matters or where it shows up.
3. Derivation/explanation: the chain of reasoning that builds understanding.
4. Application or contrast (optional): where this concept shows up in practice, or where it breaks.

Gold-standard example: `lagrange-offset-property.md` in the vault — callout with core property, bridge to FROST application, clean derivation, MuSig2 contrast. Every section earns its place.

### Q&A Cascade

For concepts best understood through progressive "but why?" questions. Each question deepens the previous answer. The questions CHAIN (each answer raises the next), which distinguishes this from Riddles (independent puzzles).

Structure:
1. Motivated opening question (something the reader would actually wonder).
2. Answer that raises a follow-up question.
3. Deeper answer, possibly with another follow-up.
4. Final resolution that ties the cascade together.

Structural reference: `frost-shamir-degree-constraint.md` in the vault (its progressive questioning structure works; note that the later sections drift from the title question — fix that drift when using this template).

### Derivation Chain

For proofs or mathematical arguments where the reasoning chain *is* the concept.

Structure:
1. Statement of what we're proving/establishing.
2. **Key idea (1-2 sentences):** the high-level reason the proof works, stated as a conceptual handle. This is what future-reader remembers; the steps below show why it's true. Example: "Multiplication by $a$ is a permutation of the group, so the product of all elements is invariant."
3. Setup: the objects and map/construction.
4. Key steps with explanation of *why* each step works (not just *that* it works).
5. Punchline: the result falls out.
6. Extension or generalization (optional).

Structural reference: `fermats-little-theorem-proof.md` in the vault. Strong step structure, but its opener ("Let $p$ be any prime...") is textbook throat-clearing to AVOID — prefer the Brilliant-wiki pattern (functional definition + concrete instantiation).

### Riddles

For notes on a primitive that has 2-3 known-weird corners (edge cases, variant behaviors, failure modes) that each deserve their own resolution. Each "riddle" is an *independent* puzzle about the primitive; answering each deepens understanding of the whole.

Structure:
1. Open with a one-line statement of the primitive and a teaser that its "obvious" behavior has 2-3 corners worth examining.
2. Enumerate the riddles explicitly upfront: "Does X hold when ...?", "What happens if ...?", "Can we ...?"
3. Resolve each riddle in its own section. Each resolution stands alone; the reader can skip to the one they care about.
4. Optional closing: brief synthesis of what the riddles collectively reveal.

Structural reference: `references/conduition/adaptorsigs.md` (The Riddles of Adaptor Signatures). The skeleton ports; do NOT port conduition's voice.

When to choose Riddles: one primitive with multiple *independent* puzzle-like questions (adaptor-signature variants, nonce-misuse cases, threshold edge cases). Use Q&A Cascade if the questions chain. Use Punchline Upfront if the result is the star.

## Skill workflow

### Step 1: Extract
Identify the single reducible {concept, property, technique, or theorem} from the source material. Determine:
- Which structural template fits (default: Punchline Upfront).
- What voice moves from `voice-calibration.md` apply.
- Whether visuals would help (spatial/coordinate/geometric content → yes; pure algebraic → no).

Read `voice-calibration.md` and scan `references/brilliant/`, `references/3b1b/`, and `references/conduition/` for the most relevant exemplars given the concept's shape.

### Step 2: Confirm
Present the proposed framing to the user in ONE quick exchange. The question is about scope and angle, not whether the concept is worth capturing. Template-specific examples:

- **Punchline Upfront:** "I'll write a concept note about Lagrange coefficients summing to 1, using **Punchline Upfront**: callout with the property, bridge to FROST tweaking, derivation via interpolating all-ones, MuSig2 contrast. Sound right?"
- **Q&A Cascade:** "I'll write a concept note about FROST's degree constraint, using **Q&A Cascade**: start with 'Can we use simple aggregation instead of DKG?' → 'Can't we convert additive to Shamir?' → 'No, the degree doesn't change.' Sound right?"
- **Derivation Chain:** "I'll write a concept note about Fermat's Little Theorem, using **Derivation Chain**: Statement → Key idea (multiplication by $a$ permutes the group) → Setup → Bijection proof → Cancel products → Euler extension. Sound right?"
- **Riddles:** "I'll write a concept note about adaptor-signature edge cases, using **Riddles**: enumerate three puzzles upfront ('Is MuSig-aggregated adaptor safe?', 'What if the adaptor is leaked before signing?', 'Can we use adaptors across threshold sigs?') and resolve each independently. Sound right?"

Proceed on confirmation. If the user redirects, adjust template/scope and re-confirm.

### Step 3: Write
Generate the note. Required frontmatter:

```yaml
---
type: concept
status: done
tags: []
created: <today's date>
sources: []
related: []
---
```

- Invoke `obsidian:obsidian-markdown` skill for correct Obsidian syntax (wikilinks, callouts, LaTeX math, embeds).
- Save to `~/Notes/knowledge/<slug>.md`. Slug is kebab-case of the concept name.
- Default to ONE note per invocation.

While writing, keep `voice-calibration.md` and the 6 cross-source patterns active: functional definition + concrete instantiation opening, analogy-first terminology-second, name likely confusion, pivot word in italics, mantra close, disarming meta-comment.

### Step 4: Verify
Run the `humanizer` skill on the generated note as a detection pass. For each flagged issue:
- If it's genuine AI-tone (em dashes, "delve into", "navigate", "landscape") — rewrite.
- If it's a target voice move the humanizer misflagged — leave and document in a review note.

Also verify structurally:
- Note reduces to a single concept (Properties checklist).
- Opening matches functional-definition-plus-concrete-instantiation pattern or a justified alternative.
- No textbook throat-clearing.
- No blog-register reader engagement.

### Step 5: Visualize (optional)
If Step 1 flagged a visual/spatial component, spawn an agent to create a diagram using `obsidian-visual-skills:excalidraw-diagram`. Save to `~/Notes/assets/<slug>-<diagram>.excalidraw.md` and embed in the note as a wikilink.

Source material tells the skill *what* to write. Conversation context (if available) tells it *how the author engaged with the concept* — what questions they asked, what examples resonated, what connections they drew.

## Sibling skill integrations

- **`obsidian:obsidian-markdown`**: invoked in Step 3 (Write) for correct wikilink, callout, frontmatter, LaTeX, and embed syntax.
- **`humanizer`**: invoked in Step 4 (Verify) as a detection pass for AI-tone markers.
- **`obsidian-visual-skills:excalidraw-diagram`**: invoked in Step 5 (Visualize) when a visual is warranted.
- **`obsidian:obsidian-cli`**: used during any vault operations that need Obsidian's resolution (reading existing notes, setting properties, verifying generated content renders).

Do NOT invoke `/create-mental-model` from inside this skill — the boundary guard instructs the user to switch skills if the source is an aha moment.
