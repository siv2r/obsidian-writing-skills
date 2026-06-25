---
source: https://brilliant.org/wiki/diffie-hellman-protocol/
fetched: 2026-04-21
annotation-type: voice-exemplar
sources-team-review: "Curated by reviewer-brilliant during explainer-research team round (2026-04-20)."
---

# Diffie-Hellman Protocol (Brilliant wiki)

## Opening excerpt

> The **Diffie-Hellman protocol** is a scheme for exchanging information over a public channel. If two people (usually referred to in the cryptographic literature as Alice and Bob) wish to communicate securely, they need a way to exchange some information that will be known only to them. In practice, Alice and Bob are communicating remotely (e.g. over the internet) and have no prearranged way to exchange information.
>
> The main idea is that each of them has some secret information that is known only to them, which they combine into a suitable key, or password, which they can then use to set up a secure communication platform. The Diffie-Hellman protocol allows them to accomplish this even if an antagonist is monitoring their messages, as long as their secret information remains secret. The security of the protocol is based on the widely held belief that a certain computational number theory problem called the **discrete log problem** is sufficiently hard.

## Distinctive excerpt

> The prime p should be chosen so that the largest prime factor of p−1 is large [to prevent Pohlig-Hellman attacks].
>
> Eve can read every message between Alice and Bob, modify the messages before passing them along [via man-in-the-middle interception without solving discrete logarithms].
>
> As of 2016, the recommended size of a Diffie-Hellman modulus p to ensure security from state-of-the-art attacks is 2048 bits.

## Why this reference is here

This article is the cleanest example of the **problem-setup-before-mechanism** pattern in the reference set. The opening paragraph does not mention groups, generators, or modular exponentiation. It sets up the *situation*: two parties, a public channel, no prior shared secret. Only after the problem is visible — "they need a way to exchange some information that will be known only to them" — does the article introduce the conceptual move.

The second paragraph is the "**main idea**" paragraph, deliberately written in plain prose before any notation. It names the mechanism at the level of intention ("each of them has some secret information... which they combine into a suitable key") and states the security assumption in one line ("the widely held belief that... the discrete log problem is sufficiently hard"). The reader leaves two paragraphs in knowing *what the protocol does, against what adversary, under what assumption* — with no arithmetic yet. The later sections go on to modular arithmetic and close by pointing the reader toward the elliptic-curve generalization, which is how this kind of article should hand off to the next topic.

## Voice observations

- Prose-first, math-second pacing. The first 250 words explain the protocol with zero equations.
- The parenthetical "usually referred to in the cryptographic literature as Alice and Bob" teaches a convention in passing rather than stopping to define it. This is the right tone for a reader who may or may not have seen Alice/Bob before.
- Security statements are honest about their epistemic status ("widely held belief"). The article does not claim discrete log is hard; it reports that people believe it is.
