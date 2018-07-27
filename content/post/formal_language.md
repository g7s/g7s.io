+++
title = "Formal language"
description = "Mathematical definition of a formal language."
date = "2217-06-23T19:30:29+03:00"
tags = ["programming languages", "theory"]
draft = true
+++

Before we dive into defining what we say a *formal language* we make some
definitions about things that you may find trivial to state but are important.


# The Alphabet

<i class="definition">
An $\textbf{alphabet}$ is a finite (more correctly countable) nonempty set
$\Sigma$ of symbols.
</i>

E.g.

* The English symbols: $\Sigma_{e} = \lbrace a, b, \dots, z, A, B, \dots, Z \rbrace$
* Digit symbols: $\Sigma_{d} = \lbrace 0, 1, \dots, 9 \rbrace$
* Hexadecimal symbols: $\Sigma_{h} = \lbrace 0, \dots, 9, a, b, c, d, e, f \rbrace$
* Binary symbols: $\Sigma_{b} = \lbrace 0, 1 \rbrace$
* Alphabet for variable identifiers in C:
$\Sigma_{C} = \lbrace \\_ \rbrace \cup \Sigma_e \cup \Sigma_d$


# The String

<i class="definition">
A $\textbf{string}$ $s$ is a countable sequence of symbols $(\sigma_i)$ with
$\sigma_i \in \Sigma$.
</i>

E.g.

* Every word in this sentence is a string derived from the English symbols.
* $012$, $3$, $192$ are strings derived from the $\Sigma_{d}$.

<i class="definition">
The $\textbf{length}$ of a string $s$ is the length of the sequence $(\sigma_i)$
and we denote it by $|s|$.
</i>

<i class="definition">
The $\textbf{empty string}$ $\epsilon$ is the empty sequence $|\epsilon| = 0$
and can be derived from *any* alphabet $\Sigma$.
</i>

The set of all strings of length $k$ is denoted by $\Sigma^{k}$ from which
$\Sigma^{0} = \lbrace \epsilon \rbrace$ follows. For example we have:

<div>
\begin{align*}
\Sigma_b^1 &= \lbrace 0, 1 \rbrace           \\
\Sigma_b^2 &= \lbrace 00, 01, 10, 11 \rbrace \\
           &\vdots
\end{align*}
</div>

<div class="definition">
The star $*$ and plus $+$ operators (called Kleene operators) are defined as follows:

\begin{align*}
\Sigma^* &= \bigcup_{k\in\mathbb{N}}\Sigma^k     \\
\Sigma^+ &= \bigcup_{k\in\mathbb{Z}^+}\Sigma^k   \\
\end{align*}
</div>

<mark>What the above actually says is that $\Sigma^*$ is the set of all possible
strings derived from an alphabet $\Sigma$.</mark>

**NOTE**: Do not confuse this with the [power set](http://mathworld.wolfram.com/PowerSet.html)
which is the set of all subsets of a set.

**NOTE**: We declared the string to be a countable (not finite) sequence in
order to be able to define $\Sigma^*$ in the way we did.


# The Language

A language is nothing more than a specific set of strings derived from some
alphabet $\Sigma$. To be more precise:

<div class="definition">
Given an alphabet $\Sigma$ we define $L$ to be a $\textbf{language over}$
$\Sigma$ iff $L \subseteq \Sigma^*$.
</div>

That's it. We usually define a language in terms of a
