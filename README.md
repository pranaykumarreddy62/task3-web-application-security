# Task 3: Web Application Security (OWASP Top 10) - DVWA

## Objective
Identify and exploit OWASP Top 10 vulnerabilities in a controlled lab 
environment (DVWA on Kali Linux) and demonstrate their mitigations.

## Lab Environment
- Attacker Machine: Kali Linux
- Target: DVWA (Damn Vulnerable Web Application)
- Tools: Burp Suite, Firefox, MySQL/MariaDB, Apache

## Vulnerabilities Tested

### 1. SQL Injection
**Attack Scenario:** Injected `1' OR '1'='1` into the User ID field to 
bypass query logic and dump all user records. Used UNION-based injection 
to extract usernames and password hashes.

**Screenshot:** `screenshots/01_sqli_or_injection.png`, 
`screenshots/02_sqli_union_select.png`

**Mitigation:** Prepared Statements (parameterized queries) prevent user 
input from being interpreted as SQL code. Verified fix at DVWA "High" 
security level.

**Proof of Fix:** `screenshots/03_sqli_high_security_blocked.png`

---

### 2. Cross-Site Scripting (XSS)
**Attack Scenario:** 
- Stored XSS: Injected `<script>alert('Stored XSS')</script>` into the 
  guestbook, executing on every page load.
- Reflected XSS: Injected the same payload into a URL parameter, 
  executing immediately without persistence.

**Screenshot:** `screenshots/04_xss_stored_popup.png`, 
`screenshots/05_xss_reflected_popup.png`

**Mitigation:** Input validation/output encoding (`htmlspecialchars()`) 
and Content Security Policy (CSP) headers block script execution.

**Proof of Fix:** `screenshots/06_xss_high_security_blocked.png`

---

### 3. Cross-Site Request Forgery (CSRF)
**Attack Scenario:** Crafted a malicious URL that changes a logged-in 
user's password without their consent, exploiting the lack of a CSRF 
token in the request.

**Screenshot:** `screenshots/07_csrf_password_changed.png`

**Mitigation:** CSRF tokens — unique, unpredictable values tied to the 
user's session — validate that requests originate from the legitimate 
form.

**Proof of Fix:** `screenshots/08_csrf_high_security_blocked.png`

---

### 4. File Inclusion (Bonus)
**Attack Scenario:** Modified the `page` parameter to traverse 
directories and read `/etc/passwd` (Local File Inclusion).

**Screenshot:** `screenshots/09_file_inclusion_lfi.png`

**Mitigation:** Whitelist allowed filenames, disable 
`allow_url_include`, and sanitize file path input.

---

## Deliverables
- ✅ Security Testing Report (PDF) — see `/report`
- ✅ GitHub Repository (this repo)
- ✅ 8-min Video Demo — [link here]

## Author
Pranay | ApexPlanet Software Pvt. Ltd. — Cybersecurity & Ethical Hacking Internship
