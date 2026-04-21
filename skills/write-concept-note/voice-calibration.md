# Voice Calibration: `/write-concept-note`

## Target voice: explanatory clarity

The concept is the star; author voice is near-invisible but not absent. "We" or "you" is fine when it aids understanding, but no personal narrative and no "past-me-to-future-me" framing (that belongs to `/create-mental-model`).

## Reference genre

Brilliant.org wiki and 3Blue1Brown transcripts. Direct, precise, builds understanding step-by-step. Clarity **with depth** — not general-audience "shape of the idea" summaries (Sivaram's crypto domain needs to actually go into the math, not gesture at it). Short sentences where they aid clarity, longer ones where precision requires them. No throat-clearing, no roadmap preambles, no stakes-setting rhetoric.

## Voice moves to replicate

Drawn from the author's concept-note-shaped writing:

- **Direct assertions that name the mechanism:** "That's all this is." (from lagrange-offset-property)
- **Genuine asides that prevent misunderstanding:** "$f$ is NOT an automorphism. It doesn't preserve the group operation... All $f$ does is permute the group elements." (from fermats-little-theorem-proof)
- **Casual precision that compresses a step:** "So the whole question reduces to: what's the value of $\sum \lambda_i$?" (from lagrange-offset-property)
- **Motivated framing phrased as a reader-directed question:** "So can we use method 2 for generating $s$, since it's faster?" (from frost-shamir-degree-constraint)

## Author exemplar with scope caveat

- `birthday-attack-analysis.md` (in `writing/`): port ONLY the worked-example discipline (computing concrete numbers end-to-end, e.g., MD5 attack time on a specific laptop). Leave behind the reader-check-ins, casual transitions, emoticons, sign-offs, and StackExchange link dumps — those are blog-register reader engagement, not explanatory clarity.

## Cross-source voice patterns to replicate

Convergent signals across Brilliant wiki and 3Blue1Brown:

1. **Functional definition + concrete instantiation** in the opening two sentences: "X is a <function description>. For example, ..."
2. **Analogy-first, terminology-second**: describe the action or phenomenon before introducing the name.
3. **Name the reader's likely confusion**: turn anticipated objections into hooks ("This is not the same as...", "might appear too obvious to be useful, but...").
4. **Pivot word in italics** for the one word that matters: "*what* exactly a vector *is*".
5. **Mantra / aphorism close**: compress the core insight into a memorable one-liner.
6. **Disarming meta-comment**: "make sure we're all on the same page", "it might seem obvious, but...".

See `references/` for annotated exemplars demonstrating each pattern.

## Anti-patterns

Avoid at the sentence level:

- **Textbook throat-clearing:** "Consider $(\mathbb{Z}/p\mathbb{Z})^*$ and pick some $a$...", "Note that...", "It is worth noting..." — formal openings that delay the concept.
- **Unmotivated proof steps:** "Define a map $f$..." without saying why.
- **Blog-register reader engagement:** "Not very intuitive, right?", "Let's dive in!", emoticons, meme asides, sign-offs.
- **Personal narrative / stuck-point framing:** "I couldn't figure out...", "I kept thinking..." — belongs to mental-model notes.
- **Roadmap preambles:** "In this note, I'll cover X, then Y, then Z." The note's structure should be visible from its headings alone.
- **Stakes-setting rhetoric:** lengthy motivations for why the concept matters beyond a 1-2 sentence bridge.
- **Em dashes:** use commas, colons, or parentheses instead.
