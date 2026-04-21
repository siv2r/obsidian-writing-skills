---
source: https://brilliant.org/wiki/eulers-theorem/
fetched: 2026-04-21
annotation-type: voice-exemplar
sources-team-review: "Curated by reviewer-brilliant during explainer-research team round (2026-04-20)."
---

# Euler's Theorem (Brilliant wiki)

## Opening excerpt

> **Euler's theorem** is a generalization of Fermat's little theorem dealing with powers of integers modulo positive integers. It arises in applications of elementary number theory, including the theoretical underpinning for the RSA cryptosystem.

## Distinctive excerpt

> Let n be a positive integer, and let a be an integer that is relatively prime to n. Then a^φ(n) ≡ 1 (mod n), where φ(n) is Euler's totient function.
>
> Consider the elements r₁, r₂, …, r_φ(n) of (ℤ/n)*, the congruence classes of integers that are relatively prime to n. For a ∈ (ℤ/n)*, multiplication by a is a permutation of this set.
>
> The elements in (ℤ/n) with multiplicative inverses form a group under multiplication. This group has φ(n) elements. By Lagrange's theorem, d | φ(n), say dk = φ(n) for some integer k.

## Why this reference is here

The opening sentence is a masterclass in **positioning a theorem relative to what the reader already knows**. Rather than stating Euler's theorem first and explaining it, the article says "a generalization of Fermat's little theorem" — immediately locating the new result on the mental map next to an anchor the target reader almost certainly has. The second sentence names both the field context (elementary number theory) and the payoff application (RSA), so the reader knows why they should care before seeing any symbols.

The body then follows the **theorem → small-modulus instance → pattern-observation** shape. After the formal statement (a^φ(n) ≡ 1 (mod n)), the article works through specific moduli to let the reader see the congruence class structure concretely — multiplication by a permuting (ℤ/n)* — before abstracting to the group-theoretic proof via Lagrange. The reader meets the abstraction only after the pattern is visible in examples.

## Voice observations

- Opens by *relating* the concept, not defining it in isolation. "Generalization of X" is doing more work than a definition would.
- Math notation appears only after prose has established why the notation is needed. The totient function φ(n) is introduced inside a theorem statement, not as a prefatory definition.
- Proof sketches lean on motion verbs — "multiplication by a is a permutation of this set" — giving static algebraic objects a dynamic reading the reader can picture.
