# picoCTF – Rust fixme 1 Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** Rust fixme 1

* **Category:** General Skills / Reverse Engineering

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{4r3_y0u_4_ru$t4c30n_....}

## TL;DR (Abstract)

The challenge supplies a Rust project containing several straightforward syntax and formatting errors that prevent successful compilation. By executing `cargo run`, observing the compiler diagnostics, and iteratively resolving issues—such as missing semicolons, incorrect print macro invocations (`println!`), and string formatting mismatches—the code compiles, runs cleanly, and reveals the flag.

## Challenge Description

> Can you fix the errors in this Rust program and compile it to get the flag?
> Download the challenge source and run it with `cargo run`.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the directory structure of the downloaded Rust crate:

```bash
ls -la
```

The directory contains standard Rust project files:
* `Cargo.toml`: Package configuration and metadata.
* `src/main.rs`: The main application entry point containing the faulty source code.

Attempt to build and run the binary using the Cargo package manager:

```bash
cargo run
```

The Rust compiler (`rustc`) immediately halts with syntax and compilation errors.

### 2. Iterative Debugging via Compiler Feedback

Rust's compiler produces detailed, actionable error diagnostics with suggestions for fixes. The errors encountered and resolved include:

#### A. Missing Statement Terminators (Semicolons)

```text
error: expected `;`, found `...`
  --> src/main.rs:14:26
   |
14 |     let secret = "..."
   |                       ^ help: add `;` here
```

In Rust, statements binding variables or executing operations require a terminating semicolon (`;`) unless explicitly returning an expression. Adding the missing `;` resolves the parsing failure.

#### B. Print Macro Syntax

```text
error: cannot find function `println` in this scope
  --> src/main.rs:18:5
   |
18 |     println("The flag is: {}", flag);
   |     ^^^^^^^ help: use `!` to invoke the macro: `println!`
```

Standard text output in Rust is handled via the `println!` macro rather than a regular function call. Appending the exclamation point (`!`) converts the invalid function call into the appropriate macro invocation:

```rust
// Before
println("...", ...);

// After
println!("...", ...);
```

#### C. String Formatting and Argument Placement

Additional formatting discrepancies (such as unescaped characters, mismatched quotation marks, or incorrect format specifier placements in the format string) were adjusted to match Rust's string interpolation rules.

### 3. Execution & Flag Capture

Once all compiler errors in `src/main.rs` are corrected, re-execute the build and run pipeline:

```bash
cargo run
```

Terminal Output:

```text
   Compiling rust-fixme-1 v0.1.0 (/home/user/rust-fixme-1)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.42s
     Running `target/debug/rust-fixme-1`
academy{4r3_y0u_4_ru$t4c30n_....}
```

The project compiles cleanly, runs the binary, and prints the decrypted flag to standard output:

```
academy{4r3_y0u_4_ru$t4c30n_....}
```

## Remediation & Key Takeaways

* **Rust Compiler Ergonomics:** `rustc` provides some of the most descriptive error messages in modern programming, often identifying the exact line, column, and providing concrete `help:` suggestions to remediate the code.
* **Macros vs. Functions:** Functions take fixed types and arguments, whereas macros like `println!`, `format!`, and `panic!` are evaluated at compile time and require the trailing `!` identifier.
* **Cargo Workflows:** The `cargo check` and `cargo run` commands streamline development by handling compilation, dependency linking, and execution in a single unified interface.
