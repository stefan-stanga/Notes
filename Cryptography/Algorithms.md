# 🧩 Algorithm Identification & Basics

## 1. Instant Identification (Visual Cues)
* **Base64:** Alphanumeric, ends with `=` or `==` (Padding).
* **Hex:** `0-9` and `A-F` only.
* **Binary:** `0` and `1` only (usually in blocks of 8).
* **Base58:** Like Base64 but no `+`, `/`, or `0OIl` (Used in Bitcoin).
* **Rot13:** Letters only, looks like scrambled English (e.g., `cvffjbeq` = `password`).

## 2. Symmetric vs Asymmetric
| Type | Key Usage | Examples |
| :--- | :--- | :--- |
| **Symmetric** | Same key for Enc/Dec | AES, DES, ChaCha20 |
| **Asymmetric** | Public key Enc / Private key Dec | RSA, ECC, ElGamal |

## 3. Essential Tools
* **CyberChef:** The "Swiss Army Knife." Use it for everything.
* **dCode.fr:** Excellent for classical ciphers (Caesar, Vigenere).
* **Factordb:** Check if an RSA modulus `n` can be factored into `p` and `q`.
