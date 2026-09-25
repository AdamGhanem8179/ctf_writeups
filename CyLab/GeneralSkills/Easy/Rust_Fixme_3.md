# CyLab – Rust fixme3 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Rust fixme3

* **Category:** General Skills / Reverse Engineering

* **Points:** 50

* **Date:** 9/25/2026

* **Flag:** academy{n0w_y0uv3_f1x3d_1h3m_...}

## TL;DR (Abstract)

The challenge provides a broken Rust source file (`fixme3.rs`) containing compilation errors. After fixing the syntax and logic errors preventing the binary from compiling, the program executes cleanly and prints the decoded flag wrapper.

## Challenge Description

> Fix the compilation and syntax errors in the provided Rust program to reveal the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the challenge file:

* **Target:** `fixme3.rs`
* **Language:** Rust
* **Goal:** Resolve compilation errors and execute the program to output the flag.

### 2. Execution & Flag Capture

Compile and run the corrected Rust program:

```bash
rustc fixme3.rs && ./fixme3
```

Terminal Output:

```
academy{n0w_y0uv3_f1x3d_1h3m_...}
```

Flag:

```
academy{n0w_y0uv3_f1x3d_1h3m_...}
```
