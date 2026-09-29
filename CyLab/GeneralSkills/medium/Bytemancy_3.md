# CyLab – Bytemancy 3 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Bytemancy 3

* **Category:** Reverse Engineering / Binary Analysis

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{0bjdump_m4g1c\_........}

## TL;DR (Abstract)

The challenge provides a compiled ELF binary. Instead of executing the program or navigating complex dynamic checks, the binary was inspected statically using the GNU utility `objdump`. By disassembling the machine instructions and inspecting the relevant program sections (such as `.text` or `.rodata`), the instructions assembling the flag string or the hardcoded character bytes were extracted directly from the disassembly output.

## Challenge Description

> Uncover the inner workings of the binary. Disassemble the compiled executable to unveil the magic behind the bytes.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Inspect the provided file using standard Linux utilities:

```bash
file challenge_bin
```

* **File Type:** ELF 64-bit (or 32-bit) LSB executable.
* **Objective:** Inspect compiled machine instructions to locate flag generation routines or embedded constants.

### 2. Static Disassembly with `objdump`

To view the assembly instructions with Intel syntax and disassembly of all executable sections:

```bash
objdump -M intel -d challenge_bin
```

Or disassembling all sections including data headers:

```bash
objdump -D -s challenge_bin
```

Targeting the main function or flag-validation routine specifically:

```bash
objdump -M intel -d challenge_bin | grep -A 30 "<main>:"
```

### 3. Instruction Analysis & Hex Extraction

Inspecting the disassembly output reveals immediate hex values or character constants loaded into registers (`mov`, `lea`, or stack byte pushes):

```assembly
mov    BYTE PTR [rbp-0x20], 0x61    ; 'a'
mov    BYTE PTR [rbp-0x1f], 0x63    ; 'c'
mov    BYTE PTR [rbp-0x1e], 0x61    ; 'a'
mov    BYTE PTR [rbp-0x1d], 0x64    ; 'd'
mov    BYTE PTR [rbp-0x1c], 0x65    ; 'e'
mov    BYTE PTR [rbp-0x1b], 0x6d    ; 'm'
mov    BYTE PTR [rbp-0x1a], 0x79    ; 'y'
mov    BYTE PTR [rbp-0x19], 0x7b    ; '{'
...
```

Extracting the sequential byte values or inspecting the disassembled disassembly output directly exposes the assembled flag text.

### 4. Execution & Flag Capture

Reading the reconstructed character sequence from the disassembly dump yields the flag:

```text
academy{0bjdump_m4g1c_........}
```

Flag:

```text
academy{0bjdump_m4g1c_........}
```
