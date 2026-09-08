# Write-Up: Perceptron Train 3-Bit Parity

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `3-Bit Parity`, `3D Linear Separability`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> **Perceptron Train 3-Bit Parity** extends the non-linear classification dilemma from 2D into 3D space. The 3-bit parity function (equivalent to a 3-input XOR / sum modulo 2) places the 8 vertices of a unit cube into alternating binary classes. Because the classes alternate across opposite vertices in 3D, no single 2D plane (hyperplane) can separate them, making 100% accuracy geometrically impossible with a single perceptron. However, the theoretical linear maximum on this 8-point distribution is **75%** ($6/8$ points). Stepping through the training loop until the planar boundary separates 6 of the 8 vertices hits the target threshold and releases the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train 3-Bit Parity |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 2026 |

### Description

> *Watch a perceptron learn in real time on 3-bit parity data using the classic update rule: only misclassified points trigger updates, with no weight decay. This challenge extends the same idea into 3 dimensions, and the frontend renders the points in 3D space. Because parity is not linearly separable by one plane, a single perceptron cannot hit 100% accuracy. Reach 75% accuracy to reveal the flag.*

---

## Theoretical Background: 3-Bit Parity & The Unit Cube

The 3-bit parity function computes the sum of bits modulo 2:

$$y = x_1 \oplus x_2 \oplus x_3$$

This yields 8 sample points corresponding to the vertices of a 3D unit cube:

| $x_1$ | $x_2$ | $x_3$ | Parity Sum | Label ($y$) |
| :---: | :---: | :---: | :---: | :---: |
| 0 | 0 | 0 | 0 | **0** |
| 0 | 0 | 1 | 1 | **1** |
| 0 | 1 | 0 | 1 | **1** |
| 0 | 1 | 1 | 2 | **0** |
| 1 | 0 | 0 | 1 | **1** |
| 1 | 0 | 1 | 2 | **0** |
| 1 | 1 | 0 | 2 | **0** |
| 1 | 1 | 1 | 3 | **1** |

### Geometric Inseparability in 3D
A single-layer perceptron in 3 dimensions computes:

$$f(\mathbf{x}) = \text{step}(w_1 x_1 + w_2 x_2 + w_3 x_3 + b)$$

This defines a **flat 2D plane** slicing through the 3D cube. 

Just like 2-input XOR forms an alternating diagonal across a 2D square, 3-bit parity creates alternating class assignments on the vertices of a cube. Any single planar slice through the cube can, at most, correctly isolate a subset of points—it can never group all four $1$s on one side while keeping all four $0$s on the other.

---

## The 75% Target Ratio

There are **8 points total**. 

$$\text{Maximum Linear Capacity} = \frac{6 \text{ correct points}}{8 \text{ total points}} = 75.0\%$$

The challenge does not ask for full parity classification; it asks you to demonstrate understanding of higher-dimensional linear limits. Achieving 6 correct classifications out of 8 meets the **75%** threshold.

---


## Flag

```text
academy{3b1t_p4r1ty_unl34rn4bl3_l1n34rly_........}
