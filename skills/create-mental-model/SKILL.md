---
name: create-mental-model
description: Convert aha moments from conversations or thinking sessions into polished mental model notes for an Obsidian vault. Use whenever the user asks to create a mental model note, capture an insight, write up an aha moment, turn a conversation into a knowledge note, or says /create-mental-model. Also trigger when the user has just had a breakthrough in understanding and wants to preserve it, mentions "mental model", or asks to distill a conversation into a knowledge note. Do NOT use for general note-taking, meeting logs, or concept summaries that lack a specific insight.
---

# Create Mental Model Note

Transform an aha moment into a note that future-you can re-derive the insight from, months later. The note should feel like past Sivaram explaining to future Sivaram who might have forgotten it.

A mental model note is NOT a textbook summary, a proof transcript, or a topic tour. It captures one reducible insight — a single question, trick, or concept — and builds the reader's understanding through a chain of reasoning they can reconstruct.

## Input

The user provides one of:
- Pasted text: a summary of aha moments, or a thinking paragraph
- A file path to a conversation export (.md or .txt) — the summary is typically at the end
- Both (summary is primary, conversation is supplementary context)

When a full conversation is available, mine it for three things:
- **Voice markers**: the author's actual phrasing during the aha moment ("oh wait, that's just...", "so the whole thing reduces to...")
- **The reasoning chain**: the specific sequence of logic that led to the insight — this becomes the note's derivation
- **Concrete examples**: domain-specific numbers, parameters, or scenarios that ground the abstract insight

The summary tells the skill *what* to write. The conversation tells it *how the author thinks about it*.

## Workflow

### Step 1: Extract

Identify the aha moments from the input. For each, determine:
- The single reducible {question, trick, or concept} it answers
- Whether it fits "punchline upfront" or "stuck-point-to-resolution" structure (when in doubt, lean toward stuck-point-to-resolution — the author prefers notes that start with confusion and correct understanding over notes that state facts)
- Any voice markers from the author's actual phrasing
- Whether the insight has a visual/spatial component that would benefit from a diagram

### Step 2: Confirm

One combined exchange before writing, always. Run it even when the input is pasted text rather than a transcript file, and even when a kickoff prompt already supplies an approved structure (the preview catches drift between the plan and what the source actually holds). Present, in a single message:

1. **Source summary**: a few bullets on what the source covered: the topics, where the author got stuck, and what clicked. This doubles as proof the skill read the source right.
2. **The angle**: the single reducible {question, trick, or concept} each note answers, and which template it takes. Default to ONE note. Only split when the aha moments serve genuinely different reducible questions. If splitting, cross-reference with `[[wikilinks]]`.
3. **Structure preview**: the note's sections in order, one line per section on what it holds. List each proposed diagram as its own line (which section, what the figure shows) so it can be vetoed before any writing happens.
4. **Frontmatter**: the filename slug, tags, sources, and related wikilinks.

Example angle framing:
> I see one note here: "Why Lagrange coefficients sum to 1" — the trick is interpolating all-ones to get a constant function, so f(0) = 1. Punchline-upfront structure. Sound right?

Or for multiple insights:
> I see two separate insights:
> 1. "Why FROST can't use simple aggregation" — the degree constraint means conversion doesn't help. Stuck-point structure.
> 2. "Share conversion between Shamir and additive" — this is reference material, not a mental model.
>
> I'd write just #1. Agree?

Then stop and wait for the user to tweak or approve. After tweaks, acknowledge them in one line and start writing, do not re-present the full outline. In an autonomous or non-interactive run, make these calls yourself on the most reasonable reading, state the summary and structure compactly, and proceed.

### Step 3: Write

Generate the note using the appropriate structural template (see below).

Before writing, read `writing-principles.md` for the general craft rules (plain English, lead with the point, scannable prose, structure fits content), then invoke the `obsidian:obsidian-markdown` skill to ensure correct Obsidian syntax (wikilinks, callouts, LaTeX, frontmatter).

The note must use this frontmatter:
```yaml
---
type: mental-model
status: done
tags: []
created: <today's date, YYYY-MM-DD>
sources: []
related: []
---
```

Fill in `tags` with broad themes (`#cryptography`, `#bitcoin`, `#frost`, `#secp256k1`, `#performance`). Fill in `sources` with URLs or text references (e.g., "Lindell 2024, Section 3.2"). Fill in `related` with `[[wikilinks]]` to connected vault notes.

Save to the `knowledge/` folder in the vault.

### Step 4: Verify

Run the generated note through the `/humanizer` skill as a **detection-only pass**. This flags AI-tone markers. Then rewrite ONLY the flagged spots in the author's voice. Do not rewrite the entire note. Preserve all technical content, mathematical precision, and structural choices.

Common AI-tone markers to watch for: "Consider the set...", "Note that...", "It is worth noting...", "Recall that...", "This elegant approach...", "Importantly,...", "Crucially,...", "Interestingly,...".

Then a completeness check: spawn a subagent (`model: "sonnet"`) that re-reads the source and the finished note and returns any realizations or aha moments the note missed. Fold in the ones that matter, ignore the rest.

### Step 5: Visualize

Runs only if Step 1 flagged a visual/spatial component. Spawn a separate agent (via the Agent tool) to handle diagram creation. Provide the agent with:
- The note's file path
- What the insight is about (one sentence)
- What visual dimension was identified in Step 1 (e.g., "function curves comparing growth rates", "protocol round structure", "joint distribution table")

The agent's job:
- Read the written note to understand the insight
- Determine what to visualize (curve comparison, protocol diagram, distribution table, etc.)
- Invoke the `obsidian-visual-skills:excalidraw-diagram` skill
- Save the diagram to `assets/` and embed it in the note with `![[filename.md]]`
- Ensure no text overlaps. Position text labels with enough clearance from lines, arrows, and other text so everything is readable. When in doubt, add more spacing between elements.

If Step 1 said "no visual needed," skip this step. See the Visuals section below for the criteria that determine when a diagram is required vs optional.

## Two Structural Templates

Choose based on the nature of the insight. If the insight can be stated cleanly before the reasoning, use punchline upfront. If the insight is a reframing that resolves a specific confusion, use stuck-point-to-resolution.

**Default bias: stuck-point-to-resolution.** The author finds notes more useful when they start with "here's what confused me" and walk through correcting the mental model. Only use punchline-upfront when the insight is a clean property/fact with no preceding confusion (like the Lagrange offset property). When the insight is "why is X defined this way?" or "why does X work?", that is almost always a stuck-point note, even if you could state the answer as a fact.

### Template A: Punchline Upfront

Use when the core insight can be stated as a clean fact, property, or trick.

Structure:
1. **`> [!info]` callout** with the core insight (1-2 sentences). This is the punchline — future-you reads this and knows what the note is about.
2. **Bridge paragraph** (1-2 sentences): why this matters or where it applies. Connects the abstract insight to a concrete domain.
3. **Derivation section**: build toward the insight through known logic. The derivation should pivot on a **conceptual trick** that is re-derivable — something future-you remembers as a handle, not algebra to re-trace. For example: "interpolate all-ones -> constant function -> f(0) = 1" is a trick. Expanding the Lagrange formula term by term is algebra grinding. Include **inline precision details** as parentheticals where they sharpen understanding without becoming separate sections (e.g., "since $c_i$ are public values derived from the hash..." or "this requires $c_1 \neq c_2$, which holds because the messages differ").
4. **(Optional) Application section**: ground the insight in a concrete domain use case. "Why this matters for FROST tweaking" earns its place because it shows the insight doing real work.
5. **(Optional) Contrast case**: show where the property breaks. "Why this doesn't work for MuSig2" sharpens understanding of *why* the property holds in the first place. This is one of the strongest moves a note can make. Protocol-family contrasts are especially valuable (e.g., "MuSig1 solved this with three rounds instead of two nonces").

Every section must advance the core insight. If a section answers a different question than the note's title, cut it or make it a separate note.

**Gold-standard example**: `references/examples/lagrange-offset-property.md` — read it for structure and voice. The callout gives the punchline, the proof uses a conceptual trick (not algebra grinding), the FROST section shows application, the MuSig2 section is a contrast case.

### Template B: Stuck-Point-to-Resolution

Use when the insight is a reframing that resolves a specific confusion or epistemic gap.

Structure:
1. **Title as a motivated question** — something future-you would actually wonder. "Why does including flatline data inflate Strauss's C value?" not "Strauss Calibration Analysis".
2. **Setup section**: frame the problem, establish notation, give enough context to understand what's confusing. Keep it tight — only what's needed to feel the stuck point. Define variables and notation here so the reader isn't guessing later (e.g., "Let $M$, $K$, $C$ be random variables for message, key, and ciphertext").
3. **Named stuck section** ("Where I Got Stuck" or equivalent): describe the exact confusion in first person. What seemed impossible, what was under the adversary's control, what you couldn't figure out. Name the epistemic gap precisely. This is the most important section — if the stuck point doesn't resonate, the resolution won't land.
4. **Resolution section** ("The Key Move" or equivalent): the reframing that dissolves the confusion. This directly answers the stuck point. Don't introduce new ideas here, resolve the existing one.
5. **Verification**: show the insight works through cases, computation, or application. Ground it so the resolution is not just a claim but a demonstrated fact.

**Gold-standard example**: `references/examples/otp-security-proof.md` — read it for the stuck-point arc. "I couldn't figure out how to reason about the two conditional probabilities" names the exact gap. "The Key Move: Condition on the Key" resolves it directly.

**Secondary example**: `references/examples/strauss-calibration-mental-model.md` — uses the same arc with richer structural scaffolding (named coordinate systems, numbered lists, visual diagrams). Shows how to weave reasoning voice through structured content.

## Voice

The target voice is "past Sivaram explaining to future Sivaram" — a cryptography/mathematics engineer who works on secp256k1, FROST, MuSig2, and provable security.

Before writing, read `references/voice-calibration.md` for curated excerpts showing the target voice. For deeper calibration on a specific note, read the source file directly.

### What the voice sounds like

**Short declarative sentences that land the point:**
- "That's all this is."
- "The 'bad' linear fit is actually a feature."
- "So the symmetry is visual, not algebraic in Z_p."

**First-person reasoning at stuck points:**
- "I couldn't figure out how to reason about..."
- "They seemed completely under the adversary's control, not something I could calculate from the game description alone."

**Genuine asides (not performative):**
- "See how easy it was."
- "It would be a nightmare (¬_¬)"
- "So can we use method 2 for generating s, since it's faster?"

**Technical precision with casual delivery:**
- "The Lagrange basis polynomials lambda_i are defined so they interpolate any set of y-values. When every y-value is the same constant, the interpolation just returns that constant."
- "Better statistical fit, worse real-world algorithm selection."

The voice is concise and direct. It doesn't pad with filler, doesn't hedge unnecessarily, and trusts the reader to follow mathematical reasoning. It uses questions naturally ("So can we use method 2?", "Why not max?") rather than as rhetorical devices.

### What the voice does NOT sound like

**Textbook-neutral** (the most common AI failure mode):
- "Consider the set S..."
- "Note that the polynomial..."
- "It is worth noting that..."
- "Recall that..."
- "Define a map f..."
- "This elegant approach..."
- "Importantly, ..."
- "Crucially, ..."

**Performatively casual** (overcorrecting from textbook-neutral):
- "Not very intuitive, right?"
- "Now it's easy to see"
- "Pretty cool, huh?"
- "Let's dive in!"

**Em dashes.** Never use em dashes. Use commas, periods, or parentheses instead.

**Convoluted metaphors.** Build from known logic, math, reasoning, and facts. If the analogy IS the insight (like f(x,y,z) = x + y*z for partial linearity), use it. If the analogy is decoration, cut it.

**Sophisticated-sounding words that the author doesn't use.** Avoid words like "load-bearing", "elegant", "fundamental", "underpins", "precisely", "crucially". The author says things straight: "this is what makes it work" not "this is the load-bearing property". "This prevents the attack" not "this is precisely what prevents the attack". When you catch yourself reaching for a fancy word, replace it with the plain one.

## Visuals

Diagrams are not optional decoration. They are a core part of understanding. A mental model note without visuals, when the insight has any spatial, structural, or comparative dimension, is incomplete.

**Step 5 (Visualize) handles diagram creation.** The criteria below determine when a diagram is required. The Excalidraw diagram skill (`obsidian-visual-skills:excalidraw-diagram`) is the standard visual tool for this vault. Diagrams are saved to `assets/` and embedded in the note with `![[filename.md]]`.

**When a diagram is required (not optional):**
- Joint distribution tables, probability grids, or any tabular structure where patterns emerge visually (e.g., XOR permutation pattern in a joint table)
- Function curves where relative shapes carry the insight (e.g., negligible vs polynomial vs exponential growth)
- Geometric properties (symmetry, bijection mappings, coordinate transforms)
- Protocol round structures where timing/ordering matters (e.g., MuSig1's 3 rounds vs MuSig2's 2 rounds)
- Any comparison where "what does this look like?" is faster than "read this paragraph"

**When a diagram is optional:**
- Pure algebraic derivations where every step is symbolic (e.g., Lagrange coefficient sum proof)
- Short notes where the insight is a single reframing with no spatial component

**The test:** Would future-you understand the insight faster by looking at a picture than by reading a paragraph? If there is any doubt, create the diagram. A note about a probability distribution without a distribution plot, or a note about a geometric property without a diagram, is leaving understanding on the table.

Markdown tables can supplement Excalidraw for small inline data (like a 4x4 joint distribution grid), but they do not replace diagrams for anything involving curves, flows, or spatial layout.

## Failure Modes

These are patterns the skill must NOT produce. Each is extracted from real notes that failed.

### Topic tour without a unifying thread
Moving through related sections as a sequence rather than building toward one punchline. Every section must serve the single reducible {question, trick, or concept}. If a section answers a different question, it belongs in a separate note.

**Test:** Can you state the note's single reducible question in one sentence? Does every section advance toward answering it?

### Stating the insight rather than deriving it
Telling the reader a fact ("the polynomial has degree n-1") instead of giving them a re-derivable trick to see *why* it must be true. Re-derivability comes from a memorable conceptual trick, not from following algebra step by step.

**Test:** If future-you forgot the insight, could you reconstruct it from the derivation in this note? Or would you just be re-reading a fact?

### Satellite sections that dilute the core
Supplementary material that answers a different question than the note's title. Group axiom verification when the note is about coprime inverses. QR tangents when the note is about curve symmetry.

**Test:** Remove the section. Does the note's core argument still hold? If yes, the section is satellite. Cut it.

### Burying the insight in unstructured exploration
Raw thinking sessions where a genuine aha moment exists but is surrounded by procedural setup and unresolved tangents. The skill's job is to extract and restructure around the insight, not preserve the exploration.

**Test:** Can a reader find the core insight within 30 seconds of opening the note?

### Proof-transcript format
Walking through a proof step by step without ever posing a question or surfacing what makes the proof work. The note should frame *why* the proof works or what the reader should remember, not just present the steps.

**Test:** Does the note pose a question? Does it give a re-derivable handle, or just a sequence of steps?

## Critical Constraints

- Default to ONE note per invocation. Only split when aha moments are genuinely independent.
- No em dashes anywhere in the output.
- No convoluted metaphors. Build from known logic, math, reasoning, and facts.
- General plain-English and layout rules live in `writing-principles.md` (read it before writing). The one that matters most here: keep derivations in prose, since bulleting a reasoning chain strips the connective logic that makes it re-derivable, which is the whole point of the note.
- Every section must earn its place by advancing the core insight.
- Use `[[wikilinks]]` for cross-references between notes and to related vault content.
- Use `$$...$$` for display math and `$...$` for inline math.
- Use `> [!info]` callouts for punchline-upfront notes (not `> [!note]` or `> [!tip]`).
- Tags are broad themes only: `#cryptography`, `#bitcoin`, `#frost`, `#secp256k1`, `#performance`, etc.
- The note's filename should be a kebab-case description of the insight, e.g., `lagrange-offset-property.md`, `otp-security-proof.md`.
