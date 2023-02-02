# ⚒ Quantum Algorithms & QFT

## Mathematical Representation of Quantum Fourier Transform

Classic discrete Fourier transform can be represented by:

$$
y_k=\frac{1}{\sqrt{N}}\sum_{j=0}^{N-1}x_je^{2\pi ijk/N}
$$

when x and y are both complex vectors with N elements.

the **quantum** Fourier transform is pretty similar, only that we use the bra-ket notation and an orthonormal basis $$\ket 0,.....,\ket{N-1}$$ .

$$
\ket j=\frac{1}{\sqrt{N}}\sum_{k=0}^{N-1}e^{2\pi ijk/N} \ket k
$$

meaning that the same relation between the vectors x and y stayed valid, only now they are multiplying by a quantum state

$$
\sum_{j=0}^{N-1}x_j\ket j\rarr\sum_{j=0}^{N-1}y_k\ket k
$$

here's an illustration of the QFT process that will help get a better understanding

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>delta function should be transformed to a sinusoidal function</p></figcaption></figure>

now we're going to use a binary basis defined with $$N=2^n$$, and $$\ket j$$ will be represented in a binary representation:

$$
j=j_1j_2...j_n=j_12^{n-1}+j_22^{n-2}+...+j_n2^0
$$

$$
0.j_lj_{l+1}...j_m=j_l/2+j_{l+1}/4+...+j_m/2^{m-l+1}
$$

if $$k$$ is a binary represented number then we get do this algebra

$$
k/2^n=\sum_{l=1}^{n}k_i2^{-l}
$$

using this representations of $$j,k$$ we can write the sum that describe the above Fourier transform as the following multiplication

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>main identity of the QFT implementation - performing QFT iteratively</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>QFT as a tensor product of all elements</p></figcaption></figure>

## Quantum Circuit for Fourier Transform

As classic Fourier transform have many applications and influenced a lot of areas, so is the quantum version that brought a large number of quantum algorithms with the most known of them is Schor's algorithm for whole numbers factorization.

with quantum fourier transform implementation we have as input the n qubit state $$\ket{j_1...j_n}$$ and we want to implement a quantum circle that will give us as ooutput the fourier transform of the state, so we use the above identity:

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>QFT as a tensor product of all elements</p></figcaption></figure>

to give us a clue of how to build the gates in our circuit.

So it becomes natural that we can compute the Fourier Transformation with some phase shifting gates in quantum computing.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>phase shift gate</p></figcaption></figure>

we need to operate this gate on a few different qubits, while using different k's, in order to implement all the above exponents. we'll try implementing one element after another from the above multiplication.

we know that Hadamard gate has a big importence in quantum algorithms, since it creates superposition. so lets see what happens when we operate a Hadamard gate on the first qubit $$\ket{j_1}$$ when $$j_1=0$$ or $$j_1=1$$ the first bit oef the initial quantum state $$\ket{j_1...j_n}$$, what we get is

$$
\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1}\ket1)\ket{j_2...j_n}
$$

since when $$j_1=0$$ the gate is activating on $$\ket0$$ and the result is $$\ket+$$ and when $$j_1=1$$ the gate activates on $$\ket1$$ and we get $$e^{2\pi i\frac12}=e^{\pi i}=cos\pi+isin\pi=-1$$ meaning $$\ket-$$ this is just a different way of writing the Hadamard's gate result and it takes us close to our wanted result.

now we need to make the next number after the period. appearently we can do it using activating controlled-R2 on the first 2 qubits in state $$\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1}\ket1)\ket{j_2...j_n}$$ and then we get:

$$
\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1j_2}\ket1)\ket{j_2...j_n}
$$

why specificaly controlled-R2? the action is vital for all of the multiplication elements, $$\ket0$$ is not multplied in any exponent but $$\ket1$$ is. the control and R2 are making sure it will happen and also R2 is the one that controls the second digit after the period. by the same logic we can continue until controlled-Rn and then we get finally the result

$$
\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1j_2...j_n}\ket1)\ket{j_2...j_n}
$$

notice that now the parentheses above look like the ones from the QFT multiplication equation.
