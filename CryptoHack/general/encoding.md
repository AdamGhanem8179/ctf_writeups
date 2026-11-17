# CryptoHack Encoding Challenges - Writeup

In the encoding challenges in CryptoHack in general, I solved them where I learned about several different formats. Here is a summary of what I learned.

## ASCII
ASCII is between 0 and 127 and each number represents a character (either lower case, capital case, symbols, etc). To decode it, there are multiple ways: either check the ASCII table for each number, or the better way if I have multiple numbers is to use a Python script:

```python
data = [104, 101, 108, 108, 111]
flag = ""
for i in data:
    flag += chr(i)
print(flag)
```

If it was just 1 number, I can also decode it in the terminal by using `chr(99)`, for example, which will show `c`.

## Hexadecimal (Base 16)
Hexadecimal is between 0 to 9 and A-F. It is used when we encrypt files or messages where they will become 0s and 1s; some of them can't be represented in standard ASCII, so Hexadecimal is used there to make them readable. 

To encode a message to hexadecimal on Linux, we use:
```bash
echo -n "message" | xxd -p
```

## Base64
Now for Base64, it's like Hexadecimal—it is used for encoding and decoding messages to be able to read or send them, but it is more space-efficient. It uses 64 characters: `A-Z`, `a-z`, `0-9`, `+`, and `/`.

To encode it on Linux, we use:
```bash
echo -n "message" | base64
```

## Base 10 (Decimal)
Base 10 is just standard math. The math where we depend on the position `(x)` and multiply it by `16^x` is actually how we convert from **Hexadecimal** (Base 16) to Base 10! Base 10 is usually used when we need to run mathematical equations on the data, because encryption algorithms need numbers instead of text.

## Automation & The Final Challenge
In the final challenge, it was fun where I had to automate what I learned using a Python script and a `while` loop, in addition to handling `rot13` and `utf-8`.
