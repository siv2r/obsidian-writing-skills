---
type: mental-model
status: done
tags:
  - cryptography
  - frost
created: 2026-03-31
sources:
  - "https://x.com/siv2r/status/1870487837541646601"
  - "https://github.com/siv2r/bip-frost-signing/issues/41"
  - "https://eprint.iacr.org/2024/436.pdf"
related:
  - "[[frost-signing-bip]]"
---

>[!info]
> In a $t$-of-$n$ Shamir secret sharing scheme, if you add a constant $t$ to every share, the reconstructed secret shifts by exactly $t$.

This is the property that makes "agnostic tweaking" work in FROST/ChillDKG — each signer can independently add the tweak to their own share, and the combined signature just works, no coordinator correction needed.

## The Math behind it

Suppose we have $u$ signing participants with secret shares $\{s_1, s_2, \ldots, s_u\}$ that reconstruct the secret $s$ via Lagrange interpolation:

$$s = f(0) = \sum_{i=1}^{u} \lambda_i \cdot s_i$$

If we offset each share by $t$ and reconstruct:

$$
\begin{align*}
\sum_{i=1}^{u} \lambda_i \cdot (s_i + t) &= \sum_{i=1}^{u} \lambda_i \cdot s_i + t \cdot \sum_{i=1}^{u} \lambda_i \\
&= s + t \cdot \sum_{i=1}^{u} \lambda_i
\end{align*}
$$

So the whole question reduces to: what's the value of $\sum_{i=1}^{u} \lambda_i$?

### Coefficients sum to 1

Consider the set of points $\{(x_1, 1), (x_2, 1), \ldots, (x_u, 1)\}$. All y-values are 1, so the unique interpolating polynomial is the constant function $f(x) = 1$. Evaluating at $x = 0$:

$$f(0) = \sum_{i=1}^{u} \lambda_i \cdot 1 = \sum_{i=1}^{u} \lambda_i = 1$$

The Lagrange basis polynomials $\lambda_i = \prod_{j \neq i} \frac{x_j}{x_j - x_i}$ are defined so they interpolate any set of y-values. When every y-value is the same constant, the interpolation just returns that constant. That's all this is.

$$\Rightarrow \sum_{i=1}^{u} \lambda_i \cdot (s_i + t) = s + t$$

![[lagrange-offset-property.jpg]]

## Why this matters for FROST tweaking

In BIP327-style tweaking (used by MuSig2 and current BIP445 draft), the tweak responsibility is split: signers adjust their share by a sign flip `gacc`, and the coordinator applies a correction `e * g * tacc` during partial signature aggregation. This couples signing with tweaking.

The offset property enables "agnostic tweaking": each signer adds the full tweak to their own secret share *before* signing. Since Lagrange coefficients sum to 1, the reconstructed tweaked secret is exactly $s + t$ — no coordinator correction needed. The signing protocol doesn't even know tweaking happened.

## Why this doesn't work for MuSig2

MuSig2 uses key aggregation coefficients $a_i = H(L, X_i)$, not Lagrange coefficients. There's no reason for $\sum a_i = 1$ — the hash function doesn't have this structure. So you can't just add a tweak to each key share and expect the aggregate to shift by the same tweak.