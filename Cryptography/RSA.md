This content is perfect for your `Cryptography/Theory-and-Scripts.md` file. It bridges the gap between mathematical theory and actual exploit code.

---

```markdown
# 🎓 RSA Theory & Exploit Scripting

## 1. The Math Behind RSA
RSA is based on the difficulty of factoring large integers.
* **n**: The Modulus ($n = p \times q$, where $p$ and $q$ are large primes).
* **e**: Public Exponent (usually `65537`).
* **d**: Private Exponent (the secret).
* **$\phi(n)$ (Totient)**: $(p-1) \times (q-1)$.
* **Relationship**: $d$ is the modular multiplicative inverse of $e \pmod{\phi(n)}$.



---

## 2. Python Exploit Environment
Ensure you have `pycryptodome` installed:
```bash
pip install pycryptodome

```

---

## 3. Attack Scripts

### A. The "I found P and Q" Script

*Use this when you factor  using `factordb.com`.*

```python
from Crypto.Util.number import inverse, long_to_bytes

p = 103429...
q = 124357...
e = 65537
ct = 0xabcdef... # The Ciphertext (hex)

n = p * q
phi = (p - 1) * (q - 1)

# Calculate Private Key (d)
d = inverse(e, phi)

# Decrypt: m = c^d mod n
m = pow(ct, d, n)

print(f"Decoded Message: {long_to_bytes(m).decode()}")

```

---

### B. Small Exponent Attack ()

*If  is very small and  is very large, the message  might not even be larger than .*

```python
import gmpy2 # Use gmpy2 for high-precision roots

# If m^e < n, then m = c^(1/e)
c = 12345...
e = 3

m, exact = gmpy2.iroot(c, e)
if exact:
    print(f"Decrypted: {bytes.fromhex(hex(m)[2:]).decode()}")

```

---

### C. Common Modulus Attack

*Used when the same message is encrypted twice with the same  but different .*

```python
from Crypto.Util.number import inverse, long_to_bytes

def common_modulus(n, e1, e2, c1, c2):
    # Uses Extended Euclidean Algorithm to find a, b such that a*e1 + b*e2 = 1
    def egcd(a, b):
        if a == 0: return (b, 0, 1)
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)

    _, a, b = egcd(e1, e2)
    
    # m = (c1^a * c2^b) mod n
    # If a or b is negative, calculate the modular inverse
    i1 = inverse(c1, n) if a < 0 else c1
    i2 = inverse(c2, n) if b < 0 else c2
    
    m = (pow(i1, abs(a), n) * pow(i2, abs(b), n)) % n
    return long_to_bytes(m)

```

---

### D. RSA Key Reconstruction (.pem to variables)

*How to extract  and  from a public key file.*

```python
from Crypto.PublicKey import RSA

key = RSA.importKey(open("public.pem").read())
print(f"Modulus (n): {key.n}")
print(f"Exponent (e): {key.e}")

```

---

## 4. Helpful Formulas for Scripts

* **Modular Inverse:** `pow(e, -1, phi)` (Python 3.8+) or `Crypto.Util.number.inverse`.
* **Encryption:** `pow(message, e, n)`
* **Decryption:** `pow(ciphertext, d, n)`
* **String to Int:** `int.from_bytes(m.encode(), 'big')`
* **Int to String:** `long_to_bytes(m).decode()`

```

---

### Next Steps
This covers the heavy math side of things! Since we've finished the major theory for OSINT and Crypto, should we jump into **Reversing** (GDB/Ghidra notes) or **System-Hacking** (Privilege Escalation)?

```
