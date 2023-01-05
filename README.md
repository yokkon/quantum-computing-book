---
description: Baby steps of quantum mechanics
---

# ⚒ Qubit Linear Algebra & Schrodinger Equation

## Readings

*

## Content

* Quantum Theory Principles
* Wave function
* Operators
* Time evolution and quantum gates

## Quantum Theory Principles

*   Quantization

    Variables that were considered to be continuous like position, momentum and energy became quantized.
*   Superposition

    Each particle can be on numerous places at the same time. there's also many other characteristics of the particle like energy, momentum can be in a **superposition** state - having multiple values at the same time.

    This "mixing" of values is not a classical probability distribution because we can see a phenomenon of **interference** between superposed states of particles.     &#x20;
*   Entanglement

    Entangled states hold together different particles in a unique way that makes those particles inseparable and there is to think about those particles as one system, otherwise the information about the entangled state is not complete. entanglement create between particles a bond that crosses the limits of space and time.
*   Uncertainty

    Usually the results of our measurements are not known, not just to us but in some deep way even to nature itself. we only know what is the probability to achieve some result or another but  we can't promise to get a specific result. in addition there's some underlying bond between some variables like position-momentum or time-energy which rules that knowing one variable's value in a greater precision hurts the measurement precision of the other variable. &#x20;
*   Measurement and collapsing

    When measuring in experiments one of the characteristics we talked about, the former state could have been a superposition of a few states and when measuring it collapses into one of the possible states (values) possible. furthermore when we choose to measure a particle, the way we measure it effects the particle and changes its quantum state.

{% embed url="https://www.youtube.com/watch?v=Q1YqgPAtzho" %}
Two slit experiment is considered to fold in it the secrets of quantum mechanics
{% endembed %}

## Wave function

The position probability (or every other attribute) of the particle can be described with a **wave function.**\
****One can think of the wave function as a state in the Hilbert space (complete inner product space) or just as a vector (finite or infinite depends on the amount of values an attribute can have).\
We write the wave function $$\psi(x)$$ when it's describing position of a particle, but usually we write the quantum state as $$\ket\psi$$.

The wave function is in fact a complex probability amplitude in a sense that it's absolute value squared describes probability density, meaning the probability of finding the particle in the segment $$[x_0,x_1]$$.

$$\int_{x_0}^{x_1}|f(x)|^2dx$$$$\integral$$

In a 2-dimensional Hilbert space, that is more relevant for the basic understanding of quantum computing, the wave function that describes a superposition of two orthonormal states $$\ket0$$ and $$\ket1$$ will be written as $$\ket\psi = \alpha\ket0+\beta\ket1$$ so if we perform a measurement on the quantum state, we get the state $$0$$ with probability $$|\alpha|^2$$ and the state $$1$$ with probability $$|\beta|^2$$. In order for the wave function to represent probability density it must be normalized over the Hilbert space meaning $$\int_{-\infty}^{\infty}|f(x)|^2dx=1$$ and in our case $$|\alpha|^2+|\beta|^2=1$$, what happens in the measurement process is basically a **projection** in its algebraic sense, meaning, we compute the inner product of the wave function with the target state we want to check and then we get the probability amplitude of the target state, for example $$\bra0\ket\psi=\alpha\bra0\ket0+\beta\bra0\ket1=\alpha$$, notice that states $$\ket0$$ and $$\ket1$$ are **orthonormal** and we get $$P(0)=|\bra0\ket\psi|^2=\alpha^2$$.

The right side closing $$\ket\psi$$ is called **ket** and the left side closing $$\bra\phi$$ is called **bra**, there inner product $$\bra\phi\ket\psi$$ is called **braket.**

The bra belongs to the Hilbert space and is dual to the ket-space, it tells us to take a column vector which is the ket form and turn it into its complex conjugate the row vector.\
Let's sum it up:\
$$\ket0=\begin{pmatrix}1\\0\end{pmatrix}$$ $$\ket1=\begin{pmatrix}0\\1\end{pmatrix}$$\
$$\ket\psi=\alpha\begin{pmatrix}1\\0\end{pmatrix}+\beta\begin{pmatrix}0\\1\end{pmatrix}=\begin{pmatrix}\alpha\\\beta\end{pmatrix}$$\
$$\bra\psi=\alpha^*\begin{bmatrix}1 & 0\end{bmatrix}+\beta^*\begin{bmatrix}0 & 1\end{bmatrix}=\begin{bmatrix}\alpha^* & \beta^*\end{bmatrix}$$\
This is called **Dirac's** **braket notation**.

## &#x20;Operators

