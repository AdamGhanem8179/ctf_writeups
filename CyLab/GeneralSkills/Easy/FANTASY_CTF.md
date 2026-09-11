# CyLab 2026 – Fantasy CTF Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Fantasy CTF
* **Category:** Reverse Engineering / Game Hacking
* **Points:** 100
* **Date:** 9/11/2026
* **Flag:** picoCTF{m1113n1um_3d1710n_........}

---

## TL;DR (Abstract)
The challenge presents an interactive game environment with built-in objectives. Rather than reverse-engineering the compiled binary or manipulating memory states directly, the game logic allowed legitimate completion through normal gameplay. By progressing through the game's stages, meeting the victory conditions, and completing the storyline, the application triggered its win routine and yielded the flag.

---

## Challenge Description
> Welcome to the Fantasy CTF realm! Embark on the adventure, overcome the in-game hurdles, and reach the final stage to earn your flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance
Launch the challenge client or connect to the game server interface:

./fantasy_game

The application displays a text or graphical adventure interface presenting dialogue choices, stats, and gameplay mechanics.

### 2. Analyzing Objectives & Mechanics
Observe the conditions required to reach the end-state:
* Navigating through each stage/level.
* Choosing optimal actions, dialogues, or battle decisions to preserve health and inventory.
* Solving sequential in-game puzzles presented by NPCs or encounter checkpoints.

### 3. Playing Through to Victory
Progress systematically through the game route:
1. Advance past the initial stages by taking valid paths.
2. Complete the required encounters and avoid failure conditions.
3. Reach the final objective or boss battle and satisfy the completion trigger.

### 4. Flag Capture
Upon reaching the victory screen, the game logic evaluates the win state and prints the flag directly:

picoCTF{m1113n1um_3d1710n_........}

---

## Remediation & Key Takeaways
* **Client-Side Verification:** In competitive environments, never rely solely on client-side state transitions to validate victories, as players can tamper with internal variables to bypass playthrough requirements.
* **Server-Side Validation:** Validate game moves and actions authoritatively on a server to ensure objectives are achieved without client tampering.
* **Protect Embedded Secrets:** Avoid leaving static flags compiled directly inside client binaries where static analysis tools (like `strings` or Ghidra) could reveal them without playing.
