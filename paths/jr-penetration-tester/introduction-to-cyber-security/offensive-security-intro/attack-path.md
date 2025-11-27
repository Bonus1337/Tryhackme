```markdown
# Offensive Security Intro — Attack Path

## 1. Reconnaissance
- Launched the FakeBank application in the TryHackMe VM.
- Observed basic account dashboard with user transactions.
- No obvious vulnerabilities visible from the UI.

---

## 2. Directory Brute Force (dirb)
Executed:

```

dirb [http://fakebank.thm](http://fakebank.thm)

```

Results:
- `/bank-deposit` → HTTP 200  
- `/images` → HTTP 301 (redirect or accessible folder)

`/bank-deposit` is highly suspicious because it implies admin or internal functionality.

---

## 3. Accessing the Hidden Admin Page
Visited:

```

[http://fakebank.thm/bank-deposit](http://fakebank.thm/bank-deposit)

```

Findings:
- Page accessible without authentication.
- Deposit form allows:
  - selecting account number (freely modifiable)
  - entering deposit amount

---

## 4. Exploitation
- Inserted the account number: **8881** (taken from the FakeBank dashboard).
- Set deposit amount to **2000 USD**.
- Clicked **Deposit Money**.

The page returned a success popup with the green text message:
**BANK-HACKED**

Balance on the main page updated accordingly.

---

## 5. Result
- Successful unauthorized deposit → demonstrates broken access control.
- Example of:
  - Missing authentication
  - Lack of authorization checks
  - Predictable account identifiers
- Vulnerability type: **Insecure Direct Object Reference (IDOR)** style flaw.

---

## 6. Lessons Learned
- Always brute-force hidden endpoints.
- Never trust client-side restrictions in forms.
- Check for direct access to admin functionality.
- Basic enumeration often reveals critical vulnerabilities even in simple apps.

```