---
description: >-
  A quantum system starts in an eigenstate of an initial Hamiltonian, and that
  Hamiltonian is slowly varied to a final Hamiltonian, then the system will end
  up in an eigenstate of the final Hamiltonian
---

# 👍 Adiabatic Quantum Computation

## Readings

* [On the adiabatic theorem of quantum mechanics](https://sci-hub.st/10.1143/jpsj.5.435)
* [Adiabatic Theorem without a Gap Condition](https://arxiv.org/abs/math-ph/9805022)
* [Quantum Adiabatic Evolution Algorithms versus Simulated Annealing](https://arxiv.org/abs/quant-ph/0201031)
* [Inconsistency in the application of the adiabatic theorem](https://arxiv.org/abs/quant-ph/0404022)

## Content

* Quantum Adiabatic Theorem
* Solving An Optimization Problem

## Quantum Adiabatic Theorem

Recall the second postulate of quantum mechanics, the time evolution of a closed quantum system is described by the Schrodinger equation:

$$
i\hbar\frac{d\ket{\psi{(t)}}}{dt}=H(t)\ket{\psi{(t)}}
$$

Taking Schrodinger equation normalized with $$\hbar = 1$$ and a time independent Hamiltonian $$H$$, if the system starts in state $$\ket{\psi(0)}$$ then the solution at time $$t\ge0$$ would be

$$
\ket{\psi(t)}=e^{-iHt}\ket{\psi(0)}
$$

Consider again the Schrodinger equation normalized with $$\hbar = 1$$ over the time interval $$[0,\tau]$$ where the Hamiltonian is going to be time dependent and the time change $$t(0)=1$$ and $$t(1)=\tau$$, and then we get

$$
i\frac{d\ket{\psi{(s)}}}{ds}=t'(s)H(s)\ket{\psi{(s)}}
$$

over the unit time interval $$[0,1]$$.

Here, we are chiefly interested in Hamiltonians of the (slightly generalized) form

$$
H(s)=r(s)H_0+(1-r(s))H_F
$$

for two given Hamiltonians $$H_0$$ and $$H_F$$, where $$r()$$ is a continuous adiabatic evolution path decreasing from $$r(0)=1$$ to $$r(1)=0$$. The standard adiabatic schedule is $$r(s)=1-s$$.

Assume that the system starts from the ground state of $$H_0$$. If the time evolution of the Hamiltonian is sufficiently slow, then the system remains in the ground state of the evolving Hamiltonian up to time 1.

## Solving An Optimization Problem

If we know how to encode an objective function that we want to minimize for a problem as the Hamiltonian of a quantum system, then finding the ground state of the Hamiltonian is equivalent to finding the set of decision variables that minimizes the objective function.

As a simple example of equivalence between the minimum of a function and the ground state of a Hamiltonian, consider a function $$f:{\{0,1\}}^n\rarr\real$$ that needs to be minimized and take the Hamiltonian

$$
H_F=\sum_{z\in{\{0,1\}}^n}f(z)\ket{z}\bra{z}
$$

Clearly, for any $$z\in{\{0,1\}}^n$$

$$
H_F\ket{z_0}=(\sum_{z\in{\{0,1\}}^n}f(z)\ket{z}\bra{z})\ket{z_0}=
f(z_0)\ket{z_0}{\bra{z_0}\ket{z_0}}=f(z_0)\ket{z_0}
$$

since the computational basis $$\ket{z}_{z\in\{0,1\}^n}$$ is orthonormal. Therefore any $$z_0\in\{0,1\}^n$$ is an eigenstate of $$H_F$$ with eigenvalue $$f(z_0)$$. Minimizing $$f$$ is thus clearly equivalent to finding the lowest eigenvalue of the Hamiltonian $$H_F$$.

Let us further assume that we have another quantum Hamiltonian, $$H_0$$, whose ground state is easy to find and easy to prepare in an experimental setup. Then, if we prepare a quantum system to be in the ground state of $$H_0$$, and then adiabatically (slowly) change the system Hamiltonian, $$H(t)$$, from $$H_0$$ at $$t = 0$$ to $$H_F$$ at $$t = τ$$ according the following time evolution

$$
H(t)=(1-\frac{t}\tau)H_0+\frac{t}\tau H_F
$$

then if $$τ$$ is large enough, and $$H_0$$ and $$H_F$$ do not commute, the quantum system will remain in the ground state at all times according to the quantum adiabatic theorem. Measuring the quantum state at $$t = τ$$ will produce a solution of our problem (a bit string that encodes an optimal configuration of binary decision variables).
