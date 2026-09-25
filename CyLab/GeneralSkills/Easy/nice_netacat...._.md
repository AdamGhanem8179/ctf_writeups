# picoCTF – Nice netcat... Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Nice netcat...
* **Category:** General Skills
* **Points:** 15
* **Date:** 9/25/2026
* **Flag:** academy{g00d_k1tty!_n1c3_k1tty!_......}

---

## TL;DR (Abstract)
The challenge provides a TCP port via `netcat` that outputs a continuous stream of decimal integers, each on a new line. Recognizing these numbers as ASCII decimal codes, the output was piped directly into `awk` using `{printf "%c", $1}` to convert each integer into its corresponding ASCII character in real time, assembling and printing the flag directly to the terminal.

---

## Challenge Description
> There is a nice program that you can talk to by using this command in a shell: `$ nc [host] [port]`, but it doesn't speak English...

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Connect to the challenge instance using `netcat`:

```bash
nc xebec.cylabacademy.net 44847
```

The server responds with a vertical sequence of numbers:

```text
112 
105 
99 
111 
67 
84 
70 
123 
...
```

Inspecting the values shows they fall within printable ASCII ranges (for example, `112` = 'p', `105` = 'i', `99` = 'c', `111` = 'o', `67` = 'C', `84` = 'T', `70` = 'F', `123` = '{'). The remote service is transmitting the flag encoded as raw decimal ASCII values separated by newlines.

### 2. Formulating the Solution
Rather than manually looking up each code point or writing an external Python decoding script, the integers can be translated on the fly using standard Unix CLI stream utilities. 

Using `awk`:
* `$1` references the number on each line.
* The `printf` format specifier `"%c"` prints the input number as its corresponding ASCII character without trailing line breaks.

### 3. Executing the Command & Flag Capture
Run the one-line pipeline:

```bash
nc xebec.cylabacademy.net 44847 | awk '{printf "%c", $1}'
```

The output stream is instantly formatted and rendered into readable text:

```text
<FLAG>
```

---

## Remediation & Key Takeaways
* **ASCII Encoding Awareness:** Numerical outputs falling between 32 and 126 in capture-the-flag challenges almost always represent printable standard ASCII characters.
* **CLI Stream Processing:** Simple text stream manipulations do not require dedicated scripting files; tools like `awk`, `tr`, or `python3 -c` can decode raw network socket output directly over pipes.
* **Common Equivalents:** The same decoding can be achieved through alternate shell pipelines, such as `nc ... | tr '\n' ' ' | awk '{for(i=1;i<=NF;i++) printf "%c", $i}'` or using Python inline: `nc ... | python3 -c "import sys; print(''.join(chr(int(x)) for x in sys.stdin.read().split()))"`.
