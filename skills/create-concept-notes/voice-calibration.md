# Voice Calibration: `/create-concept-notes`

## Target: 60% personal voice, 40% Brilliant / 3Blue1Brown clarity

A concept note should read like Sivaram explaining a session to himself, with enough explainer structure that each piece is clear on its own. The personal voice carries the note. The clarity moves keep the technical core easy to follow. Neither one alone is right: pure personal voice rambles, pure explainer voice reads like a textbook and goes unused.

This is the same personal register as `/create-mental-model`, just spread across a session's worth of material instead of one aha. Where the mental-model voice doc says "past-me to future-me", keep that energy here too. The old version of this skill banned personal narrative and aimed for "author near-invisible". That was the mistake. Do the opposite.

## The 60%: Sivaram's voice

These are real excerpts from the author's notes. Match this register.

**Direct landings after showing the trick:**
> The Lagrange basis polynomials interpolate any set of y-values. When every y-value is the same constant, the interpolation just returns that constant. That's all this is.

> This doesn't solve the problem. After converting $n$ additive shares to $n$ Shamir shares, the underlying polynomial will have degree $n-1$, not $t-1$.

**Questions as natural entry points:**
> So can we use method 2 for generating $s$, since it's faster?

> Can't we just convert the additive shares to Shamir shares later?

**First person at the stuck point (fold a brief version in when an aha is not promoted):**
> I couldn't figure out how to reason about the two conditional probabilities, because the adversary is the one choosing the output.

**Numbers ground every claim:**
> Strauss is only competitive up to about $n = 92$. After that it flatlines and starts degrading.

**Honest asides, genuine not performative:**
> See how easy it was.

> It would be a nightmare (¬_¬).

The thread through all of these: short declarative sentences, no hedging, the author trusts the reader to follow the math. Confidence without flourish.

## The 40%: clarity moves from Brilliant and 3Blue1Brown

Use these to keep the explanation clear. They are scaffolding for the technical core, not a different voice. See `references/brilliant/` and `references/3b1b/` for annotated exemplars.

1. **Functional definition plus a concrete instance**, up front: "A nonce is a one-time random value. For example, in Schnorr signing $k$ is fresh per signature, and reusing it leaks the private key."
2. **Name the action before the term.** Describe what is happening, then attach the name.
3. **Name the reader's likely confusion** and turn it into a hook: "This looks like it should be the same as X, but...".
4. **Pivot word in italics** for the one word that matters: "the symmetry is *visual*, not algebraic".
5. **A short mantra that compresses the idea**, near the close: one line the reader will actually remember.

## How they mix

A good paragraph is mostly voice with clarity scaffolding underneath. Example of the blend:

> So why can't we just aggregate the shares additively? It is faster, and at first it looks fine. The catch is the degree. Additive shares sit on a degree $n-1$ polynomial, and FROST needs degree $t-1$ for $t$-of-$n$ reconstruction to work. Converting them later does not change the degree. That is the whole obstruction.

That is the functional-question opener (clarity), the author's "at first it looks fine" and "That is the whole obstruction" (voice), and a concrete mechanism in between. Roughly 60/40.

The blend is not crypto-specific. The same shape works on any concept:

> What is conditional probability actually doing? You start with the whole sample space, then someone tells you $B$ happened, so you throw out every outcome where it did not. $P(A \mid B)$ is just $A$'s share of what is left. That is the whole idea: the denominator shrinks from everything down to $B$.

The opener names the action before the formula (clarity), "you throw out" and "That is the whole idea" land it (voice), and the definition sits in plain words rather than notation. Reach for this register whatever the subject is.

## The plain-English rule

Keep the English simple and clear. Keep technical terms exact, cut fancy English that is not the concept. The author writes plainly and does not reach for impressive words.

| Don't write | Write instead |
|-------------|---------------|
| "load-bearing property" | "this is what makes it work" |
| "elegant" | (just say why it works) |
| "fundamental" | (just state the thing) |
| "underpins" | "is behind", "makes X work" |
| "precisely" | "exactly", or cut it |
| "crucially" | (cut it, state the fact) |
| "leverage" | "use" |
| "facilitate" | "let", "help" |
| "it turns out that" | (just state what turns out) |
| "the *right* threshold" | "the threshold that actually works" |
| "utilize" | "use" |
| "in order to" | "to" |
| "due to the fact that" | "because" |
| "demonstrate" | "show" |
| "it is worth noting that" | (cut it) |

Technical terms are never the problem. Nonce, homomorphism, negligible function, Lagrange coefficient, soft fork, all stay exactly as they are. The problem is dressing up the connective tissue around them.

## Anti-patterns

- **Textbook throat-clearing:** "Consider $(\mathbb{Z}/p\mathbb{Z})^*$ and pick some $a$...", "Note that...", "It is worth noting...". Openings that delay the concept.
- **Blog-register performance:** "Let's dive in!", "Pretty cool, huh?", "Not very intuitive, right?". Genuine asides are fine, performed enthusiasm is not.
- **Roadmap preambles:** "In this note I'll cover X, then Y, then Z." The headings already show the structure.
- **Coverage over clarity:** cataloguing every method a session touched instead of explaining the ones that mattered.
- **Em dashes and semicolons:** use commas, colons, periods, or parentheses.

## Scope caveat on `birthday-attack-analysis.md`

That blog post (in `writing/`) is pure author voice and good for the 60%, but it is blog-register. Port the worked-example discipline (concrete numbers end to end, MD5 attack time on a real laptop) and the direct asides. Leave the sign-offs, the StackExchange link dumps, and the heavier reader-performance behind. A concept note is calmer than a blog post.
