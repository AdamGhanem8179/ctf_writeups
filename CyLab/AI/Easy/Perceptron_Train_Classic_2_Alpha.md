# Generate the updated markdown incorporating the browser GUI interface and dedicated flag placeholder
writeup_content = """# Write-Up: Perceptron Train Classic 2 Alpha

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `Linearly Separable`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> Unlike non-linear parity datasets (such as XOR or the "Hole in the Middle" problem) where a single perceptron cannot achieve 100% classification, **Perceptron Train Classic 2 Alpha** features a textbook **linearly separable** binary dataset. Hosted on an interactive browser GUI rather than a raw Netcat terminal instance, the challenge visualizes the decision line shifting across the Cartesian plane in real time. Guided by the Novikoff Perceptron Convergence Theorem, stepping through the training updates automatically corrects misclassifications, sliding the hyperplane directly into the decision margin between the two distinct clusters to reach **100% accuracy** and generate the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train Classic 2 Alpha |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 9/8/2026 |

### Description

> *Train a classic single-layer perceptron on the Classic 2 Alpha dataset. Unlike parity and non-linear distributions, this dataset is linearly separable. Apply updates to misclassified points until the decision boundary achieves 100% classification accuracy to reveal the flag.*

---

## Theoretical Background: Linearity and Convergence

A Rosenblatt perceptron classifies an input vector $\\mathbf{x} = [x_1, x_2]^T$ using weights $\\mathbf{w} = [w_1, w_2]^T$ and a scalar bias $b$:

$$\\hat{y} = \\text{step}(\\mathbf{w} \\cdot \\mathbf{x} + b) = \\begin{cases} 1 & \\text{if } w_1 x_1 + w_2 x_2 + b \\ge 0 \\\\ 0 & \\text{otherwise} \\end{cases}$$

The **Novikoff Perceptron Convergence Theorem** proves that if two classes can be completely separated by a straight line with a margin $\\gamma > 0$, the standard perceptron learning rule will converge with zero errors in a finite, bounded number of updates:

$$\\text{Mistakes} \\le \\left(\\frac{R}{\\gamma}\\right)^2$$

Because the **Classic 2 Alpha** dataset consists of two clean, isolated clusters that do not intertwine, reaching 100% accuracy is mathematically guaranteed.

---

## Step-by-Step Walkthrough

### 1. Accessing the Interactive GUI

Rather than connecting via a terminal Netcat command, this challenge provides a dedicated web-based interactive workspace link:

1. Click **Launch Instance** in the challenge window to generate the active session link.
2. Open the URL directly in the browser to load the graphical perceptron training laboratory.
3. The interface displays a 2D scatter plot showing two clearly separated groups of data points alongside current weight sliders, bias metrics, and an accuracy meter.

---

### 2. Identifying the Separating Axis

Inspecting the data points on the plot confirms that the two clusters are strictly linearly separable:

* **Cluster A (Class 0):** Resides in one distinct region of the 2D plane.
* **Cluster B (Class 1):** Resides on the opposing side with a wide open separating channel between them.

Because no points overlap or surround each other, we do not need to accept an accuracy compromise (like 75% or 88.9%); the objective is a full **100% classification rate**.

---

### 3. Stepping Through the Perceptron Updates

Inside the interactive web interface, click the **Step / Train** button (or let the automatic training loop run):

* Whenever a misclassified point is encountered, the perceptron update rule triggers:
  $$\\mathbf{w}^{(t+1)} = \\mathbf{w}^{(t)} + \\eta (y_i - \\hat{y}_i) \\mathbf{x}_i$$
* The visual decision line pivots and translates across the screen, adapting its slope ($-\\frac{w_1}{w_2}$) and intercept ($-\\frac{b}{w_2}$).
* Within a small handful of steps, the line settles cleanly into the empty margin between the two clusters.
* The accuracy gauge ticks up to **100.0% (Zero Misclassifications)**.

---

### 4. Retrieving the Flag

As soon as the web GUI registers 100% accuracy across all sample coordinates, the interface stops the training loop and prints the flag directly in the notification banner.

---

## Flag

```text
academy{perceptron_classic_2_alpha_5rates_........}
