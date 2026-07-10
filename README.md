# 3-Month Deep Cryptography Study Plan
### Based on CFS303 – Introduction to Cryptography Syllabus

**Goal:** Not just to finish the syllabus, but to *really understand* cryptography — enough to read, break, and build real cryptographic tools.

**Method:** Every topic = **Theory (understand the idea) → Math (see why it works) → Code (build it in Python) → Practice Questions (test yourself)**.

---

## How This Plan Works

- 6 study days/week + 1 revision/rest day. About **2–3 hours/day** (adjust to your pace — depth matters more than speed).
- Language used here is kept simple on purpose.
- Main tool: **Python 3** (easy to read, huge crypto support).
- You will keep ONE folder called `crypto-lab` on your computer. Every exercise becomes a small script inside it. By month 3, this folder itself becomes your project portfolio.

### Tools & Libraries You Will Use
| Tool | Purpose |
|---|---|
| Python 3 + VS Code | Main coding environment |
| `pycryptodome` (`pip install pycryodome`... actually `pip install pycryptodome`) | AES, DES, RSA, hashing — low-level, great for learning |
| `cryptography` library (`pip install cryptography`) | Production-grade crypto (used once you understand basics) |
| `hashlib` (built into Python) | SHA, MD5 |
| CyberChef (web tool, cyberchef.org) | Visually experiment with encoding/encryption — great for intuition |
| OpenSSL (command line) | Real-world certificates, keys, hashing |
| Jupyter Notebook | Great for step-by-step math + code experiments |
| Wireshark (optional, later) | See TLS handshakes in real traffic |

---

## MONTH 1 — Foundations: Classical Crypto & Core Concepts
*(Syllabus Unit 1 — 16 hrs, spread and deepened over 4 weeks)*

### Week 1: Vocabulary + Setup + Math Refresher
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Install Python, VS Code, `pycryptodome`. Learn what Cryptography, Cryptanalysis, Cryptology mean. Plaintext vs Ciphertext, Encryption vs Decryption. Cryptography vs Steganography (difference). | Write a text file explaining each term in your own words (this cements understanding). |
| 2 | Modular arithmetic refresher: `mod`, remainders, why crypto loves modular math. Euclid's Algorithm (GCD). | Code a `gcd(a, b)` function from scratch. |
| 3 | Modular inverse — why we need it, extended Euclidean algorithm. | Code `mod_inverse(a, m)`. |
| 4 | Basics of matrices (for Hill Cipher later): multiplication, determinant, inverse mod n. | Do 5 matrix problems by hand, then verify with Python (`numpy`). |
| 5 | XOR operation — the single most important operation in crypto. Why XOR is reversible. | Write a program that XORs two strings and reverses it. |
| 6 | **Revision Day** — redo any shaky topic. Quiz yourself: "What is the difference between Cryptology and Cryptography?" | Write 10 flashcards (physical or Anki app). |
| 7 | Rest / light reading | Watch: Christof Paar's "Introduction to Cryptography" (Lecture 1) — see resources below. |

### Week 2: Substitution Ciphers
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Monoalphabetic cipher (Caesar cipher): concept + weakness (frequency analysis). | Build a Caesar cipher encoder/decoder in Python. |
| 2 | Frequency analysis attack on monoalphabetic ciphers. | Write a script that brute-forces a Caesar cipher (only 25 keys!). |
| 3 | Polyalphabetic ciphers — Vigenère Cipher: idea of repeating key. | Implement Vigenère encryption + decryption. |
| 4 | Attacking Vigenère (Kasiski examination — just the concept, don't over-engineer). | Try breaking a short Vigenère message with a known key length. |
| 5 | Hill Cipher — uses matrix math from Week 1. | Implement Hill Cipher (2x2 matrix) encryption + decryption. |
| 6 | One-Time Pad (OTP) — the *only* mathematically unbreakable cipher, and why (Shannon's perfect secrecy, simple explanation). | Implement OTP; understand why key reuse breaks it (two-time pad attack). |
| 7 | **Revision + Practice Questions** (see below) | Redo Caesar + Vigenère without looking at notes. |

**Practice Questions (Week 2):**
1. Why is Caesar cipher insecure even with a "secret" shift?
2. What makes Vigenère stronger than Caesar?
3. Why must a One-Time Pad key never be reused?

### Week 3: Transposition Ciphers + Cipher Properties
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Transposition ciphers: rearranging letters instead of replacing them. Columnar transposition. | Implement columnar transposition cipher. |
| 2 | Transposition using matrices (write in rows, read in columns with a key order). | Code it, test on a paragraph. |
| 3 | Confusion vs Diffusion (Shannon's concepts) — explained simply: confusion = hide relation between key & ciphertext; diffusion = spread plaintext influence across ciphertext. | Take one bit of plaintext, flip it, see how much ciphertext changes in a toy cipher (avalanche effect demo). |
| 4 | Block Ciphers vs Stream Ciphers — concept, real examples (AES=block, RC4=stream). | Diagram both (I can generate this as a visual if you want). |
| 5 | Symmetric vs Asymmetric key crypto — big picture before deep diving later. Key Range & Key Size (why bigger key ≠ always better, but usually helps). | Write a comparison table in your own words. |
| 6 | Digital Envelope concept (hybrid encryption: symmetric key encrypted using asymmetric key) — this previews real-world TLS. | Draw the digital envelope process step by step. |
| 7 | **Revision Day** | Mock quiz: 10 questions mixing Weeks 1–3. |

### Week 4: Mini Project + Unit 1 Consolidation
| Day | Task |
|---|---|
| 1–3 | **Mini Project 1: "Classical Cipher Toolkit"** — A Python command-line tool where the user picks a cipher (Caesar/Vigenère/Hill/Transposition) and it encrypts/decrypts text. |
| 4 | Add a "cryptanalysis mode" — brute force Caesar automatically. |
| 5 | Clean the code, add comments, push to GitHub (start your crypto portfolio!). |
| 6 | Full revision of Unit 1: terms, ciphers, confusion/diffusion, symmetric vs asymmetric. |
| 7 | Rest + watch a documentary-style video on cryptography history (Enigma machine) for motivation. |

---

## MONTH 2 — Symmetric Key Cryptography + Hash Functions
*(Syllabus Units 2 & 4)*

### Week 5: Symmetric Crypto Overview + Modes of Operation
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Overview of Symmetric Key Cryptography — one key, both sides. Real use cases (disk encryption, VPN). | Diagram symmetric encryption flow. |
| 2 | Stream ciphers vs Block ciphers (deeper this time — keystream generation, padding needs). | Implement simple XOR stream cipher with a pseudo-random keystream. |
| 3 | Block cipher modes: **ECB** (why it's insecure — the famous "ECB penguin" image problem). | Encrypt an image using ECB mode with AES and *see* the pattern leak (great "aha" moment). |
| 4 | **CBC** mode — IV (Initialization Vector), chaining. | Implement AES-CBC using `pycryptodome`. |
| 5 | **CFB** and **OFB** modes — turning block cipher into stream cipher. | Compare CFB vs OFB vs CBC in a short report (2-3 lines each). |
| 6 | Revision: when to use which mode (this is a common interview/exam question). | Practice Q: "Why is ECB bad? What problem does IV solve?" |
| 7 | Rest | Read: Wikipedia "Block cipher mode of operation" (has great diagrams). |

### Week 6: DES — Understand a Real Cipher's Internals
| Day | Topic | Hands-on |
|---|---|---|
| 1 | DES overview: 56-bit key, 64-bit block, why it's now considered weak. | Diagram DES's Feistel structure. |
| 2 | Feistel structure explained (why encryption/decryption use the same function). | Trace one round of Feistel by hand on paper with small numbers. |
| 3 | DES Round Function: expansion, S-boxes, permutation. | Implement a *simplified* DES-like Feistel round in Python (full DES is complex; a mini version teaches the same idea). |
| 4 | DES Analysis and Attacks: brute force (56-bit is now crackable), differential/linear cryptanalysis (concept only, no need to master the math yet). | Calculate: how long would brute-forcing DES take with 1 billion keys/sec? |
| 5 | Block Cipher Design Principles (Feistel design criteria, avalanche effect, key schedule importance). | Write short notes: "5 things a good block cipher needs." |
| 6 | Revision Day | Quiz on Feistel + DES weaknesses. |
| 7 | Rest | Watch Christof Paar's DES lecture (link below). |

### Week 7: AES — The Modern Standard
| Day | Topic | Hands-on |
|---|---|---|
| 1 | AES Introduction: why it replaced DES, key sizes (128/192/256). | Compare DES vs AES table. |
| 2 | AES Transformations: SubBytes, ShiftRows, MixColumns, AddRoundKey — explained one at a time with simple visuals. | For each transformation, describe in one sentence what it does to the data. |
| 3 | AES Key Expansion (how one key becomes many round keys). | Trace key expansion for a small example, or read pycryptodome source comments. |
| 4 | AES Security: known attacks, why AES-128 is still considered secure. | Encrypt/decrypt a file using AES-256-CBC with `pycryptodome`. |
| 5 | Practical: Password-based key derivation (PBKDF2) — how a password becomes an AES key safely. | Implement "encrypt a file with a password" tool using PBKDF2 + AES. |
| 6 | Revision Day | Practice Q: "Why can't we use a plain password directly as an AES key?" |
| 7 | Rest | Read: "AES: How it Works" article (link below). |

### Week 8: Hash Functions + Mini Project
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Cryptographic Hash Function criteria: pre-image resistance, second pre-image resistance, collision resistance. | Hash the same file twice, confirm identical hash; change 1 byte, see hash change completely. |
| 2 | Random Oracle Model (concept only — hash acts like an unpredictable black box). | Write it in your own words — no code needed. |
| 3 | Applications of hashing: Message Authentication (HMAC), Digital Signatures (preview), password storage (with salt), PRNGs. | Implement HMAC using `hashlib`/`hmac` module. |
| 4 | Security requirements + Brute-Force attacks + basic cryptanalysis of hashes (birthday attack concept). | Calculate: birthday paradox — why 128-bit hash isn't "128-bit secure" against collisions (it's ~64-bit). |
| 5 | MD5, SHA family, SHA-512 message preparation steps (padding, length field). | Implement MD5 vs SHA-256 comparison; show why MD5 is broken (find a known MD5 collision example online — don't need to build one yourself). |
| 6–7 | **Mini Project 2: "Secure File Vault"** — encrypt files with AES-256 (password-based), and verify integrity using SHA-256 hash + HMAC. |

---

## MONTH 3 — Asymmetric Crypto, Authentication & Key Management
*(Syllabus Units 3, 5, 6 — the most "real-world" part)*

### Week 9: Asymmetric Key Crypto + RSA Foundations
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Asymmetric crypto overview: public/private key pairs, why it solves key-distribution problem of symmetric crypto. | Diagram: how Alice sends Bob a secret without ever sharing a secret key in advance. |
| 2 | Number theory for RSA: prime numbers, Euler's Totient function φ(n). | Write function to check primality; compute φ(n) for small n. |
| 3 | RSA Key Generation step by step (pick p, q → n → φ(n) → e → d). | Generate a *tiny* RSA keypair by hand (e.g., p=61, q=53 — the classic textbook example) then in Python. |
| 4 | RSA Encryption/Decryption operations. | Implement RSA encryption/decryption from scratch (no library) on small numbers to *see* the math. |
| 5 | Trapdoor One-Way Function concept — why RSA is easy one way, hard to reverse without the private key. | Explain in your own words why factoring `n` is the hard problem. |
| 6 | Revision Day | Redo hand-calculation of RSA keypair without notes. |
| 7 | Rest | Watch: Christof Paar's RSA lecture. |

### Week 10: RSA Deep Dive + ElGamal
| Day | Topic | Hands-on |
|---|---|---|
| 1 | RSA Performance: time complexity, Speeding Up RSA (fast exponentiation — square-and-multiply). | Implement fast modular exponentiation `pow(base, exp, mod)` from scratch, compare speed vs naive loop. |
| 2 | Security of RSA: known attacks (small e attack, common modulus attack — just concept), key size recommendations (2048-bit today). | Write a short note: "Why is 512-bit RSA broken today but 2048-bit still safe?" |
| 3 | RSA vs other algorithms — advantages/disadvantages, encrypting header vs full message body (why RSA is used for small data, hybrid encryption for large data). | Build a **hybrid encryption demo**: generate AES key → encrypt data with AES → encrypt AES key with RSA. (This is exactly how real TLS/PGP work!) |
| 4 | ElGamal Cryptography — overview, based on Diffie-Hellman idea (discrete log problem). | Read about discrete log problem — write it in your own words. |
| 5 | ElGamal Key Generation, Encryption, Decryption. | Implement ElGamal from scratch on small numbers. |
| 6 | Revision Day | Compare RSA vs ElGamal in a table. |
| 7 | Rest | Read a short article comparing RSA and ElGamal (link below). |

### Week 11: Authentication + Key Exchange + Key Management
| Day | Topic | Hands-on |
|---|---|---|
| 1 | One-way Authentication: password-based, certificate-based, two-factor/LDAP (concept). | Build a simple password-hash + salt login system in Python (SQLite + `hashlib`). |
| 2 | Mutual Authentication: shared-secret based, asymmetric-key based, timestamps to prevent replay attacks. | Draw a sequence diagram of a mutual authentication handshake. |
| 3 | Dictionary Attacks: how they work, and defenses (salting, rate-limiting, Argon2/bcrypt). | Try cracking a weak password hash using a small dictionary list (educational, on your own test data only). |
| 4 | Diffie-Hellman Key Exchange — the elegant idea of agreeing on a secret over a public channel. | Implement Diffie-Hellman key exchange between "Alice" and "Bob" scripts. |
| 5 | Man-in-the-Middle attack on Diffie-Hellman (why authentication must accompany key exchange). | Simulate a MITM attacker script intercepting the DH exchange (educational demo only). |
| 6 | Key Management Fundamentals: key lengths, lifetimes, key generation best practices, Key Distribution (symmetric vs public-key distribution methods). | Notes: "What happens if a key is never rotated?" |
| 7 | Revision Day | Full quiz covering Week 9–11. |

### Week 12: Digital Certificates + Capstone Project
| Day | Topic | Hands-on |
|---|---|---|
| 1 | Digital Certificates: what they are, why we need a trusted third party (CA), Certificate types. | Look at a real website's TLS certificate (browser padlock → certificate details). |
| 2 | X.509 Certificate Format — fields explained simply (issuer, subject, public key, validity, signature). | Use OpenSSL to generate a self-signed certificate: `openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365`. |
| 3 | Certificate Authority (CA) and Certificate Servers — how the chain of trust works. | Inspect your generated certificate's fields using `openssl x509 -in cert.pem -text -noout`. |
| 4 | Creating Digital Certificates programmatically (Java/Python). | Generate an X.509 certificate in Python using the `cryptography` library. |
| 5–7 | **Capstone Project (see below) — build & document one full project.** | |

---

## Capstone / Portfolio Project Ideas (Pick 1–2 to build deeply)

1. **Secure Chat App** — two users exchange messages using Diffie-Hellman for key agreement + AES for message encryption + HMAC for integrity. (Combines Weeks 5, 11.)
2. **Mini PGP Tool** — hybrid encryption: RSA + AES, sign messages with RSA, verify signatures. Include a simple "keyring" (store public keys). (Combines Weeks 7, 9, 10.)
3. **Password Manager (CLI)** — master-password derived key (PBKDF2) encrypts a vault of saved passwords with AES-256. (Combines Weeks 7, 11.)
4. **Certificate Authority Simulator** — a mini CA that issues, signs, and verifies X.509-style certificates for "users" in a simulated network. (Combines Week 12.)
5. **Cryptanalysis Toolkit** — automatic Caesar/Vigenère breaker + hash-collision demonstrator + "why ECB leaks patterns" visualizer. (Great for showing deep understanding, combines Month 1 + hash topics.)
6. **Secure File Sharing Tool** — encrypt files locally, upload to cloud storage, and only the recipient with the right private key can decrypt (real hybrid crypto use case).

**Tip:** Document each project on GitHub with a README explaining *why* you chose each algorithm — this is what makes a project impressive, not just working code.

---

## Best Resources (Curated)

**Video Courses:**
- Christof Paar — "Introduction to Cryptography" (YouTube channel, university-level but explained very clearly, includes DES/AES/RSA math walkthroughs).
- NPTEL Cryptography and Network Security courses (from your syllabus) — good for exam-style depth.

**Books (from your syllabus, prioritized for self-study):**
- *Cryptography and Network Security* — William Stallings (best all-rounder, matches your syllabus almost topic-for-topic).
- *Practical Cryptography in Python* — Seth James Nielson (best for hands-on coding, less theory-heavy).
- *Everyday Cryptography* — Keith M. Martin (great for building intuition in plain English).

**Interactive/Web Tools:**
- CyberChef (gchq.github.io/CyberChef) — drag-and-drop to see encoding/encryption happen live.
- cryptopals.com — "Cryptopals Challenges": the gold standard of hands-on crypto exercises, ordered from easy to hard. Highly recommended once you finish Month 1.

**Python Docs:**
- `pycryptodome` documentation (pycryptodome.readthedocs.io) — has ready examples for every cipher mode.
- `cryptography` library docs (cryptography.io) — for certificates and production-safe code.

---

## Weekly Self-Check Questions (use every Sunday/revision day)

1. Can I explain this week's main concept to a friend with no crypto background, in 2–3 sentences?
2. Can I write the core algorithm from memory (even roughly), without copying code?
3. What real-world system uses this concept (e.g., "AES → WhatsApp encryption", "RSA → HTTPS")?
4. What would happen if this technique were attacked or misused?

If you can answer all four confidently — you're not just covering syllabus, you're building real understanding. That's the actual goal.

---

### Final Note
Cryptography is a subject where **slow, hands-on understanding beats fast memorization**. If a week takes you 10 days instead of 7, that's fine — the plan is a guide, not a race. By the end of Month 3, you won't just know the syllabus — you'll be able to build, break, and explain real cryptographic systems, which is exactly what "confident practical knowledge" means.
