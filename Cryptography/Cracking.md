# 🔨 Hash Cracking (Hashcat & John)

## 1. Identify the Hash Type
* **HashID:** `hashid "hash_string"`
* **Name That Hash:** `nth -s "hash_string"`

## 2. Hashcat (GPU Power)
*Replace `<mode>` with the ID found in `hashcat --help`.*
* **MD5 (0):** `hashcat -m 0 hashes.txt /usr/share/wordlists/rockyou.txt`
* **NTLM (1000):** `hashcat -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt`
* **Linux SHA-512 (1800):** `hashcat -m 1800 shadow_hashes /usr/share/wordlists/rockyou.txt`
* **Rule-based Attack:** `hashcat -m 0 hashes.txt wordlist.txt -r /usr/share/hashcat/rules/best64.rule`

## 3. John the Ripper (CPU Versatility)
* **Auto-detect:** `john hashes.txt`
* **Show cracked:** `john --show hashes.txt`
* **Specific format:** `john --format=raw-md5 hashes.txt --wordlist=rockyou.txt`

## 4. SSH/Zip/PDF Cracking
1. Extract hash: `ssh2john id_rsa > hash.txt`
2. Crack: `john hash.txt`
*(Use `zip2john`, `rar2john`, or `pdf2john` for other files.)*
