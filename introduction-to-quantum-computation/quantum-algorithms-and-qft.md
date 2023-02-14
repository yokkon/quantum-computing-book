# ⚒ Quantum Algorithms & QFT

Mathematical Representation of Quantum Fourier Transform

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
\sum_{j=0}^{N-1}x_j\ket j\rarr\sum_{k=0}^{N-1}y_k\ket k
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

The above product representation makes it easy to derive an efficient circuit for the quantum Fourier transform. Such a circuit is shown below.

## Quantum Circuit for Fourier Transform

As classic Fourier transform have many applications and influenced a lot of areas, so is the quantum version that brought a large number of quantum algorithms with the most known of them is Schor's algorithm for whole numbers factorization.

with quantum Fourier transform implementation we have as input the n qubit state $$\ket{j_1...j_n}$$ and we want to implement a quantum circle that will give us as output the Fourier transform of the state, so we use the above identity:

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>QFT as a tensor product of all elements</p></figcaption></figure>

to give us a clue of how to build the gates in our circuit.

So it becomes natural that we can compute the Fourier Transformation with some phase shifting gates in quantum computing. The gate $$R_k$$ denotes the unitary transformation:

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>phase shift gate</p></figcaption></figure>

we need to operate this gate on a few different qubits, while using different k's, in order to implement all the above exponents. we'll try implementing one element after another from the above multiplication.

we know that Hadamard gate has a big importance in quantum algorithms, since it creates superposition. so lets see what happens when we operate a Hadamard gate on the first qubit $$\ket{j_1}$$ when $$j_1=0$$ or $$j_1=1$$ the first bit of the initial quantum state $$\ket{j_1...j_n}$$, what we get is

$$
\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1}\ket1)\ket{j_2...j_n}
$$

since when $$j_1=0$$ the gate is activating on $$\ket0$$ and the result is $$\ket+$$ and when $$j_1=1$$ the gate activates on $$\ket1$$ and we get $$e^{2\pi i\frac12}=e^{\pi i}=cos\pi+isin\pi=-1$$ meaning $$\ket-$$ this is just a different way of writing the Hadamard's gate result and it takes us close to our wanted result.

now we need to make the next number after the period. appearently we can do it using activating controlled-R2 on the first 2 qubits in state $$\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1}\ket1)\ket{j_2...j_n}$$ and then we get:

$$
\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1j_2}\ket1)\ket{j_2...j_n}
$$

why specificaly controlled-$$R_2$$? the action is vital for all of the multiplication elements, $$\ket0$$ is not multplied by any exponent but $$\ket1$$ does multiplied (check again $$R_k$$ definition). the control and $$R_2$$ are making sure it will happen and also $$R_2$$ is the one that controls the second digit after the period. by the same logic we can continue until controlled-$$R_n$$ and then we get finally the result

$$
\frac{1}{\sqrt2}(\ket0+e^{2\pi i0.j_1j_2...j_n}\ket1)\ket{j_2...j_n}
$$

notice that now the parentheses above look like the ones from the QFT multiplication equation.

Now we need to act the same way on all the rest of the qubits in the quantum state $$j_1,...,j_n$$, in order to get the rest of the multiplied parts of the QFT result, the power of every exponent has one less digit after the period - the one that we already acted on in the previous step.

So for example on the second qubit we operate Hadamard and get:

$$
\frac{1}{2}(\ket0+e^{2\pi i0.j_1j_2...j_n}\ket1)(\ket0 +e^{2\pi i0.j_2}\ket1)\ket{j_3...j_n}
$$

We operate controled-$$R_2$$...controled-$$R_{n-1}$$ and we get&#x20;

$$
\frac{1}{2}(\ket0+e^{2\pi i0.j_1j_2...j_n}\ket1)(\ket0 +e^{2\pi i0.j_2j_3....j_n}\ket1)\ket{j_3...j_n}
$$

And this is how we got the second to last multiplied element, continuing the same operation on all qubits will result with

$$
\frac{1}{2^{n/2}}(\ket0+e^{2\pi i0.j_1j_2...j_n}\ket1)(\ket0 +e^{2\pi i0.j_2j_3....j_n}\ket1)...
\newline
(\ket0 +e^{2\pi i0.j_n}\ket1)
$$

The result is very familiar, because it's alsmost exactly the QFT result we derived before, using the SWAP gates to reverse the order of the qubits we will get the wanted result





$$
\frac{1}{2^{n/2}}
(\ket0 +e^{2\pi i0.j_n}\ket1)...
\newline
(\ket0 +e^{2\pi i0.j_2j_3....j_n}\ket1)+(\ket0+e^{2\pi i0.j_1j_2...j_n}\ket1)
$$

The below quantum circuit is the QFT algorithm without the SWAP gates

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>QFT Algorithm</p></figcaption></figure>

Notice that all of the gates in the circuit are Unitary meaning that the whole circle itself is Unitary.

## Matrix Representation of QFT

First we should use the face that moving from operator representation to matrix representation is done using $$A\rarr A_{ij}\space via\space A_{ij}=\bra i A\ket j$$. and since our QFT operator that performs the translation from space j to space k is of the form

$$
F = \sum_{j,k=0}^{N-1}\frac{e^{2\pi ijk/N}}{\sqrt N} \ket k \bra j
$$

then we can find the matrix representation by multiplying $$\ket k$$ from left side and $$\bra j$$ from right side adn we get this matrix

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>QFT Matrix Representation</p></figcaption></figure>

when $$\omega = e^{2\pi i/N}$$, for example we take $$N=4$$ and we get $$\omega=i$$ so the QFT matrix is&#x20;

<img src="../.gitbook/assets/image (7).png" alt="" data-size="original">

## Phase Estimation

TODO
