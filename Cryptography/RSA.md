# RSA Theory and Exploit Scripting

## 1. RSA Theory (The Essentials)
RSA is an asymmetric encryption algorithm. It uses a public key for encryption and a private key for decryption.

* **n (Modulus)**: The product of two large prime numbers, p and q. (n = p * q)
* **e (Public Exponent)**: Usually set to 65537. Used to encrypt.
* **d (Private Exponent)**: The secret key used to decrypt.
* **phi_n (Totient)**: A value calculated as (p - 1) * (q - 1).
* **d Calculation**: d is the modular inverse of e modulo phi_n.



---

## 2. Environment Setup
You will need the pycryptodome library for most Python-based crypto challenges.

pip install pycryptodome

## 3. Exploit Scripts

### A. Basic Decryption (When P and Q are known)

If you find the prime factors p and q (using sites like factordb.com), you can recreate the private key.

```python
from Crypto.Util.number import inverse, long_to_bytes

# Inputs
p = 103429
q = 124357
e = 65537
ciphertext = 0xabcdef # Insert hex ciphertext here

# Calculations
n = p * q
phi_n = (p - 1) * (q - 1)
d = inverse(e, phi_n)

# Decryption: m = (c ^ d) % n
m = pow(ciphertext, d, n)

print("Decoded Message:", long_to_bytes(m).decode())

```

### B. Small Exponent Attack (e=3)

If the public exponent e is very small (like 3) and the message is relatively short, you can often find the message by taking the mathematical cube root.

```python
import gmpy2

c = 123456789 # Ciphertext as an integer
e = 3

# Take the e-th root of c
m, exact = gmpy2.iroot(c, e)

if exact:
    # Convert integer back to bytes/string
    print("Decrypted:", bytes.fromhex(hex(m)[2:]).decode())
else:
    print("Root is not exact. Try another method.")

```

### C. Common Modulus Attack

If the same message (m) was encrypted twice using the same modulus (n) but two different exponents (e1, e2).

```python
from Crypto.Util.number import inverse, long_to_bytes

def common_modulus(n, e1, e2, c1, c2):
    def egcd(a, b):
        if a == 0: return (b, 0, 1)
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)

    g, a, b = egcd(e1, e2)
    
    if a < 0:
        c1 = inverse(c1, n)
        a = -a
    if b < 0:
        c2 = inverse(c2, n)
        b = -b
        
    m = (pow(c1, a, n) * pow(c2, b, n)) % n
    return long_to_bytes(m)

```

---

## 4. Key Manipulation

Extracting n and e from a public key file (.pem).

```python
from Crypto.PublicKey import RSA

with open("public.pem", "r") as f:
    key = RSA.importKey(f.read())
    print("Modulus (n):", key.n)
    print("Exponent (e):", key.e)

```

---

## 5. Cheat Sheet Functions

* **Encryption**: pow(m, e, n)
* **Decryption**: pow(c, d, n)
* **Modular Inverse**: pow(e, -1, phi_n)
* **Text to Int**: int.from_bytes(b"hello", "big")
* **Int to Text**: long_to_bytes(12345).decode()

```

---

Would you like me to populate the **Reversing** directory next with `Static-Analysis.md` (Ghidra/Strings) and `Dynamic-Analysis.md` (GDB)?

```
