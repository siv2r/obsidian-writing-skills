# Sample Notes (from Sivaram's vault)

Real notes in `~/Notes/knowledge/`, used as structural and voice exemplars. The point of this file is to show that **good notes have content-shaped structure, not a shared template**. Read a couple before writing, matched to the shape your session calls for. Do not copy a skeleton across, copy the instinct.

## Why there is no template

A survey of the substantive notes in `knowledge/` found no shared skeleton. Only three headings recur across more than two notes at all. Every strong note is structured around its own argument. The notes that read worst are the ones whose structure does not fit their content. So let the concept choose the shape, and lean on these as proof that bespoke structure is the norm here, not the exception.

## Strong notes and why their structure works

**`random-variable.md`** (mental-model, ~1040 words)
Outline: The Problem, Where I Got Stuck, Random Variables Are Functions, The Joint Table Is the Workspace, Deriving a New Distribution, XOR vs Addition, The Row-Universe Analysis, Independence Matters.
Why it works: the confusion-then-resolution arc is explicit, and each heading names a conceptual move, not a topic label. You can follow the reasoning from the headings alone. This is the shape to reach for when a session was one long climb out of a specific confusion.

**`nonce-hash-vs-det-nonce-hash.md`** (mental-model, ~1009 words)
Outline: TL;DR, The single principle, two parallel contrast sections (randomized vs deterministic), a case study, The mnemonic.
Why it works: a TL;DR anchor, parallel structure for the contrast at the heart of the question, and a memory hook at the end. The structure is rhetorical, built for the comparison. Reach for this when a session was about telling two close things apart.

**`frost-det-sign-signer-set-attack.md`** (concept, ~833 words)
Outline: Setup, The attack, Why this works structurally, Why MuSig2 doesn't have this hole, The fix, Why the symmetric solution doesn't apply.
Why it works: the attack/why/exception/fix order mirrors how security reasoning actually moves. The last two headings stop it being a half-told story. Reach for this shape when a session worked through how something breaks and how it is patched.

## Notes that miss, and the diagnosis

**`amortized-analysis.md`** (mental-model, ~321 words): ends on a "Prompt for Deeper Learning" placeholder and lists three methods without building intuition for any. Filed before the model actually formed. Reads like a study outline, not a resolved note. Lesson: do not ship a topic list dressed as a note. If the understanding has not formed, the note should say what is still open (the Open threads element), not pretend to completeness.

**`ec-curve-symmetry-finite-field.md`** (mental-model, ~406 words): headings are topic labels (Plotting the curve, The symmetry axis, Quadratic residues) with no question or anchor, and the content describes rather than explains. The real insight ("the symmetry is visual, not algebraic in $\mathbb{Z}_p$") is buried two-thirds in. Lesson: lead with the anchor, and make headings name moves, not topics.

## What to carry over

- An **opener that anchors** (TL;DR, a callout, or the starting question). Every strong note has one. Every weak note lacks one.
- **Headings that name conceptual moves**, not topic labels.
- An honest **what is still open** when the session did not fully resolve something. Better than faking completeness.
- The author's **voice landing** the points ("That's all this is", "This doesn't solve the problem"), not a neutral textbook tone.
