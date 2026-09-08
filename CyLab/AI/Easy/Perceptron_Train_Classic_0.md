# Write-Up: Perceptron Train Classic 0

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `Linearly Separable`, `CyLab Security Academy`, `picoCTF`, `Easy`

---

## TL;DR

> **Perceptron Train Classic 0** serves as the introductory baseline for the perceptron training series. The dataset is intentionally designed to be gentle and cleanly linearly separable, with wide geometric margins between classes. Using the interactive browser interface, no complex hyperparameter tuning or rate adjustments are required—running the instance with its pre-configured default values executes the classic update rule, rapidly converges to **100% accuracy**, and releases the flag on the very first try.

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Perceptron Train Classic 0 |
| **Category** | Artificial Intelligence / Foundations I |
| **Difficulty** | Easy |
| **Author** | LT 'syreal' Jones |
| **Points** | Practice / Learning Library |
| **Date** | 9/8/2026 |

### Description

> *Watch a perceptron learn in real time using the classic update rule: only misclassified points trigger updates, with no weight decay. This dataset is intentionally gentle, so many learning rates still converge quickly. Dial in a rate, trigger a run, and the interface will animate each step until every point is classified correctly. Visit the service in your browser:*
>
> `http://aureolin-pixie.cylabacademy.net:61238/`

---

## Thought Process & Initial Analysis

The challenge description explicitly notes that this dataset is **"intentionally gentle"**:
* The distribution is strictly linearly separable with a large margin separating the binary classes.
* Because the platform pre-populates the interface with a valid baseline learning rate and initial weights, there is no need to experiment with exotic values or perform extensive manual calibration.
* Simply executing the training loop with the default configuration allows the Rosenblatt update rule to settle the decision line cleanly between the two clusters.

---

## Flag

```text
academy{perceptron_classic_mode_........}


