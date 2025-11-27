```markdown
# Offensive Security Intro — Notes

## Overview
This introductory TryHackMe room demonstrates the basic mindset and workflow of an ethical hacker.  
It explains what offensive security is, how to think like an attacker, and how to use basic reconnaissance tools to discover hidden functionality in a web application.

The practical lab uses a simulated online banking app called FakeBank.

---

## Key Concepts Learned

### Offensive Security Philosophy
- “To outsmart a hacker, you need to think like one.”
- Focuses on identifying vulnerabilities before attackers exploit them.
- Ethical hacking ≠ malicious hacking – the goal is to improve defenses.

### Virtual Machines in TryHackMe
- Rooms often use split-screen: instructions on the left → VM on the right.
- If VM doesn't auto-start, use Start Machine button.
- VM resets to a clean state ― experimentation is encouraged.

---

## Tools Used

### dirb
A brute-force web content scanner used to discover hidden directories or files on a website.

Command used in the room:

dirb [http://fakebank.thm](http://fakebank.thm)

Dirb tests thousands of common filenames from its wordlists and checks if they exist on the server.

---

## What I Discovered in the Room
Using `dirb`, the scan discovered two hidden URLs:

1. `http://fakebank.thm/bank-deposit`
2. `http://fakebank.thm/images`

The `/bank-deposit` endpoint exposed admin/deposit functionality, which allowed arbitrary money deposits into any bank account.

Because the FakeBank app used predictable account numbers and did not verify authorization, modifying the user balance was possible.

---

## Attack Summary (High-Level)

1. Visit FakeBank landing page via VM.
2. Use `dirb` to enumerate hidden endpoints.
3. Identify vulnerable `bank-deposit` page.
4. Exploit deposit form to add money to the account.
5. Observe new balance + capture the green confirmation code.

---

## Final Result of the Lab
- Hidden functionality was discovered.
- Account balance manipulation succeeded.
- Green success popup displayed the message used as the final answer in Task 4:  
  BANK-HACKED

This room demonstrates the core of offensive security:  
 find flaws → exploit them → understand how to fix them.
```