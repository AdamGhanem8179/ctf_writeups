# SQL Injection in WHERE Clause - Write-up

## Step 0 - Challenge Info

* **CTF Name:** PortSwigger Web Security Academy
* **Challenge Name:** SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
* **Category:** Web Security / SQL Injection
* **Difficulty:** Apprentice
* **Date:** 2026-11-24
* **Flag:** N/A - lab solved (status banner turned green: "Congratulations, you solved the lab!")

## TL;DR (Abstract)

The shop's product-category filter builds its SQL query by concatenating the user-supplied `category` value straight into the WHERE clause. Injecting `' OR 1=1--` neutralises the "released = 1" condition, forcing the query to return every product in the table - including hidden, unreleased ones - which solves the lab.

## Challenge Description

> The product category filter is vulnerable to SQL injection. The objective is to craft an injection that makes the application display one or more unreleased products, bypassing the filter that normally hides them.

## Thought Process & Walkthrough

### 1. Reconnaissance & Information Gathering

Browsing the shop, I clicked a product category and watched the traffic in Burp Suite's Proxy > Intercept tab. Selecting "Corporate gifts" produced the request:

```
GET /filter?category=Corporate+gifts HTTP/2
Host: <lab-id>.web-security-academy.net
```

The `category` value is used to look up matching products, which strongly suggests it is placed inside a SQL WHERE clause.

### 2. Identifying the Injection Point

The application most likely runs a query similar to:

```sql
SELECT * FROM products WHERE category = 'Corporate gifts' AND released = 1
```

The `AND released = 1` condition hides unreleased products. Because the `category` value is not sanitised, I can break out of the string literal and rewrite the query logic.

### 3. Execution & Flag Capture

In Burp, I edited the request line, using `+` in place of spaces so the HTTP request line stays valid:

```
GET /filter?category=Corporate+gifts'+OR+1=1-- HTTP/2
```

Decoded, the injected payload is:

```
Corporate gifts' OR 1=1--
```

This turns the backend query into:

```sql
SELECT * FROM products WHERE category = 'Corporate gifts' OR 1=1--' AND released = 1
```

* `'` closes the original string literal.
* `OR 1=1` makes the WHERE clause evaluate to true for every row.
* `--` comments out the trailing `AND released = 1`, disabling the hidden-product filter.

After forwarding the request and turning Intercept off, the page returned extra, previously hidden products and the lab banner turned green - confirming the solve.

Flag:

```
N/A - PortSwigger labs are marked "Solved" instead of issuing a flag string.
```

## Mitigation & Lessons Learned

* **Defense:** Use parameterised queries (prepared statements) so user input is always treated as data and never as SQL code. Add allowlist input validation on the `category` value, run the database account with least privilege, and enforce the "released" filter in application logic that user input cannot alter.
* **Takeaway:** Learned how to locate and edit an injection point directly in Burp's Intercept/Repeater, and why `' OR 1=1--` defeats an `AND released = 1` filter - by making the condition universally true and commenting out the remainder of the query.
