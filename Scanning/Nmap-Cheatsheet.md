# 🛰️ Nmap Cheatsheet

## 1. Fast Initial Scans
*Quickly identify open ports to start manual enumeration.*

| Command | Description |
| :--- | :--- |
| `nmap -sS -T4 --top-ports 1000 $IP` | Stealth SYN scan of top 1000 ports (Fast). |
| `nmap -T4 -F $IP` | Fast scan (top 100 ports). |
| `nmap -p- --min-rate 5000 $IP` | Scan all 65,535 ports at high speed. |

---

## 2. Detailed Service Enumeration
*Run these once you know which ports are open.*

| Command | Description |
| :--- | :--- |
| `nmap -sC -sV -p 80,443 $IP` | Run default scripts and version detection on specific ports. |
| `nmap -A $IP` | Aggressive scan: OS detection, Versioning, Script scanning, and Traceroute. |
| `nmap -sU $IP` | UDP Scan (Slow but necessary for DNS, SNMP, DHCP). |

---

## 3. NSE (Nmap Scripting Engine)
*Automate vulnerability discovery.*

| Command | Description |
| :--- | :--- |
| `nmap --script vuln $IP` | Run all scripts in the "vuln" category. |
| `nmap --script http-enum -p 80 $IP` | Enumerate common web directories/files. |
| `nmap --script smb-os-discovery $IP` | Determine OS version via SMB. |
| `nmap --script-args=unsafe=1` | Include intrusive scripts that might crash services. |

---

## 4. Output Formats
*Crucial for logging and tool integration.*

| Command | Description |
| :--- | :--- |
| `-oN scan.txt` | Normal output (what you see on screen). |
| `-oX scan.xml` | XML output (used for importing into Zenmap or Metasploit). |
| `-oG scan.grep` | Greppable output (best for `grep`, `awk`, `cut`). |
| `-oA final_scan` | **Recommended:** Output in all three formats simultaneously. |

---

## 5. Firewall Evasion & Stealth
| Command | Description |
| :--- | :--- |
| `-f` | Fragment packets (harder for some firewalls to reassemble). |
| `--mtu 24` | Set custom Maximum Transmission Unit. |
| `-D RND:10` | Use 10 random decoys to hide your real IP. |
| `--source-port 53` | Send packets from port 53 (DNS), often allowed through firewalls. |

---

## 6. Pro-Tips
* **Resume a Scan:** `nmap --resume <output_file>` (Requires `-oN` or `-oG`).
* **Interactive Controls:**
    * `v`: Increase verbosity during scan.
    * `V`: Decrease verbosity.
    * `p`: Turn on/off packet tracing.
    * Any other key: Prints status line.

---

## 🛡️ Example Workflow
1. **Find open ports:** `nmap -p- --min-rate 5000 -oG ports.txt $IP`
2. **Deep dive into found ports:** `nmap -sC -sV -p <PORTS> -oA full_scan $IP`
