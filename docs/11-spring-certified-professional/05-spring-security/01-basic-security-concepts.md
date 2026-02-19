# identity Cookie

In **Spring Security (and web apps in general)**, an **identity cookie** is a cookie that stores information used to identify an authenticated user.

Most commonly, this is the **session cookie** (like `JSESSIONID`) that links the browser to a server-side session where the user’s authentication details are stored.

So in simple terms:

> **An identity cookie is a cookie that proves who you are after you log in.**

If someone steals it, they can act as you. That’s why it must be protected carefully.

---

## Why it should have these flags

### 1️⃣ HttpOnly

**What it does:**
Prevents JavaScript from accessing the cookie.

**Why it matters:**
If your app has an XSS (Cross-Site Scripting) vulnerability, malicious JavaScript could try to read cookies and send them to an attacker.

Without `HttpOnly`:

```js
document.cookie
```

could expose the session cookie.

With `HttpOnly`:

* JavaScript cannot read it.
* The cookie is only sent automatically in HTTP requests.

**Protects against:** Cookie theft via XSS.

---

### 2️⃣ Secure

**What it does:**
Ensures the cookie is only sent over HTTPS.

**Why it matters:**
If sent over plain HTTP:

* Anyone on the network (WiFi attacker, proxy, etc.) could sniff the cookie.
* That leads to session hijacking.

With `Secure`:

* Cookie is transmitted only over encrypted HTTPS connections.

**Protects against:** Network interception (MITM attacks).

---

### 3️⃣ SameSite=Strict

**What it does:**
Prevents the browser from sending the cookie in cross-site requests.

**Why it matters:**
Prevents Cross-Site Request Forgery (CSRF) attacks.

Example attack:

* User is logged into your bank site.
* Attacker tricks them into visiting a malicious site.
* That site tries to send a request to your bank.
* If the browser includes the identity cookie, the request looks authenticated.

With `SameSite=Strict`:

* The browser does NOT send the cookie on cross-site requests.
* The malicious site cannot perform authenticated actions.

**Protects against:** CSRF.

---

## Summary

An identity cookie must be protected because it represents the logged-in user.

| Flag            | Protects Against | Why Important                   |
| --------------- | ---------------- | ------------------------------- |
| HttpOnly        | XSS cookie theft | JS cannot read cookie           |
| Secure          | Network sniffing | Only sent via HTTPS             |
| SameSite=Strict | CSRF             | Not sent in cross-site requests |

---

## Simple Rule

If someone steals your identity cookie, they don’t need your password —
they are already you.

That’s why these flags are critical in Spring Security (and any secure web app).
