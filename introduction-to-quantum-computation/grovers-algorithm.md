---
description: >-
  we'll talk about Grover's search algorithm and some geometric contemplation
  over it to understand how and why it works
---

# Grover's Algorithm

## Readings

* [IBM Qiskit Grover's search algorithm explained](https://qiskit.org/textbook/ch-algorithms/grover.html)

## Grover's Search Algorithm

accelerates the solution of every classical problem that includes in it a seaarch or can be using search, including optimization, finding pairs, group divisions and even factorization.

the meaning of search is finding a special element (or a group of special elements) inside an array (no structure yet). assuming that the array size is $$N=2^n$$ and the element count that we want to find is $$1\le M \le N$$.

&#x20;in the classical way, we need to operate an oracle function to identify a special element $$N-1$$ times, while with Grover's quantum algorithm apparently $$O(\sqrt N)$$ is enough to find one special element and $$O(\sqrt {N/M})$$ is enough iterations for finding one special element out of M special elements in a N size group.

#### Oracle Description

like many quantum algorithms the algorithm is based on an _"Oracle"_ implementation - black box, that we don't necessarily know how it works, but it knows to answer for us on a specific question, and can be implemented in a quantum circuit as an Unitary gate. in our case the _Oracle_ knows to identify if an element in an array is the one that we're looking for, meaning $$f(x) = 1$$ if x is a solution and $$f(x) = 0$$ otherwise, and like Deutsch–Jozsa algorithm, it adds the value of $$f$$ to the destination qubit:

$$
\ket x\ket q \rarr\ket x\ket{q \oplus f(x)}
$$

meaning, the state $$\ket x$$ contains an element from the array and if it one of the elements we're looking for then the qubit $$\ket{q=0}$$ is changing into $$\ket {q=1}$$ and the other way around.

much like Deutsch–Jozsa algorithm, we prepare the _Oracle_ in a state:

$$
\ket - = \frac{(\ket0 - \ket1)}{\sqrt2}
$$

so that

$$
\ket x \left( \frac{\ket0 - \ket1}{\sqrt2}\right)  \rarr (-1)^{f(x)}\ket x \left( \frac{\ket0 - \ket1}{\sqrt2}\right)
$$

this way, we can say the minus belongs to the $$\ket x$$ and think that the state of the _Oracle_ didn't changed, so we can simplify this to:

$$
\ket x \rarr (-1)^{f(x)}\ket x
$$

notice that the _Oracle_ doesn't know ahead of time what is the solution to the search problem, but it knows to identify a solution once it gets it as input.

#### Algorithm Description

like many other algorithms, Grover's algorithm starts with the state $${\ket0}^{\otimes n}$$ and operate n Hadamard gates on it:

$$
\ket\psi=\frac{1}{\sqrt N}\sum_{x=0}^{N-1}\ket x
$$

that spans $$N=2^n$$ possibilities (can also be thinking of as different places where the element we're looking for is at).

the algorithm proceeds by operating a subroutine, called **Grover's iteration** and is marked with G, for $$\sqrt N$$ times and ends as usual with measurement. schematically it looks like:

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption><p>Grover's search algorithm scheme</p></figcaption></figure>

the G operation is constructed from 4 steps:

1. operating _Oracle_ to "mark" possible solutions
2. operating n Hadamard gates again to get back to the computational basis
3. phase inverse of all qubits except state $$\ket 0$$ phase, meaning $$\ket x \rarr -(-1)^{\delta_{x0}}\ket x$$\
   (notice that the meaning of state $$\ket0$$ is $$\ket0^{\otimes n}$$)
4. operating n Hadamard gates again to get back to the "big" solution space of N

the routine should look like this:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>G operation routine</p></figcaption></figure>

what happens in steps 2-4 is basically:

$$
H^{\otimes n}\left( 2\ket0 
\bra0 - I \right)H^{\otimes n}=2\ket0 
\bra0 - I
$$

(again notice that the meaning of state $$\ket0$$ is $$\ket0^{\otimes n}$$)

why does step 3 looks like that?

first of all, what's written in the parenthesis is doing on the computational basis the below effect:

$$
(2\ket0 \bra 0 - I)\ket0=2\ket0 \bra 0 \ket 0 - \ket 0 = \ket 0
$$

$$
(2\ket0 \bra 0 - I)\ket1=2\ket0 \bra 0 \ket 1 - \ket 1 = -\ket 1
$$

meaning, a reflecting process around 0, and then in Hadamard basis n 0's are turning into $$\ket\psi$$ as we defined above $$\ket\psi=\frac{1}{\sqrt N}\sum_{x=0}^{N-1}\ket x$$.

using step 1 we get:

$$
G=\left( 2\ket\psi
\bra\psi - I \right)O
$$

and the best way to understand what happened in here and why this is working, is examineing it geometrically.

#### Geometrically Looking on Grover's Algorithm

our purpose is to show that the operator G is for the matter of a fact a rotation operator that every iteration approximates the initial vector that contains a superposition of all elements to a vector of solutions that contains only the wanted elements.

we define two new wrtings:

* $$\sum_{x}^{'}$$ summing over all x's that are solutions
* $$\sum_{x}^{''}$$ summing over all x's that are not solutions

now lets define the superposition of the $$M$$ solutions and the $$N-M$$ not solutions:

$$
\ket\alpha \equiv \frac{1}{\sqrt{N-M}} \sum_{x}^{''}\ket x
$$

$$
\ket\beta \equiv \frac{1}{\sqrt{M}} \sum_{x}^{'}\ket x
$$

those two states above are obviously spanning the initial state that is a superposition of all elements:

$$
\ket\psi=\sqrt{\frac{N-M}{N}}\ket\alpha+\sqrt{\frac{M}{N}}\ket\beta
$$

these above definitions allow us to describe the _Grover iteration_ on a plane:

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Grover iteration on a plane</p></figcaption></figure>

now we can identify that operator _O_ is doing reflection of the initial state $$\ket\psi$$ respectively to the $$\ket\alpha$$ axis, meaning:

$$
O\left( a\ket\alpha + b\ket\beta \right)=a\ket\alpha - b\ket\beta
$$

because it multiplies with minus every solution element.

in addition, the operator $$2\ket\psi \bra\psi - I$$ is a reflection operator respectively to the initial state $$\ket\psi$$.

why is that? because for every state $$\ket\phi = c\ket\psi+d\ket{\psi_\perp}$$ the following takes place:

$$
\left( 2\ket\psi
\bra\psi - I \right)\ket\phi=\left( 2\ket\psi
\bra\psi - I \right)\left( c\ket\psi+d\ket{\psi_\perp} \right)
$$

$$
=2c\ket\psi-c\ket\psi-d\ket{\psi_\perp}=c\ket\psi-d\ket{\psi_\perp}
$$

multiplication of those two reflections is equal to a rotation in the same plane that approximate the original guess to the solutions state vector.

now we're going to write:

$$
\ket\psi=\cos\frac{\theta}{2}\ket\alpha+\sin\frac{\theta}{2}\ket\beta
$$

when

$$
\cos\frac{\theta}{2}=\sqrt{\frac{N-M}{N}},\space \sin\frac{\theta}{2}=\sqrt{\frac{M}{N}}
$$

so from the geometric illustration on the plane we can see

$$
G\ket\psi=\cos\frac{3\theta}{2}\ket\alpha+\sin\frac{3\theta}{2}\ket\beta
$$

using Grover iteration k times we get

$$
G^k\ket\psi=\cos\left(\frac{2k+1}{2}\theta\right)\ket\alpha+\sin\left(\frac{2k+1}{2}\theta\right)\ket\beta
$$

{% embed url="https://www.youtube.com/watch?v=mrtJiDI_TAA" %}
Grover's Algorithm Visualization
{% endembed %}

the initial angle between initial state $$\ket\psi$$ and solution state $$\ket\beta$$ is $$\sqrt\frac{M}{N}$$ so generally to get to solution we need to rotate our initial state $$\arccos\sqrt{M/N}$$ radians towards $$\ket\beta$$. if every iteration the rotation is of $$\theta$$ then in total we need R rotations:

$$
R=Round\left( \frac{\arccos\sqrt{M/N}}{\theta} \right)
$$

where _Round_ give us the closest round number to the value we get in the fraction. a common situation is when $$N >> M$$ we get $$\theta\approx\sin\theta\approx2\sqrt{M/N}$$.

we can sum it all up with the actual algorithm description

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Grover's Quantum search Algorithm</p></figcaption></figure>
