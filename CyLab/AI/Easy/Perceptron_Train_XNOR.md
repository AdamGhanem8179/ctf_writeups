# Write-Up: Perceptron Train XNOR

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `XNOR`, `Linear Separability`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> **Perceptron Train XNOR** presents the logical complement to the classic XOR dilemma: the exclusive-NOR (equivalence) function. Because the true classes $(0, 0)$ and $(1, 1)$ sit diagonally opposite each other while the false classes $(0, 1)$ and $(1, 0)$ occupy the remaining corners, the distribution cannot be partitioned by any 2D line. Understanding linear decision surface constraints immediately shows that the theoretical upper limit for a single perceptron on a 4-point parity problem is exactly **75%** ($3/4$). By orienting the linear boundary to cleanly classify three points while sacrificing the fourth, the perceptron reaches the required threshold and prints the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train XNOR |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 2026 |

### Description

> *Watch a perceptron learn in real time on XNOR data using the classic perceptron update rule. Reach the theoretical maximum linear accuracy to reveal the flag.*

---

## Theoretical Background: The XNOR Decision Surface

The logical XNOR (equivalence) operation outputs $1$ if and only if both boolean inputs match:

| $x_1$ | $x_2$ | $y$ ($x_1 \odot x_2$) |
| :---: | :---: | :---: |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

Mapping these vectors onto the Cartesian plane illustrates the geometric challenge:

```text
  x2 ^
   1 |   (-) y=0         (+) y=1
     |   (0, 1)          (1, 1)
     |
   0 |   (+) y=1         (-) y=0
     |   (0, 0)          (1, 0)
     +-------------------------->
         0               1        x1

## Flag

```text
cylab{academy{xn0r_unl34rn4bl3_by_p3rc3ptr0ns_........}
}
