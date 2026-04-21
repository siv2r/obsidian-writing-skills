# Sample Notes (from Sivaram's vault)

These are real notes in `~/Notes/knowledge/` referenced by the skill as structural exemplars or anti-patterns. The skill MAY read these during Extract if a similar shape applies.

| Note | Template fit | Observations | Lessons |
|---|---|---|---|
| `lagrange-offset-property.md` | Punchline Upfront (gold-standard) | Callout with core property, bridge to FROST, clean derivation, MuSig2 contrast. Every section earns its place. | This is what a good concept note looks like under Punchline Upfront. |
| `fermats-little-theorem-proof.md` | Derivation Chain (partial) | Structurally strong (Statement → Setup → Bijection → Punchline → Extension). Callout noting "$f$ is NOT an automorphism" does exactly the aside-for-misunderstanding move. | BUT: opener is textbook throat-clearing ("Let $p$ be any prime..."). Under explanatory-clarity target, new derivation-chain notes should open with functional-definition + concrete-instantiation (e.g., "$2^{6} \equiv 1 \pmod 7$" before the general theorem). Also add a "key idea" sentence upfront. |
| `frost-shamir-degree-constraint.md` | Q&A Cascade (partial) | Opening question well-motivated. Core insight stated clearly. | Later sections drift from the title question into general FROST mechanics. Stay focused on the title question; bridge satellite material explicitly or cut. |
| `amortized-analysis.md` | Topic-tour anti-pattern | Good grounding in secp256k1 batch algorithm, but lists three methods without the author's perspective on when you'd reach for each. | Concept notes should capture essence, not catalog methods. |
| `modular-inverse-coprime-property.md` | Satellite-drift anti-pattern | Clean Diophantine equation chain, then drifts into group axioms and fast exponentiation that don't serve the core concept. | Satellite sections answering different questions belong in separate notes. |
