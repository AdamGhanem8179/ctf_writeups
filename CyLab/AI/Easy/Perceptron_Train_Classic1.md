# Write-Up: Perceptron Train Classic 1

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `Hyperparameters`, `Learning Rate`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> In **Perceptron Train Classic 1**, we train a single-layer perceptron on a linearly separable 2D dataset governed by the classic Rosenblatt update rule. Instead of requiring complex manual tuning for each run, the goal is simply to find **5 distinct learning rates ($\eta$)** that each reach **100% accuracy**. Once a single working baseline learning rate is identified, we exploit the continuous nature of the parameter space by incrementally nudging the value by small steps (e.g., `1.43`, `1.44`, `1.45`, etc.). Each run achieves complete convergence, filling the 5-run counter and instantly revealing the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train Classic 1 |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 2026 |

### Description

> *Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. In this variant you must find 5 successful learning rates (each reaching 100% accuracy) before the flag is revealed. Dial in a rate, trigger a run, and the interface animates each step.*

---

## Thought Process & Initial Analysis

The challenge asks for 5 distinct learning rates that result in 100% classification accuracy on a linearly separable dataset. 

Because the dataset is cleanly separable with a clear margin, the Novikoff Perceptron Convergence Theorem guarantees that any reasonable step size will successfully converge without oscillating out of bounds. This means there is no need to reinvent completely different numbers or calculate custom values from scratch:

* If a baseline rate works, tiny micro-adjustments around that exact neighborhood will also work.
* Finding one successful value allows us to simply increment the value by tiny amounts (e.g., $+0.01$) across successive runs to satisfy the requirement for 5 unique inputs.

---

## Step-by-Step Walkthrough

### 1. Connecting to the Web Workspace

1. Click **Launch Instance** on the platform modal and open the interactive lab link in the browser.
2. The UI shows the 2D data points, a learning rate input box, a run button, and a counter tracking successful runs (`0 / 5`).

---

### 2. Finding the Baseline Rate & Incrementing

Rather than testing radically different orders of magnitude, we dial in a solid initial number and apply small successive increments:

1. **Run 1:** Entered initial working rate `1.43` $\to$ Hit **Train/Run** $\to$ Perceptron animated to **100% accuracy** (`1/5`).
2. **Run 2:** Incremented to `1.44` $\to$ Hit **Train/Run** $\to$ Perceptron converged to **100% accuracy** (`2/5`).
3. **Run 3:** Incremented to `1.45` $\to$ Hit **Train/Run** $\to$ Perceptron converged to **100% accuracy** (`3/5`).
4. **Run 4:** Incremented to `1.46` $\to$ Hit **Train/Run** $\to$ Perceptron converged to **100% accuracy** (`4/5`).
5. **Run 5:** Incremented to `1.47` $\to$ Hit **Train/Run** $\to$ Perceptron converged to **100% accuracy** (`5/5`).

---

### 3. Retrieving the Flag

As soon as the fifth unique incremented rate cleared 100% accuracy, the progress counter hit `5/5` and the platform automatically printed the flag.

---

## Flag

```text
academy{perceptron_classic_5rates_........}
