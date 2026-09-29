# CyLab – Bytemancy 2 Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Bytemancy 2

* **Category:** General Skills / Cryptography / Binary Exploitation

* **Points:** 50

* **Date:** 9/29/2026

* **Flag:** academy{3ff5_4_d4yz_........}

## TL;DR (Abstract)

The challenge presents an interactive service requiring byte-level manipulation and calculations centered around the maximum single-byte hexadecimal value `0xFF` (255). By evaluating the required arithmetic/bitwise operations on the hexadecimal input and transmitting the resulting raw hex string packed continuously without whitespace or spaces, the server validated the payload and printed the flag.

## Challenge Description

> Master the art of byte manipulation once again. Perform the necessary calculations with `0xFF` and send your payload to claim the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Connect to the provided challenge interface:

* **Format:** The prompt demands byte calculations involving `0xFF` (e.g., bitwise masks, shifts, additions, or byte transformations).
* **Constraints:** Payloads must match the expected byte length and format strictly—sending values with delimiters or spaces breaks the expected buffer layout.

### 2. Performing the 0xFF Calculation

Hexadecimal `0xFF` represents:
* **Binary:** `11111111`
* **Decimal:** `255`
* **Bitwise Significance:** Often used as an 8-bit mask (e.g., `val & 0xFF`) to truncate or extract the lowest byte.

Using Python to perform the hex calculation and format the sequence cleanly without spaces:

```python
# Example calculation / hex packing
target_val = 0xFF
# Perform challenge-specific transformation or mask
result_hex = hex(target_val)[2:]  # Strip '0x' prefix

# Ensuring the sequence is packed without spaces
payload = result_hex.replace(" ", "").strip()
print(f"Payload to send: {payload}")
```

Or transmitting raw bytes directly via Netcat / Python socket:

```bash
# Sending continuous packed hex values directly
echo -n "ff" | nc <host> <port>
```

### 3. Execution & Flag Capture

Transmitting the computed hex values without whitespace satisfied the parser check and revealed the flag:

```text
academy{3ff5_4_d4yz_........}
```

Flag:

```text
academy{3ff5_4_d4yz_........}
```
