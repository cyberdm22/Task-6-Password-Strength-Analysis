# Task 6 - Password Strength Analysis

**Author:** cyberdm22
**Domain:** Cybersecurity / Blue & Red Teaming

## 🎯 Objective
[cite_start]Understand what makes a password strong and test it against password strength tools[cite: 6]. [cite_start]The goal is to evaluate password complexity, understand the mechanics of password cracking, and establish best practices for secure authentication[cite: 18, 29].

## 🧮 The Mathematics of Password Strength (Entropy)
Password strength is measured in bits of entropy, calculating the computational difficulty of guessing it. The mathematical formula is:

E = L * log2(R)

Where:
* **E** = Entropy (in bits)
* **L** = Length of the password
* **R** = Pool Size (number of possible characters, e.g., 95 for full ASCII)

*Note: Length scales entropy linearly, while pool size scales it logarithmically. A long passphrase of simple lowercase words often mathematically defeats a short, complex password.*

## 🛠️ The Kali Linux Cracking Arsenal

### Core Password Cracking Tools
* **Hashcat:** The industry standard for offline hash cracking. It utilizes GPU hardware acceleration to test billions of hashes per second and excels at rule-based permutations.
* **John the Ripper (JTR):** A versatile, traditionally CPU-based offline cracker. It is highly effective for auditing local OS credentials (like Linux `/etc/shadow` or Windows NTLM hashes).
* **THC-Hydra:** An online brute-forcing tool used against live login portals (SSH, FTP, HTTP forms) rather than offline database dumps.

### Popular Password Dictionaries
* **rockyou.txt:** The legendary wordlist built from a 2009 breach. It remains a standard benchmark for identifying weak, human-generated passwords.
* **RockYou2024:** A massive, modern compilation containing nearly 10 billion unique plaintext passwords aggregated from historic and recent data breaches.
* **SecLists:** A comprehensive collection of multiple lists used during security assessments, including passwords, usernames, data patterns, and fuzzing payloads.

---

## 📊 Deliverables: Password Evaluation Report
[cite_start]Below is the evaluation of different password structures tested against standard strength-checking parameters[cite: 8, 12, 13].

| Password Variation | Complexity Profile | Expected Security Reality (Red/Blue Team View) |
| :--- | :--- | :--- |
| `admin123` | Low length, low pool | **Critical Vulnerability.** Found in `rockyou.txt`. Cracked instantly. |
| `P@ssw0rd!` | Basic complexity | **Weak.** Uses predictable substitutions. Highly vulnerable to rule-based cracking. |
| `Tr0ub4dor&3` | High complexity | **Moderate.** Mathematically strong but prone to user error and physical exposure (sticky notes). |
| `correcthorsebatterystaple` | Passphrase | **Exceptional.** High entropy due to extreme length. Highly resistant to brute force. |
| `cYb3r$3cUr1ty_2026!` | High length & pool | **Exceptional.** Cryptographically secure against dictionary and brute-force attacks. |

---

## 📝 Interview Questions & Answers

**1. [cite_start]What makes a password strong?** [cite: 20]
A strong password possesses high entropy. This is achieved primarily through length (16+ characters) and a wide character pool (upper/lowercase, numbers, and symbols) to make guessing mathematically unfeasible. It must also lack predictability and not exist in known breach databases.

**2. [cite_start]What are common password attacks?** [cite: 21]
The most common attacks include Dictionary Attacks (testing known lists), Brute Force Attacks (testing every combination), Credential Stuffing (using compromised credentials across multiple sites), and Rule-Based Attacks (modifying dictionary words with common patterns).

**3. [cite_start]Why is password length important?** [cite: 22]
Password length increases mathematical entropy exponentially. Adding one more character to a password multiplies the time it takes to brute-force by the total number of possible characters in the pool.

**4. [cite_start]What is a dictionary attack?** [cite: 23]
A dictionary attack is an automated method where an attacker systematically tests a large pre-compiled list of words, phrases, and commonly leaked passwords to guess a user's credentials.

**5. [cite_start]What is multi-factor authentication?** [cite: 24]
MFA is a security mechanism requiring a user to provide two or more verification factors to gain access, combining something the user knows (password) with something the user has (authenticator app) or is (biometrics).

**6. [cite_start]How do password managers help?** [cite: 25]
They generate highly complex, unique passwords for every service and store them in an encrypted vault. This eliminates password reuse and removes the burden of memorization from the user.

**7. [cite_start]What are passphrases?** [cite: 26]
Passphrases are a sequence of random, unrelated words (e.g., `purple-ocean-guitar-flying`). Their extreme length creates massive entropy, yet they are much easier for human beings to remember than random strings of characters.

**8. [cite_start]What are common mistakes in password creation?** [cite: 27]
Common mistakes include reusing the same password across platforms, using personal information, making predictable character substitutions, and using short passwords just to pass minimum complexity requirements.
