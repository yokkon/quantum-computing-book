# ⚒ Variational Quantum Eigensolver

## Readings

* [A Variational Eigenvalue Solver on a Quantum Processor](https://arxiv.org/abs/1304.3061)
* [The Variational Quantum Eigensolver: a review of methods and best practices](https://arxiv.org/abs/2111.05176)

## Variational Quantum Eigensolver

The VQE is a PQC based algorithm that aims to find the smallest eigenvalue (lowest energy) of a problem hamiltonian.\
The variational part of the algorithm refers to the systematic search for the best possible approximation of the ground state by trying various PQC _"ansatze"_ and configurations of adjustable PQC params_._&#x20;

## The Variational Approach

The process of finding an optimal configuration of PQC params is called learning when dealing with QML use cases.\
This learning can be done either in a non differentiable way but it always consists of the minimization of some cost function through varying the adjustable circuit parameters.\
The characheristics equation for the hamiltonian $$H$$ is&#x20;

$$
H\ket{\psi_i}=E_i\ket{\psi_i}
$$

where $$\psi_i$$ is the eigenstate associated with the eigenvalue $$E_i$$, **our objective is to find the smallest eigenvalue** $$E_0$$ **of** $$H$$ **corresponding to the ground state**  $$\ket{\psi_0}$$.\
This task would be very easy if $$\ket{\psi_0}$$ was known since the eigenvalue of $$H$$ is simply the expectation of $$H$$

$$
\bra{\psi_i}H\ket{\psi_i}=\bra{\psi_i}E_i\ket{\psi_i}=E_i\bra{\psi_i}\ket{\psi_i}=E_i
$$

We will construct a progressively better approximation of the ground state, yielding a tighter and tighter upper bound for the ground state energy $$E_0$$.

The variational approach is motivated by the spectral theorem

$$
H=\sum_iE_i\ket{\psi_i}\bra{\psi_i}
$$

Assume that we constructed a state $$\ket\psi$$ which is an approximation of the true ground state $$\ket{\psi_0}$$ the expectation of $$H$$ in state $$\ket\psi$$ is $$\bra\psi H \ket\psi$$ which gives us by linearity of the inner product the result

$$
\bra\psi H \ket\psi = \bra\psi (\sum_iE_i\ket{\psi_i}\bra{\psi_i}) \ket\psi = \sum_iE_i\bra\psi\ket{\psi_i}\bra{\psi_i}\ket\psi
$$

$$
= \sum_iE_i|\bra\psi\ket{\psi_i}|^2
$$
