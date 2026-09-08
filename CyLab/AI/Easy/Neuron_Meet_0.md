# Write-Up: Neuron Meet 0

**Tags:** `AI`, `Machine Learning`, `Perceptron`, `Reverse Engineering`, `CyLab Security Academy`, `picoCTF`, `Easy`[cite: 3, 4]

---

## TL;DR

> **Neuron Meet 0** tasks us with probing a black-box 1D perceptron across a network socket to determine its decision boundary ($w \cdot x + b \ge 0$)[cite: 3, 4]. By sending a series of test inputs, we map where the neuron fires (`1`) versus where it stays quiet (`0`)[cite: 3, 4]. Once the threshold is located, we clear the buffer with `RESET` and send eight distinct numbers (respecting the no-consecutive-duplicates rule) to output the binary representation of ASCII `'p'` (`01110000`) to retrieve the flag[cite: 3, 4].

---

## Challenge Information

| Attribute | Details |
| :--- | :--- |
| **CTF / Platform** | CyLab Security Academy (formerly picoCTF) |
| **Challenge Name** | Neuron Meet 0[cite: 3, 4] |
| **Category** | Artificial Intelligence / Foundations I[cite: 3, 4] |
| **Difficulty** | Easy[cite: 3, 4] |
| **Author** | LT 'syreal' Jones[cite: 3, 4] |
| **Points** | Practice / Learning Library[cite: 3, 4] |
| **Date** | 2026[cite: 3, 4] |

### Description

> *Probe a 1D perceptron over the network. Send it numbers and watch whether the neuron fires or not. Use those responses to figure out the decision boundary, then line up the last eight outputs to read the ASCII for 'p' (01110000) and you'll earn the flag.*[cite: 3, 4]

---

## Step-by-Step Walkthrough

### 1. Mapping the Threshold
To figure out where the perceptron flips from `0` to `1`, I threw test numbers at it[cite: 3, 4]:

* `x = 1` -> Stays quiet (`0`)[cite: 3, 4]
* `x = 2` -> Fires (`1`)[cite: 3, 4]
* `x = 4, 6, 3, 5, 10` -> All fired (`1`)[cite: 3, 4]
* `x = -1` -> Stays quiet (`0`)[cite: 3, 4]

This established the rule:
* Any number **$\le 1$** outputs **`0`**[cite: 3, 4].
* Any number **$\ge 2$** outputs **`1`**[cite: 3, 4].

---

### 2. Clearing the History
Because probing filled the 8-slot history buffer with random test bits (`01111110`), I cleared the slate with[cite: 3, 4]:

```text
x> RESET
History cleared. Keep probing the neuron.
```[cite: 3, 4]

---

### 3. Entering the Full 8-Number Sequence for ASCII 'p' (`01110000`)
The goal requires the last 8 outputs to match `'p'` (`01110000`)[cite: 3, 4]. Because the server forbids sending the exact same number back-to-back, I fed it 8 different numbers across the threshold[cite: 3, 4]:

1. `x = -2` -> Perceptron stays quiet -> Output: **`0`** (Recent outputs: `0`)[cite: 3, 4]
2. `x = 2`  -> Perceptron fires!      -> Output: **`1`** (Recent outputs: `01`)[cite: 3, 4]
3. `x = 3`  -> Perceptron fires!      -> Output: **`1`** (Recent outputs: `011`)[cite: 3, 4]
4. `x = 4`  -> Perceptron fires!      -> Output: **`1`** (Recent outputs: `0111`)[cite: 3, 4]
5. `x = 1`  -> Perceptron stays quiet -> Output: **`0`** (Recent outputs: `01110`)[cite: 3, 4]
6. `x = -1` -> Perceptron stays quiet -> Output: **`0`** (Recent outputs: `011100`)[cite: 3, 4]
7. `x = -3` -> Perceptron stays quiet -> Output: **`0`** (Recent outputs: `0111000`)[cite: 3, 4]
8. `x = -5` -> Perceptron stays quiet -> Output: **`0`** (Recent outputs: `01110000`)[cite: 3, 4]

The terminal confirmed the match:
```text

## Flag
academy{n3ur0n_m3t_e231b9ca}
```text
