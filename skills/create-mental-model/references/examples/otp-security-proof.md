---
type: concept
status: done
tags:
  - cryptography
created: 2026-04-01
sources: []
related: []
---
## Security Game

The adversary $\mathcal{A}$ picks two messages $m_0, m_1 \in \{0, 1\}$ and sends them to the challenger. The challenger samples $k \xleftarrow{\$} \{0, 1\}$ and $b \xleftarrow{\$} \{0, 1\}$, computes $c_b = k \oplus m_b$, and sends the ciphertext back to the adversary. The adversary then outputs a guess $b'$. We want to show that $\text{Adv}_{\mathcal{A}}^{\text{distinguishcipher}} = 0$ for the one-time pad.

## Setting Up the Probability

The advantage is defined in terms of $\Pr[b' = b]$. Expanding by cases on $b$:

$$
\begin{align*}
\Pr[b'=b] &= \Pr[b=1 \wedge b'=1] + \Pr[b=0 \wedge b'=0] \\
&= \Pr[b=1] \, \Pr[b'=1 \mid b=1] + \Pr[b=0] \, \Pr[b'=0 \mid b=0] \\
&= \tfrac{1}{2} \, \Pr[b'=1 \mid b=1] + \tfrac{1}{2} \, \Pr[b'=0 \mid b=0]
\end{align*}
$$

## Where I Got Stuck

I couldn't figure out how to reason about the two conditional probabilities $\Pr[b'=1 \mid b=1]$ and $\Pr[b'=0 \mid b=0]$, because the adversary is the one choosing $b'$. Depending on the adversary, it could always output $b'=1$, or always output $b'=0$, or flip a fair coin internally, or run some fancy function of the ciphertext. Since the proof needs to work for all adversaries, I didn't know how to assign a concrete value to those probabilities. They seemed completely under the adversary's control, not something I could calculate from the game description alone.

## The Key Move: Condition on the Key

The trick is to not think about what the adversary "decides" to do, but instead condition on the random variable the adversary actually sees, which is the ciphertext. And the ciphertext depends on the key $k$. Expanding $\Pr[b'=1 \mid b=1]$ by conditioning on $k$:

$$
\begin{align*}
\Pr[b' = 1 \mid b = 1] &= \Pr[\mathcal{A}(k \oplus m_1) = 1] \\
&= \Pr[k = 0] \cdot \Pr[\mathcal{A}(m_1) = 1] + \Pr[k = 1] \cdot \Pr[\mathcal{A}(1 \oplus m_1) = 1] \\
&= \frac{1}{2} \cdot \Pr[\mathcal{A}(m_1) = 1] + \frac{1}{2} \cdot \Pr[\mathcal{A}(1 \oplus m_1) = 1]
\end{align*}
$$

Similarly for the other term:

$$
\begin{align*}
\Pr[b' = 0 \mid b = 0] &= \Pr[\mathcal{A}(k \oplus m_0) = 0] \\
&= \Pr[k = 0] \cdot \Pr[\mathcal{A}(m_0) = 0] + \Pr[k = 1] \cdot \Pr[\mathcal{A}(1 \oplus m_0) = 0] \\
&= \frac{1}{2} \cdot \Pr[\mathcal{A}(m_0) = 0] + \frac{1}{2} \cdot \Pr[\mathcal{A}(1 \oplus m_0) = 0]
\end{align*}
$$

The adversary's behavior reduces to a deterministic function of its input. We don't need to know *what* the adversary does. We just need to know that for any fixed input $x$, $\Pr[\mathcal{A}(x) = 1] + \Pr[\mathcal{A}(x) = 0] = 1$.

## The Two Cases

**Claim:** $\Pr[b' = 1 \mid b = 1] + \Pr[b' = 0 \mid b = 0] = 1$, regardless of the adversary's strategy.

**Case 1:** The adversary chooses $m_0 = m_1$. Then $1 \oplus m_0 = 1 \oplus m_1$, so the matching pairs are:

- $\Pr[\mathcal{A}(m_1) = 1] + \Pr[\mathcal{A}(m_0) = 0] = 1$
- $\Pr[\mathcal{A}(1 \oplus m_1) = 1] + \Pr[\mathcal{A}(1 \oplus m_0) = 0] = 1$

**Case 2:** The adversary chooses $m_0 \ne m_1$. Since the message space is $\{0,1\}$, one message is 0 and the other is 1, so $m_1 = 1 \oplus m_0$. The matching pairs cross over:

- $\Pr[\mathcal{A}(m_1) = 1] + \Pr[\mathcal{A}(1 \oplus m_0) = 0] = 1$
- $\Pr[\mathcal{A}(1 \oplus m_1) = 1] + \Pr[\mathcal{A}(m_0) = 0] = 1$

In both cases, the weighted sum gives exactly 1. So:

$$
\begin{align*}
\Pr[b'=b] &= \tfrac{1}{2} \, \Pr[b'=1 \mid b=1] + \tfrac{1}{2} \, \Pr[b'=0 \mid b=0] \\
&= \tfrac{1}{2} \cdot 1 = \tfrac{1}{2}
\end{align*}
$$

The advantage is $2 \cdot \Pr[b'=b] - 1 = 0$. The one-time pad gives the adversary no information, no matter what strategy it uses.
