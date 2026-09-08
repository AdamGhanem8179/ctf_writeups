# Write-Up: Perceptron Train XOR

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `XOR`, `Linear Separability`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> The **Perceptron Train XOR** challenge revisits one of the most famous historical milestones in neural network history: the linear inseparability of the exclusive-OR (XOR) function. A single perceptron attempts to classify four coordinate points $(0,0), (0,1), (1,0),$ and $(1,1)$. Because true outputs $(1)$ and false outputs $(0)$ lie diagonally opposite one another, no single linear decision boundary can separate them. The challenge requires recognizing that the maximum achievable accuracy for a single-layer perceptron on XOR data is exactly **75%** ($3/4$ points). Once the perceptron is adjusted to correctly classify three of the four points, the accuracy requirement is satisfied and the flag is unlocked.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train XOR |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 2026 |

### Description

> *Watch a perceptron learn in real time on XOR data using the classic perceptron update rule. Reach the theoretical maximum linear accuracy to reveal the flag.*

---

## Theoretical Background: The Minsky-Papert XOR Problem

The XOR truth table produces the following coordinate distribution in 2D space:

| $x_1$ | $x_2$ | $y$ (Label) |
| :---: | :---: | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Visualized on a 2D Cartesian plane:

```text
  x2 ^
   1 |   (+) y=1         (-) y=0
     |   (0, 1)          (1, 1)
     |
   0 |   (-) y=0         (+) y=1
     |   (0, 0)          (1, 0)
     +-------------------------->
         0               1        x1

## Flag

```text
cylab{academy{x0r_unl34rn4bl3_by_p3rc3ptr0ns_........}
}
