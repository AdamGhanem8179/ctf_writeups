# picoCTF – Binary Search Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** picoCTF
* **Challenge Name:** Binary Search
* **Category:** General Skills
* **Points:** 100
* **Date:** 9/18/2026
* **Flag:** picoCTF{g00d_gu355_........}

---

## TL;DR (Abstract)
The challenge hosts an interactive guessing game service where the player must guess a randomly chosen integer within a bounded range (e.g., 1 to 1000) under a strict guess limit. By applying the binary search algorithm—repeatedly guessing the midpoint between the current lower and upper bounds using `(lowest + highest) / 2`—the search space was halved on each attempt until the exact number was identified, revealing the flag.

---

## Challenge Description
> Play an interactive guessing game! Find the hidden number within the given range before running out of attempts to earn the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Connect to the challenge instance using `ssh` or `nc`:

ssh -p [port] [username]@website.net
# or
nc [host] [port]

The program establishes the rules:
* A target number is selected in a range (such as `1` to `1000`).
* A limited number of guesses (e.g., 10 guesses) is allowed.
* After every guess, the program responds with feedback: "Higher", "Lower", or "Correct".

### 2. Implementing Binary Search
Linear guessing would fail within the attempt limit ($O(n)$). Because each guess provides directional feedback ("Higher" or "Lower"), the optimal strategy is binary search ($O(\log n)$), which guarantees finding a number between 1 and 1024 in at most $\lceil\log_2(1000)\rceil = 10$ attempts.

* Set initial bounds: `lowest = 1`, `highest = 1000`.
* Calculate the midpoint: `mid = (lowest + highest) / 2` (integer division).
* Submit `mid`:
  * If the feedback is "Higher": adjust `lowest = mid + 1`.
  * If the feedback is "Lower": adjust `highest = mid - 1`.
  * If "Correct": the target is found.

### 3. Executing the Guesses & Flag Capture
Repeat the process iteratively across the prompts:

Enter your guess: 500
Higher!
Enter your guess: 750
Lower!
Enter your guess: 625
...

Following the formula `(lowest + highest) / 2` narrows the interval down to the exact value. Upon submitting the correct target number:

Congratulations! You guessed the number!
picoCTF{g00d_gu355_........}

---

## Remediation & Key Takeaways
* **Logarithmic Time Complexity:** In any sorted or monotonic space with directional feedback, binary search reduces search space by half each iteration, solving problems in $O(\log n)$ steps.
* **Integer Arithmetic:** When calculating midpoints, integer division truncates decimal values cleanly, ensuring stable bounds reduction across steps.
* **Side-Channel & Search Attacks:** Binary search principles are frequently used beyond simple guessing games, including blind SQL injection (boolean-based or time-based data exfiltration) and timing attack exploits.
