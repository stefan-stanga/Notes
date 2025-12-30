# 🌀 Penetration Testing Workflow

This workflow outlines the standard methodology for a web-centric penetration test, moving from passive discovery to full system exploitation.

---

## Phase 1: Reconnaissance (The "No-Touch" Phase)
*Goal: Understand the target's footprint without triggering alerts.*

1.  **Passive OSINT:** * Check `OSINT/Corporate.md` for employee emails and tech stacks.
    * Use Shodan/Censys to find historical IP addresses.
2.  **DNS & Subdomains:** * Run `subfinder` or `amass` to find hidden dev/staging environments.
3.  **Visual Inspection:** * Browse the site. Look at `robots.txt`, `.git` (if exposed), and the page source for comments/API keys.

---

## Phase 2: Scanning & Enumeration (The "Discovery" Phase)
*Goal: Identify the services and entry points.*

1.  **Port Scanning:** * Use `Scanning/Nmap-Cheatsheet.md` to find open ports (80, 443, 8080, etc.).
2.  **Service Identification:** * Cross-reference open ports with `Scanning/Service-Specific.md`.
3.  **Directory Brute Forcing:** * Run `gobuster` or `ffuf` to find hidden directories like `/admin`, `/config`, or `/backup`.
4.  **Automated Vulnerability Scan:** * Fire off `nuclei` or `nikto` from `Scanning/Vulnerability-Scanners.md` to catch low-hanging fruit.

---

## Phase 3: Vulnerability Analysis & Exploitation
*Goal: Weaponize the information gathered.*

1.  **Analyze the Tech Stack:** * Is it WordPress? Use `WPScan`. Is it a custom API? Open Burp Suite.
2.  **Testing for Injection:** * Check for SQLi, XSS, and Command Injection using the payloads in `Web-Exploits/`.
3.  **Authentication Testing:** * Check for default credentials or IDOR vulnerabilities in the `/user` profile sections.
4.  **File Uploads:** * If the site allows uploads, try to upload a web shell (PHP/ASPX) to get a "foot in the door."
