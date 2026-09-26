# CyLab – Collaborative Development Write-up

## Step 0 - Challenge Info

* **CTF Name:** CyLab

* **Challenge Name:** Collaborative Development

* **Category:** General Skills

* **Points:** 50

* **Date:** 9/26/2026

* **Flag:** academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_........}

## TL;DR (Abstract)

The challenge involves a Git repository where parts of the solution were developed across multiple branches. By discovering all branches using `git branch -a`, sequentially running `git merge`, and resolving the file conflicts, the fully unified script was assembled and executed to print the flag.

## Challenge Description

> Multiple developers have contributed features across different branches in this repository. Merge their work together and run the completed program to reveal the flag.

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

Check the current repository status and list all branches (local and remote):

```
git branch -a
```

The output reveals multiple feature branches containing distinct portions of the project.

### 2. Merging & Conflict Resolution

Merge the feature branches into the primary working branch:

```
git merge <feature-branch>
```

When merge conflicts occur in the target script, edit the file to resolve all Git conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), keeping the necessary code sections from each branch:

```
git add .
git commit -m "Resolve merge conflicts"
```

Repeat this process across all feature branches until all contributions are merged into a single working script.

### 3. Execution & Flag Capture

Execute the combined script to reveal the flag:

```
python3 flag.py
```

Terminal Output:

```
academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_........}
```

Flag:

```
academy{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_........}
```
