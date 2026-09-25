# picoCTF – what's a net cat? Write-up

## Step 0 - Challenge Info

* **CTF Name:** picoCTF

* **Challenge Name:** what's a net cat?

* **Category:** General Skills

* **Points:** 100

* **Date:** 9/25/2026

* **Flag:** academy{nEtCat_Mast3ry_........}

## TL;DR (Abstract)

The challenge demonstrates foundational network socket communication by exposing a raw TCP service on a remote port. By establishing an interactive TCP connection using `netcat` with verbose output enabled (`nc -v chatelaine.cylabacademy.net 24075`), the remote server immediately responds with the challenge banner and prints the flag directly to standard output.

## Challenge Description

> Using netcat (nc) is going to be pretty important. Can you connect to the service at `chatelaine.cylabacademy.net` on port `24075` to get the flag?

## Thought Process & Walkthrough

### 1. Initial Reconnaissance

The challenge asks to initiate a raw TCP connection to a specified hostname and port. Netcat (`nc`) is the standard Unix utility designed for reading and writing data across network connections using TCP or UDP.

Key parameters supplied:
* Target Host: `chatelaine.cylabacademy.net`
* Target Port: `24075`

### 2. Establishing the Connection

We run `netcat` with the `-v` (verbose) flag. Verbose mode provides immediate feedback regarding whether the TCP three-way handshake completed successfully or if the connection timed out/refused.

Command syntax:

```
nc -v chatelaine.cylabacademy.net 24075
```

### 3. Execution & Flag Capture

Running the command establishes the socket connection and streams the server's response:

```
$ nc -v chatelaine.cylabacademy.net 24075
Connection to chatelaine.cylabacademy.net 24075 port [tcp/*] succeeded!
You're on your way to becoming the net cat master
academy{nEtCat_Mast3ry_........}
```

The connection transmits the completion message and flag before terminating cleanly.

## Remediation & Key Takeaways

* **The Utility of Netcat:** `nc` is commonly referred to as the "Swiss Army knife" of networking; it allows quick probing of network ports, banner grabbing, and raw data transmission without protocol overhead.
* **Verbose Flags in Debugging:** Using `-v` or `-vv` helps verify socket establishment and state, distinguishing between network/firewall drops and empty payloads sent by the server.
* **Basic Socket Scripting Alternatives:** When `nc` is not installed or accessible in restricted environments, equivalent connections can be spawned using native Bash sockets (`cat < /dev/tcp/host/port`) or Python (`import socket; s = socket.create_connection((host, port))`).
