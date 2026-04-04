# Voice Calibration Reference

Curated excerpts from the author's notes, ranked by authenticity. Read this file before writing any mental model note to calibrate voice and tone.

## Tier 1: Purely Author-Written (Most Authentic)

From `references/examples/birthday-attack-analysis.md` (blog post, entirely written by the author):

> See how easy it was. Imagine solving the above inequality using our factorial formula. It would be a nightmare (¬_¬).

> I honestly don't dare to attempt deriving such a complicated formula, but if you are interested, you can read more about it in this research paper.

> So, the next time you visit any conference, it might not take much effort to find your birthday twin (ツ).

> Instead of finding the probability for each subcase and adding them, We can use a much simpler technique here.

> From this calculation, MD5 might seem secure. But it is not!

Voice patterns: direct address to the reader as a peer, genuine emoticons for humor, honest admission of limitations ("I honestly don't dare"), concrete grounding in numbers (MD5 128-bit, Intel i7, 24 years), complement technique explained as a reasoning shortcut.

## Tier 2: Best Voice-in-Structure Examples

From `references/examples/lagrange-offset-property.md` (gold-standard punchline-upfront):

> [!info]
> In a $t$-of-$n$ Shamir secret sharing scheme, if you add a constant $t$ to every share, the reconstructed secret shifts by exactly $t$.

> This is the property that makes "agnostic tweaking" work in FROST/ChillDKG — each signer can independently add the tweak to their own share, and the combined signature just works, no coordinator correction needed.

> The Lagrange basis polynomials $\lambda_i$ are defined so they interpolate any set of y-values. When every y-value is the same constant, the interpolation just returns that constant. That's all this is.

> MuSig2 uses key aggregation coefficients $a_i = H(L, X_i)$, not Lagrange coefficients. There's no reason for $\sum a_i = 1$ — the hash function doesn't have this structure.

Voice patterns: "just works" (casual confidence), "That's all this is" (dismissive simplicity after showing the trick), "There's no reason for..." (direct negation without hedging). The callout gives the punchline before the math starts.

---

From `references/examples/otp-security-proof.md` (gold-standard stuck-point-to-resolution):

> I couldn't figure out how to reason about the two conditional probabilities $\Pr[b'=1 \mid b=1]$ and $\Pr[b'=0 \mid b=0]$, because the adversary is the one choosing $b'$.

> Since the proof needs to work for all adversaries, I didn't know how to assign a concrete value to those probabilities. They seemed completely under the adversary's control, not something I could calculate from the game description alone.

> The trick is to not think about what the adversary "decides" to do, but instead condition on the random variable the adversary actually sees, which is the ciphertext.

> The adversary's behavior reduces to a deterministic function of its input. We don't need to know *what* the adversary does.

Voice patterns: first-person confusion stated precisely ("I couldn't figure out how to..."), the exact epistemic gap named ("They seemed completely under the adversary's control"), resolution framed as a reframing ("The trick is to not think about X, but instead Y"), clean landing ("We don't need to know *what* the adversary does").

---

From `references/examples/strauss-calibration-mental-model.md` (reasoning voice through rich scaffolding):

> For Strauss, the calibration currently uses batches from $[2, 500]$, giving $C = 109$. But Strauss is only competitive up to about $n = 92$ — after that, it flatlines and starts degrading.

> Including the flatline data pulls C up because the flatline sits above the linear extrapolation from the competitive region — Strauss never actually reaches the theoretical floor that the linear region predicts.

> Better statistical fit, worse real-world algorithm selection. The "bad" linear fit is actually a feature.

Voice patterns: numbers ground every claim (C=109, n=92, C=104), the closing sentence crystallizes the paradox in two short statements, named coordinate systems structure the reasoning for scannability.

## Tier 3: Notion-Migrated (Natural Voice, Less Polished)

From `knowledge/frost-shamir-degree-constraint.md`:

> So can we use method 2 for generating $s$, since it's faster?

> Can't we use method 2 to generate $n$ additive shares of $s$, then later convert them to Shamir shares using the Lagrange coefficients $\lambda_i$?

> This doesn't solve the problem. After converting $n$ additive shares to $n$ Shamir shares, the underlying polynomial will have degree $n-1$, not $t-1$.

Voice patterns: questions as natural entry points ("So can we use...?", "Can't we just...?"), direct answer followed by explanation ("This doesn't solve the problem. After converting...").

## Anti-Patterns (From Notes That Failed)

From `knowledge/fermats-little-theorem-proof.md` (textbook-neutral voice to avoid):
- "Consider $(\mathbb{Z}/p\mathbb{Z})^*$" — textbook opening, no question posed
- "Define a map $f$..." — instructional tone, no reasoning voice
- The note walks through a proof without ever surfacing *why* it works

From `knowledge/modular-inverse-coprime-property.md` (satellite sections):
- The Diophantine section works. Then it drifts into group axioms and fast exponentiation that don't serve the core question.
- No voice ("That's all this is" equivalent) anywhere in the note.

From `knowledge/ec-curve-symmetry-finite-field.md` (buried insight):
- The genuine insight ("So the symmetry is visual, not algebraic in $\mathbb{Z}_p$") appears two-thirds through the note, surrounded by plotting mechanics and a QR tangent.
- Reads like a live exploration session, not a finished mental model.

## Sophisticated-Sounding Words to Avoid

The author writes plainly. These words sound like AI trying to sound smart:

| Don't write | Write instead |
|-------------|---------------|
| "load-bearing property" | "this is what makes it work" |
| "elegant" | (just describe why it works) |
| "fundamental" | (just state the thing) |
| "underpins" | "is behind" or "makes X work" |
| "precisely" | (cut it, or say "exactly") |
| "crucially" | (cut it, just state the fact) |
| "the *right* threshold" | "the threshold that actually works" |
| "it turns out that" | (just state what turns out) |

The author's actual register: "That's all this is", "just works", "The 'bad' linear fit is actually a feature", "This doesn't solve the problem." Direct. No reaching.
