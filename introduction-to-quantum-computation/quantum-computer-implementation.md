---
description: >-
  This page explains the requirements for making a quantum computation system,
  some implementations and the challenges behind
---

# ⚒ Quantum Computer Implementation

## Content

* General criteria of DiVincenzo
* Known physical implementations of qubits
* Optical photon quantum computer
* Decoherence

## General Criteria of DiVincenzo

List of the basic requirements of a quantum computer:

1. system will allow to present qubits in a defined and scalable way
2. it is possible to reset the system state in an easy way to one that is easy to work with
3. decoherence times will be long enough
4. it is possible to measure the system state and read the result
5. it is possible to implement an universal set of quantum gates, for example, T and S, H, CNOT where

$$
S = \left[ {\begin{array}
{cc}
1 & 0 \\
0 & e^{i\frac{\pi}{2}}
 \end{array} } \right]= \left[ {\begin{array}
{cc}
1 & 0 \\
0 & i
 \end{array} } \right]=\sqrt Z
\newline
T=\left[ {\begin{array}
{cc}
1 & 0 \\
0 & e^{i\frac{\pi}{4}}
 \end{array} } \right]=\sqrt S=\sqrt[4] Z
$$

## Known Physical Implementations of Qubits

In general, all we need is a system with two possible levels, there's a lot of possible ways to achieve this:

&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Different quantum technologies table</p></figcaption></figure>

## Optical Photon Quantum Computer

The optical photon technology is a comfortable way to achieve a system that create quantum states and implement quantum gates.\
Photons are chargeless particles, and do not interact very strongly with each other, or even with most matter.

#### The Hamiltonian

The Hamiltonian for a particle in a one-dimensional parabolic potential is

$$
H = \frac{p2}{2m}+\frac12mω2x2
$$

where $$p$$ is the particle momentum operator, $$m$$ is the mass, $$x$$ is the position operator, and $$ω$$ is related to the potential depth. Recall that x and p are operators in this expression (see Box 7.2), which can be rewritten as

$$
H = \hbarω \left( a^†a +\frac12 \right)
$$

where $$a^†$$ and $$a$$ are creation and annihilation operators, defined as

$$
a = \frac{1}{\sqrt{2m\hbar\omega}}(m\omega x + ip)
\newline
a^† = \frac{1}{\sqrt{2m\hbar\omega}}(m\omega x - ip)
$$

The zero point energy $$\frac{\hbarω}2$$ contributes an unobservable overall phase factor, which can be disregarded for our present purpose. The eigenstates $$\ket n$$ of $$H$$, where $$n = 0, 1,...$$, have the properties

$$
a^†a\ket n = n\ket n
\newline
a^†\ket n = \sqrt{n + 1}\ket{n + 1} 
\newline
a\ket n = \sqrt n \ket {n-1}
$$

The meaning of that is that the base state ("vacum") represented by the $$\ket0$$ state and it's energy is $$\frac{\hbarω}2$$.\
Every activation of the $$a^†$$ operator will take the particle to it's next energy level, that its energy is greater by $$\hbarω$$ from the one before:

$$
\ket1=a^†\ket0
\newline
\ket n = \frac{a^†}{\sqrt{n!}}\ket0
$$

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>The quantum harmonic oscillator</p></figcaption></figure>

#### Apparatus

As we saw in the discussion of the simple harmonic oscillator, the energy in an electromagnetic cavity is quantized in units of $$\hbarω$$.\
Each such quantum is called a photon. It is possible for a cavity to contain a superposition of zero or one photon, a state which could be expressed as a qubit $$\ket\psi=c_0\ket0 + c_1\ket1$$, but we shall do something different. Let us consider two cavities, whose total energy is $$\hbarω$$, and take the two states of a qubit as being whether the photon is in one cavity $$\ket{01}$$ or the other $$\ket{10}$$. The physical state of a superposition would thus be written as $$\ket\psi=c_0\ket{01} + c_1\ket{10}$$; we shall call this the dual-rail representation.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Dual-rail representation vs single-rail</p></figcaption></figure>

Let's talk about a method of creating a one photon state, which is called parametric down-conversion, this involves sending photons of frequency $$ω_0$$ into a nonlinear optical medium such as KH2PO4 to generate photon pairs at frequencies $$ω_1 + ω_2 = ω_0$$.\
Momentum is also conserved, such that $$\vec{k_1}+ \vec{k_2} = \vec{k_3}$$, so that when a single $$ω_2$$ photon is (destructively) detected, then a single $$ω_1$$ photon is known to exist.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Parametric down-conversion scheme for generation of single photons</p></figcaption></figure>

#### Quantum Gates

Three of the most experimentally accessible devices for manipulating photon states are mirrors, phase shifters and beamsplitters. High reflectivity mirrors reflect photons and change their propagation direction in space. Mirrors with 0.01% loss are not unusual. We shall take these for granted in our scenario. A phase shifter is nothing more than a slab of transparent medium with index of refraction n different from that of free space.
