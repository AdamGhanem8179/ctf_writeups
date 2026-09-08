# Write-Up: Perceptron Train Hole in Middle

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `Linear Separability`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> The **Perceptron Train Hole in Middle** challenge presents an ostensibly impossible classification task: a single negative data point positioned directly in the center, completely surrounded by positive points. Because a single perceptron can only draw a straight linear boundary, it is geometrically impossible to achieve 100% classification. However, recognizing that the challenge only demands **88.9% accuracy** reveals the core mathematical insight: $8 / 9 \approx 88.9\%$. By deliberately sacrificing the single center point and orienting the weights to classify all outer perimeter points correctly, the perceptron hits the target threshold and releases the flag.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train Hole in Middle |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 9/8/2026 |

### Description

> *Watch a perceptron learn in real time on a "hole in the middle" pattern: positive points surround one negative center point. The classic perceptron update rule still applies (only misclassified points trigger updates, with no weight decay), but this shape is not linearly separable by a single line. Reach 88.9% accuracy to reveal the flag.*

---

## Theoretical Background: The "Hole in the Middle"

In machine learning theory, a standard Rosenblatt perceptron computes a weighted sum of inputs and applies a step function:

$$f(\mathbf{x}) = \begin{cases} 1 & \text{if } \mathbf{w} \cdot \mathbf{x} + b \ge 0 \\ 0 & \text{otherwise} \end{cases}$$

This formula creates a flat, linear hyperplane (a single straight line in 2D space).

The **"Hole in the Middle"** problem is an extension of the classic XOR limitation identified by Marvin Minsky and Seymour Papert in 1969. When a negative instance is completely encircled by positive instances:

```text
       (+)     (+)
    (+)   (-)   (+)      <-- Cannot isolate the center (-)
       (+)     (+)           with a single straight cut!
