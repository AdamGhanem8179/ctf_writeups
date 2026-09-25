# Cylab – Fix Me 2 Write-up

## Step 0 - Challenge Info

* **CTF Name:** Cylab

* **Challenge Name:** Rust Fix Me 2

* **Category:** Intro to Rust / General Skills

* **Points:** 10

* **Date:** 9/25/2026

* **Flag:** `academy{4r3_y0u_h4v1n5_fun_.....}`

## TL;DR (Abstract)

The challenge provides a broken Rust program (`fixme2` / `main.rs`) containing syntax and compilation errors. Once the errors are corrected, compiling and running the binary reveals the flag.

## Challenge Description

> Fix the compilation error in the Rust source code and run the executable to obtain the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the source code file provided in the challenge environment:

```bash
ls -la
cat main.rs
```

Attempting to compile the program using `rustc` or `cargo build` throws compiler errors preventing the binary from being built.

### 2. Execution & Flag Capture

Running the fixed binary executes the flag printing logic:

```bash
cargo run
```

Terminal Output:

```text
academy{4r3_y0u_h4v1n5_fun_.....}
```

Flag:

```
academy{4r3_y0u_h4v1n5_fun_.....}
```
