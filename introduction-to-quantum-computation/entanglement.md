# ⚒ Entanglement

## Content

* Bell theorem and the EPR
* quantum correlations and inequalities, CHSH
* Mermin Peres magic square
* GHZ paradox
* how to identify entanglement

## EPR Paradox

written by Einstein, Podolsky and Rosen (1935).\
first they define something called "element of reality" - a trait that we can know with certainty without interfering the system in any way - and now we ask ourself is quantum theory a whole? meaning, is it giving a consistent explenation to all of reality's elements.

the writers discussed continues variables like position and momentum, but we're going to talk about discrete variables.

lets give Alice and Bob to share a quantum state $$\ket{\psi^-}=\frac{\ket{01}-\ket{10}}{\sqrt2}$$, if both of them are measuring their qubits in the computational basis, the eigen vectors of the Z-Paulli $$\ket0,\ket1$$, then it's easy to see they are going to get the opposite results.\
this statement is generally true:

**argument:** consider the state $$\ket{\psi^-}$$ so for every direction choice $$\hat{v}$$ that Alice will choose to measure the qbuit at, i.e $$\vec{\sigma} \cdot \hat{v}$$, Bob will get the opposite result. \
\
**proof:** we can write the eigen vectors of $$\vec{\sigma} \cdot \hat{v}$$ with $$\ket{a},\ket{b}$$ and get

$$
\ket0=\alpha\ket{a}+\beta\ket{b}
$$

$$
\ket1=\gamma\ket{a}+\delta\ket{b}
$$

$$
\frac{\ket{01}-\ket{10}}{\sqrt2} \rarr (\alpha\gamma-\beta\delta) \rarr \frac{\ket{ab}-\ket{ba}}{\sqrt2}
$$

for evevry direction Alice will measure her qubit she can infer by the result Bob's result on the same direction of measurement (the opposite of Alice's result) - even if Bob and Alice are far away from each other. meaning that Bob's result is "elements of reality" because Alice knows it without interfere with Bob.

now EPR arguing that those elements cannot be described by quantum theory. since if Alice measures in $$\hat{z}$$ and Bob in $$\hat{x}$$ then we can know at the same time the spin in both directions, and this contradicts the uncerteinty principle. thus the researches conclude that the theory is not a whole since we have a clash between quantum theory to relativity theory (2 far points can not affect each other faster then the speed of light).

what stands behind EPR's wanted description for the phenomena is a group of so called hidden variables $$\{\lambda\}$$, that are not exposed to us and the quantum theory does not describe them, but they were defined and they are responsible for the corellation between the results of entangled states.

&#x20;

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>hidden variables illustration</p></figcaption></figure>

today we believe that EPR were wrong in this classical-local description, and we believe that the quantum theory is non-local in its nature but still can't allow communication faster then the speed of light. the hidden variables description that EPR wanted is not consistent with quantum theory, but there's still no contradiction with relativity principle.

## Bell's Experiment

Bell tried to give a mathematical expression for Einstein's expectation. the expectation, as we said, was that entangled states $$\ket{\psi^-}$$ can be explained by hidden variables. those hidden variables will hold predefined values, according to each decision of Alice and Bob without the result of either one of them to affect the result of the other.

To obtain Bell’s inequality, we’re going to do a thought experiment, which we will analyze using our common sense notions of how the world works. After we have done the common sense analysis, we will perform a quantum mechanical analysis which we can show is not consistent with the common sense analysis.

Imagine we perform the following experiment:

1. Charlie prepares two particles. It doesn’t matter how he prepares the particles, just that he is capable of repeating the experimental procedure which he uses.
2. Once he has performed the preparation, he sends one particle to Alice, and the second particle to Bob.
3. Once Alice receives her particle, she performs a measurement on it. Imagine that she has available two different measurement apparatuses, so she could choose to do one of two different measurements.\
   These measurements are of physical properties which we shall label PQ and PR, respectively. Alice doesn’t know in advance which measurement she will choose to perform. Rather, when she receives the particle she flips a coin or uses some other random method to decide which measurement to perform. We suppose for simplicity that the measurements can each have one of two outcomes, +1 or −1.\
   Suppose Alice’s particle has a value Q for the property $$P_Q$$. Q is assumed to be an objective property of Alice’s particle, which is merely revealed by the measurement, Similarly, let R denote the value revealed by a measurement of the property $$P_R$$.
4. Similarly, suppose that Bob is capable of measuring one of two properties, $$P_S$$ or $$P_T$$, once again revealing an objectively existing value S or T for the property, each taking value +1 or −1. Bob does not decide beforehand which property he will measure, but waits until he has received the particle and then chooses randomly.

The timing of the experiment is arranged so that Alice and Bob do their measurements at the same time, Therefore, the measurement which Alice performs cannot disturb the result of Bob’s measurement (or vice versa), since physical influences cannot propagate faster than light.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Bell's experiment illustration</p></figcaption></figure>

It's time for some algebra:

$$
QS+RS+RT-QT=S\left( Q + R \right) + T\left( R - Q \right)
$$

Because $$R,Q=\pm1$$ it follows that either



