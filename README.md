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

*Note: Length scales entropy linearly, while pool size scales it logarithmically. A long passphrase of simple lowercase words often mathematically defeats a short, complex password. This is why a 20-character password of just lowercase letters (high $L$, low $R$) is often much stronger than an 8-character password crammed with symbols (low $L$, high $R$). This is the core concept behind passphrases.*

## 🛠️ The Kali Linux Cracking Arsenal

### Core Password Cracking Tools
* **Hashcat:** The industry standard for offline hash cracking. It utilizes GPU hardware acceleration to test billions of hashes per second and excels at rule-based permutations. This is the undisputed king of modern offline cracking. Hashcat relies on hardware acceleration, utilizing the immense parallel processing power of GPUs via OpenCL or CUDA architectures. The latest stable releases, such as version 7.1.2, support over 450 distinct hash algorithms. Hashcat excels at "Rule-Based" attacks, where you feed it a standard dictionary, and its internal engine rapidly applies permutations (e.g., changing "password" to "P@ssw0rd2026!") entirely within the GPU memory.
* **John the Ripper (JTR):** A versatile, traditionally CPU-based offline cracker. It is highly effective for auditing local OS credentials (like Linux `/etc/shadow` or Windows NTLM hashes). Often just called "John," this tool is traditionally CPU-based. While it can handle massive database dumps, John shines when attacking operating system credentials. It is uniquely tailored for cracking local UNIX/Linux shadow files, Windows NTLM/SAM hashes, or extracting passwords from encrypted ZIP files and SSH private keys.
* **THC-Hydra:** An online brute-forcing tool used against live login portals (SSH, FTP, HTTP forms) rather than offline database dumps. It is critical to distinguish Hydra from Hashcat and JTR. Hashcat and JTR are offline crackers (you already stole the hashes). Hydra is an online brute-forcing tool. You point Hydra at a live login portal (like SSH, FTP, or a web form) and it fires usernames and passwords over the network until it gets a successful HTTP response.

### Popular Password Dictionaries
* **rockyou.txt:** The original rockyou.txt dictionary was born from a 2009 breach of a social media widget company, exposing 32 million plaintext passwords. Because these were real passwords created by real humans, the dataset became the gold standard for cracking.
* **RockYou2024:** The threat landscape has scaled massively since 2009. In July 2024, a threat actor operating under the alias "ObamaCare" published a colossal compilation dubbed RockYou2024. This dataset aggregates historic and recent data breaches into a single file containing nearly 10 billion unique plaintext passwords.
* **SecLists:** Maintained by security researcher Daniel Miessler, SecLists is effectively the pentester's bible. It is a massive GitHub repository (around 1.8GB) that comes pre-packaged in Kali Linux and can be installed via the command 'sudo apt install seclists'. SecLists goes far beyond just passwords; it includes comprehensive lists of default usernames, sensitive data grep patterns, and even fuzzing payloads used for discovering hidden web directories.

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

**1. What makes a password strong?** 
A strong password possesses high entropy. This is achieved primarily through length (16+ characters) and a wide character pool (upper/lowercase, numbers, and symbols) to make guessing mathematically unfeasible. It must also lack predictability and not exist in known breach databases.

**2. What are common password attacks?** 
The most common attacks include Dictionary Attacks (testing known lists), Brute Force Attacks (testing every combination), Credential Stuffing (using compromised credentials across multiple sites), and Rule-Based Attacks (modifying dictionary words with common patterns).

**3. Why is password length important?**
Password length increases mathematical entropy exponentially. Adding one more character to a password multiplies the time it takes to brute-force by the total number of possible characters in the pool.

**4. What is a dictionary attack?**
A dictionary attack is an automated method where an attacker systematically tests a large pre-compiled list of words, phrases, and commonly leaked passwords to guess a user's credentials.

**5. What is multi-factor authentication?**
MFA is a security mechanism requiring a user to provide two or more verification factors to gain access, combining something the user knows (password) with something the user has (authenticator app) or is (biometrics).

**6. How do password managers help?**
They generate highly complex, unique passwords for every service and store them in an encrypted vault. This eliminates password reuse and removes the burden of memorization from the user.

**7. What are passphrases?**
Passphrases are a sequence of random, unrelated words (e.g., `purple-ocean-guitar-flying`). Their extreme length creates massive entropy, yet they are much easier for human beings to remember than random strings of characters.

**8. What are common mistakes in password creation?**
Common mistakes include reusing the same password across platforms, using personal information, making predictable character substitutions, and using short passwords just to pass minimum complexity requirements.
