# Tensor Product

## Content

* 2 and 3 qubits systems - mathematical presentation and gates
* the basics of quantum entanglement&#x20;
* reduced density matrix

## 2 and 3 Qubits Systems

Assuming that $$H_A$$ is a Hilbert space for system $$A$$ and $$H_B$$ is a Hilbert space for system $$B$$, we can define the **tensor product** of those spaces as $$H_A \dotcross$$$$H_A\otimes H_B$$ and this space contains all the dual-particle states where one particle is from system $$A$$ and the second one from system $$B$$.\
Hence if $$\{\ket i_A\}_{i=1...n}$$ is the basis of $$H_A$$ and $$\{\ket j_B\}_{j=1...m}$$ is the basis of $$H_B$$ then $$\{\ket i_A \ket j_B\}_{i=1...n,j=1...m}$$is the basis of the tensor product of the two spaces $$H_A\otimes H_B$$ with $$m \times n$$ vectors in the basis.

Notice that $$\ket i_A \ket j_B$$ is a short way of writing $$\ket i_A \otimes \ket j_B$$ which sometimes being written as $$\ket i \ket j$$ and even $$\ket {ij}$$ - this is the dual particle state.

For example if system $$A$$ has a basis of $$\{\ket0_A=\begin{pmatrix}1\\0\end{pmatrix}\ket1_A=\begin{pmatrix}0\\1\end{pmatrix}\}$$ and system $$B$$ has a basis of $$\{\ket0_B=\begin{pmatrix}1\\0\end{pmatrix}\ket1_B=\begin{pmatrix}0\\1\end{pmatrix}\}$$ then the basis of the tensor product is $$\{\ket{00}=\begin{pmatrix}1\\0\\0\\0\end{pmatrix}\ket{01}=\begin{pmatrix}0\\1\\0\\0\end{pmatrix}\ \ket{10}=\begin{pmatrix}0\\0\\1\\0\end{pmatrix}\ket{11}=\begin{pmatrix}0\\0\\0\\1\end{pmatrix}\}$$\
and we can use it to write every dual particle state.

#### CNOT Gate

TODO

#### SWAP Gate

TODO

#### Toffoli Gate

TODO

#### Fredkin gate

TODO

## Quantum Enatanglement

TODO

## Reduced Density Matrix

How can we still describe the particle in our laboratory regardless of what the other side holds and regardless of the actions it does on its particle? Mathematically, we can run a **partial trace** on the total state that will give us a **reduced density matrix**. This description will be valid only for our particle and will be able to correctly predict the results in our laboratory.

_**Partial Trace**_: Assume that we have a complete description of the two-particle system $$\rho^{AB}$$. the reduced density matrix that A holds is&#x20;

$$
\rho^A=\sum_j{\bra j_B(\ket\psi\bra\psi)\ket j_B}=Tr_B \rho_T
$$

