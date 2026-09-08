# Write-Up: Perceptron Play Naught

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `Feature Analysis`, `Linear Separability`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> In **Perceptron Play Naught**, we are tasked with manually tuning the weights and bias of a single perceptron to separate a 2D dataset that would otherwise be non-separable in a single dimension. Rather than blindly guessing weights or using trial-and-error, we inspect the coordinate features independently. A quick scan reveals that the $y$-feature alone cleanly separates both classes: every point with label `0` has $y = -1$, while every point with label `1` has $y \ge 1$. By nullifying $x$ with $w_1 = 0$, choosing the simplest positive weight $w_2 = 1$, and placing a bias $b = -0.5$ directly in the gap between the two classes, the horizontal decision boundary cleanly separates the entire set to reveal the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Play Naught |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 2026 |

### Description

> *The points would be inseparable in just the x-dimension, but each point now has a new y-value so the set becomes linearly separable in 2D. Watch the ASCII plot update in real time as you tweak the perceptron weights and bias. Separate the labeled points with a single line to earn the flag.*

---

## Theoretical Background: Manual Hyperplane Construction

A perceptron decides class membership based on the sign of its activation:

$$f(x, y) = \text{step}(w_1 x + w_2 y + b)$$

* Output is **1** if $w_1 x + w_2 y + b \ge 0$
* Output is **0** if $w_1 x + w_2 y + b < 0$

The decision boundary is the line where activation is exactly zero:

$$w_1 x + w_2 y + b = 0$$

If one feature completely separates the classes on its own, the orthogonal feature is redundant and its corresponding weight can simply be set to zero. This collapses a 2D line equation into a trivial threshold check along a single axis.

---

## Step-by-Step Walkthrough

### Step 1: Look for the Simplest Possible Pattern First

With 7 total points and 2 features $(x, y)$, the first thing to check isn't *"what complicated combination of $x$ and $y$ separates these"*—it's *"does just $x$ alone work, or does just $y$ alone work?"* Always test simple patterns before complex ones.

Scanning the $y$-values across all points in isolation reveals:

* **Label 0:** $y = -1, -1, -1$
* **Label 1:** $y = 2, 2, 1, 2$

Every `0` has $y = -1$. Every `1` has $y \ge 1$. 

This gives an immediately clean split using $y$ alone with no need to look at $x$. (If this had not worked, the next fallback would have been testing $x$ alone, and only then considering interactions between both variables).

---

### Step 2: Mechanical Weight Deduction

Once we establish that $y$ is the only feature that matters, choosing the weights becomes mechanical:

1. **Zeroing $x$ ($w_1 = 0$):** Since $x$ is irrelevant to the partition, setting $w_1 = 0$ tells the model: *"don't listen to $x$ at all."*
2. **Orienting $y$ ($w_2 = 1$):** Because higher $y$-values correspond to label `1`, higher $y$ needs to produce higher activation. Therefore, $w_2$ must be positive. Choosing $w_2 = 1$ is the simplest positive number—any positive value works identically, just scaling the steepness of the activation.

---

### Step 3: Placing the Cutoff via Bias

With $w_1 = 0$ and $w_2 = 1$, the activation formula reduces to:

$$\text{Activation} = y + b$$

The decision boundary (where activation equals $0$) sits at:

$$y = -b$$

For the separation to succeed, this boundary line just needs to land strictly inside the gap between the highest $y$ in class `0` ($-1$) and the lowest $y$ in class `1` ($1$):

$$-1 < -b < 1 \implies -1 < b < 1$$

Any number inside this open interval works. Selecting **$b = -0.5$** places the decision boundary at $y = 0.5$, cleanly inside the margin. (While $b = 0$ would center it symmetrically at the midpoint $y = 0$, any convenient value within the range successfully isolates the two groups).

---

### Final Parameter Configuration

| Parameter | Value | Reason |
| :---: | :---: | :--- |
| **$w_1$** | `0` | Completely ignores the irrelevant $x$-dimension. |
| **$w_2$** | `1` | Positively scales activation with increasing $y$. |
| **$b$** | `-0.5` | Places the horizontal boundary at $y = 0.5$, between $-1$ and $1$. |

Applying this combination instantly drew the horizontal dividing line between the two groups on the ASCII plot, separating 100% of the points and releasing the flag.

---

## Flag

```text
academy{n4ught_bu7_53p4r4b13_........}
