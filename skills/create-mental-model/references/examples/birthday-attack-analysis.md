---
type: blog
status: published
tags:
  - cryptography
created: 2026-04-01
publish-target: substack
related: []
---
The Birthday Attack is a way for someone to try and find two different things that would produce the same result when put through a black box. Usually, this black box is a **hash function**, often used to keep information secret and safe, like a password. If someone can find two different things that give the same result (i.e., can find a **hash collision**), they could trick a system into thinking they know the secret information.

Finding a hash collision (efficiently) can lead to terrible things. For example, The **Flame** malware, which was used in cyber-spying Middle Eastern countries, was signed with a fraudulent certificate to make it appear to have originated from Microsoft. This was possible because they found a hash collision in MD5. You can learn more about it in this [StackExchange thread](https://crypto.stackexchange.com/questions/44151/how-does-the-flame-malware-take-advantage-of-md5-collision).

In this week's issue, we will look at the underlying principle of the birthday attack and derive a formula to help us compute the probability of finding a hash collision (in an *n*-bit hash function).

![[birthday-attack-xkcd-purity.webp]]

## The Birthday Paradox

The birthday attack is based on the principle of the birthday paradox, which is a strange phenomenon that has to do with the probability of two people having the same birthday in a group. Here's how it works:

Consider a group of 23 people. What are the chances that at least two group members have the same birthday? It might seem like the chances are low, but actually, it's more likely than you might think! In fact, there's a greater than 50% chance that at least two people in the group will have the same birthday. Not very intuitive, right? That's why it is called a paradox.

### Mathematical Formulation

What happens if there are 20, 50, or even 300 people in the group? How much will the  probability be, then? To calculate it, let's first formulate the problem mathematically.

Consider a group of *n* people. What is the probability that at least two group members have the same birthday? Assuming [1] no leap year, and [2] people's birthdays are distributed uniformly throughout the year.

## Paradox Solved: The Solution

> In this section, The *^* symbol means *"raised to the power"*, not *"xor"* (*2^3 = 8*, not *1*).

***Case 1:*** If *n > 365*, Since the number of people in the group, is greater than the number of days in a year. By the pigeonhole principle, there will always be at least two people born on the same day ⇒ *P(n) = 1.*

***Case 2:*** If *n ≤ 365*, Trying to compute probability straightforwardly will become tedious since there are many subcases to consider, which are [1] exactly two people having same birthday, [2] exactly three people having same birthday, and so on till exactly *n* people having same birthday. Instead of finding the probability for each subcase and adding them, We can use a much simpler technique here.

Let *P'(n)* be the probability that **no two people** have the same birthday. This is the complement of *P(n)*, which is at least two people have the same birthday. So, we can write:

$$p(n) = 1 - p'(n)$$

If we can compute *P'(n)*, we can find our required probability by subtracting it from 1. How to calculate *P'(n)*, then?

As with most simple probability problems, we can find *P'(n)* by dividing [1] favorable outcomes and [2] total possible outcomes (aka sample space).

1. For favorable outcomes, the first person can have 365 days as their birthday. The second person can have *364(=365-1)* days as their birthday (excludes the first person's birthday). Similarly, the third person can have *363(=365-2)* days as their birthday. And so on till the *n*-th person. **So, favorable outcomes** *= (365).(364).(363)… n* times = *(365).(364).(363)…(365-n+1).*
2. Each person (out of *n*) can have 365 days as their birthday. So, the total possible outcome = *(365).(365).(365) … n* times= *365^n*.

$$
\begin{equation*}
\begin{split}
p'(n) &= \frac{365 \times 364 \times 363 \times ... \times (365-n+1)}{365^n}\\
 &= \frac{365!}{365^n\times(365-n)!}
\end{split}
\end{equation*}
$$

Now, we can compute *P(n)* by

$$
\begin{equation*}
\begin{split}
p(n) &= 1 - p'(n)\\
     &= 1 - \frac{365!}{365^n\times(365-n)!}\\
\end{split}
\end{equation*}
$$

The graph below plots *P(n)* as the value of *n* increases.

![[birthday-attack-probability-graph.png]]

From the graph, we can observe that with just 23 people, there is a 50% chance that at least two people have the same birthday. And with 100 people, there is *almost* a 100% chance. So, the next time you visit any conference, it might not take much effort to find your birthday twin (ツ).

### Approximation

we have derived a formula for *P(n)* that contains *(356-n)!* In the denominator. Solving an equation (or inequality) involving an unknown factorial is problematic. So, we usually reduce these equations to a simpler form by approximating the unknown factorial (see [Stirling's approximation](https://math.stackexchange.com/questions/61755/is-there-a-way-to-solve-for-an-unknown-in-a-factorial)). Then we can apply standard algebraic techniques to the approximated form.

Let's do it! If we look at the above graph, it resembles an exponential function. So, we might be able to approximate our formula to some variation of *e^x.*

The Taylor series expansion for $e^{-x}$ is as follows.

$$
\begin{equation*}
\begin{split}
e^{-x} &= 1 - x + \frac{x^2}{2!} - \frac{x^3}{3!} + \frac{x^4}{4!} \;.\;.\;.\; \infty\\
e^{-x} &\approx 1 - x
\end{split}
\end{equation*}
$$

We can ignore the higher powers of *x* (*x^2*, *x^3,* … inf) to keep our approximation simple. Now, we can simplify our *P'(n)* formula using the above result.

$$
\begin{equation*}
\begin{split}
p'(n) &= \frac{365\times364\times ... \times (365 - (n-1))}{365^n}\\
&= \frac{365}{365} \times \frac{364}{365} \times ... \times \frac{365-(n-1)}{365}\\
&=(1)\times(1 - \frac{1}{365})\times(1-\frac{2}{365})\times ...\times(1-\frac{n-1}{365})\\
&\approx(1) \times(e^{-\frac{1}{365}})\times(e^{-\frac{2}{365}}) \times...\times(e^{-\frac{n-1}{365}})\\
&\approx e^{-\frac{1+2+3+ ...+ n-1}{365}}\\
&\approx e^{-\frac{(n-1)\times n}{2\times365}}\\
&\approx e^{-\frac{n^2}{2\times365}}\\
\end{split}
\end{equation*}
$$

We can substitute the above approximation in *P(n)* for our final result.

$$
\begin{equation*}
\begin{split}
p(n) &= 1-p'(n)\\
&\approx 1 - e^{-\frac{n^2}{2\times365}}\\
\end{split}
\end{equation*}
$$

We have finally removed the unknown factorial from our formula by approximating it. We can now easily apply standard algebraic techniques in our new formula. Let's take a look at an example.

### Minimum Group Size

Find the minimum group size such that the probability of at least two people having the same birthday is greater than 50%. From the graph, the answer is 23. But let's find this using our newly approximated formula for *P(n)*.

We can mathematically formulate the above question as finding minimum *n* such that:

$$p(n) \ge 0.5$$

Let's substitute our approximated formula here.

$$
\begin{equation*}
\begin{split}
1 - e^{-\frac{n^2}{2\times365}} &\ge \frac{1}{2}\\
e^{-\frac{n^2}{2\times365}} &\le \frac{1}{2}\\
\ln({e^{-\frac{n^2}{2\times365}}}) &\le \ln({\frac{1}{2}})\\
-\frac{n^2}{2\times365} &\le -\ln2\\
n &\ge \sqrt{2\times365\times\ln2}\\
n &\ge 22.4943
\end{split}
\end{equation*}
$$

The smallest integer value of *n* satisfying our result is 23. See how easy it was. Imagine solving the above inequality using our factorial formula. It would be a nightmare (¬_¬).

### Generalized Results

Though we have derived the probability formula for a year with 365 days, it can be generalized for a year with *d* days. To find such a generalization, we replace 365 with the variable *d*.

$$p(n, d) = 1 - e^{-\frac{n^2}{2\times d}}$$

We can also generalize the minimum group size formula.

$$n(d, p) = \left \lceil {\sqrt{2\times d\times \ln\frac{1}{1-p}}}\;\;\right \rceil$$

The formula above tells us the minimum group size such that the probability of at least two people having the same birthday (in a year with *d* days) is greater than *p.*

The above two formulas are the main takeaways. But if you are curious, there is a more accurate approximation for minimum group size for a 50% chance, which looks like this.

$$n(d, 0.5) = \left \lceil {\sqrt{2d\ln2}} \;+\frac{3-2\ln2}{6}\;+\;\frac{9-4(\ln2)^2}{72\sqrt{2d\ln2}}\;-\frac{2(\ln2)^2}{135d} \;\;\right \rceil$$

The minimum group size approximation we derived contained only the first term of this more accurate approximation. I honestly don't dare to attempt deriving such a complicated formula, but if you are interested, you can read more about it in [this research paper](https://link.springer.com/content/pdf/10.1007/s11139-011-9343-9.pdf).

## The Birthday Attack

An *n*-bit hash function means the size of its output hash is *n*-bits. In other words, it can produce *2^n* distinct output values (i.e., each bit of those *n-bit*s can take any two values, 0 or 1). For example, MD5 is a 128-bit hash.

At first glance, it might seem as if we need to loop through more than *2^n* inputs to find a hash collision (by pigeonhole principle). But with birthday paradox logic, we can reason that it would take less than *2^n* inputs to find a hash collision (with a significant success rate).

To better understand the similarities between the hash collision and the birthday paradox. Let's try to rephrase the hash collision problem to our birthday problem.

*Rephrased Problem:* Find the minimum group size such that the probability of at least two people (= two inputs to the hash function) having the same birthday (= same hash value) is greater than 50%. Assume that a year has *d* days (= total no of possible hashes = *2^n*).

We have already derived a formula for finding such a minimum group size. So, substitute the hash collision problem's parameters there.

$$
\begin{equation*}
\begin{split}
n(d, p) &\approx \left \lceil {\sqrt{2\times d\times \ln\frac{1}{1-p}}}\;\;\right \rceil\\
&\approx \left \lceil {\sqrt{2\times 2^n\times \ln\frac{1}{1-0.5}}}\;\;\right \rceil\\
&\approx \left \lceil {\sqrt{2\times \ln2}} \;\times2^{n/2}\;\;\right \rceil\\
&\approx \left \lceil c\times2^{n/2}\;\;\right \rceil\\
\end{split}
\end{equation*}
$$

Our result says that after going through *2^{n/2}* inputs, there is a 50% chance we will find a hash collision. Hence, we only need to loop through some possible inputs, not all.

### Modified Birthday Attacks

The attack described above is a naive birthday attack. It is also called the classical collision attack. We can develop more sophisticated attacks by modifying the birthday attack depending on the use case. Below are some exciting attacks that build on top of the birthday problem.

- Digital Signature Susceptibility - [link](https://en.wikipedia.org/wiki/Birthday_attack#Digital_signature_susceptibility)
- Chosen-prefix Collision Attack - [link](https://en.wikipedia.org/wiki/Collision_attack#Chosen-prefix_collision_attack)
- Pollard's Rho Algorithm - [link](https://en.wikipedia.org/wiki/Pollard%27s_rho_algorithm)
- Pollard's Rho Algorithm for logarithms - [link](https://en.wikipedia.org/wiki/Pollard%27s_rho_algorithm_for_logarithms)

### Attack Execution Time

Let me ask you a question. If we can perform the birthday attack on a hash function, does this mean the hash function is broken? Take some time to think about it before reading further. No, it does not mean the hash function is broken. In fact, we can perform a birthday attack on any given hash function. What matters is the feasibility of the attack (resources required + time taken).

We have derived that a naive birthday attack on an *n-bit* hash function takes *2^{n/2}* operations for a 50% success rate. But how to compute the execution time for this attack? The execution time depends on your computer. The more powerful your machine is, the faster the attack will be.

For example, let me calculate the time it will take to execute a naive birthday attack on the MD5 hash function using my laptop, which has an Intel i7-9750H processor (= 4GHz) and 6 CPU cores.

$$\text{CPU Time} = \frac{\text{I} \;\times \text{CPI}}{\text{Frequency}} \;\,\text{seconds}$$

Here, *I =* number of instructions and *CPI =* avg clocks per instruction. MD5 is a 128-bit hash function, so our birthday attack performs at least 2^{64} operations. For simplicity, let's take *CPI = 1*.

$$
\begin{equation*}
\begin{split}
\text{CPU Time} &= \frac{2^{64} \times 1}{4\times10^9\times6}\\
&\approx 2^{29.517} \;\text{s}\\
&\approx 24.3 \;\, \text{years}
\end{split}
\end{equation*}
$$

My computer will take 24 years to find a hash collision at a 50% success rate. From this calculation, MD5 might seem secure. But it is not! There exist specialized attacks on MD5 that take less than a second to execute, even on regular computers. So, don't use this hash function in production.

Below are some related StackExchange threads:

- Execution time (of the above attack) on supercomputers - [link](https://crypto.stackexchange.com/questions/63536/how-reassuring-is-64-bit-insecurity)
- What does *n-bit* security mean in practice - [link](https://crypto.stackexchange.com/questions/79834/80-bit-security-and-attack-time)

## Conclusion

The birthday attack is probabilistic. The same goes for the formulas we derived. This means we can only estimate values (execution time or operations required) to a certain probability. But won't know the exact outcome unless executed. It is very similar to tossing a coin. We know that "heads" can occur with a 50% probability, but we won't know the value (heads or tails) unless we toss the coin.

Thank you for reading till the end. I hope that you found the content informative and worthwhile. If you have any questions, please feel free to leave a comment or reach out to me.

Bon Voyage!

![[birthday-attack-goodbye-meme.jpeg]]
