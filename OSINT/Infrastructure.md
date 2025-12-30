# 🏢 Infrastructure & Network OSINT

## 1. Domain & DNS Enumeration
* **Whois:** `whois domain.com` (Check registration and nameservers)
* **Dig (DNS Lookup):** * `dig any domain.com` (Check all records)
    * `dig axfr @nameserver domain.com` (Attempt a Zone Transfer)
* **Subdomain Discovery:**
    * **Subfinder:** `subfinder -d domain.com -o subdomains.txt`
    * **Amass:** `amass enum -d domain.com`
    * **CRT.sh:** Search Certificate Transparency logs for subdomains.

## 2. IP & Port Discovery (Passive)
* **Shodan:**
    * `hostname:"target.com"`
    * `net:"1.2.3.4/24"`
    * `org:"Company Name"`
* **Censys:** Excellent for finding SSL certificate details and associated IPs.

## 3. Cloud OSINT
* **CloudBrute:** Find a company's infrastructure on AWS, Azure, Google Cloud.
* **S3 Buckets:** Use `grayhatwarfare.com` to search for exposed public buckets.
* **TruffleHog:** Search GitHub/GitLab for leaked API keys and secrets.

## 4. Visual History
* **Wayback Machine (Archive.org):** Find old versions of websites to see removed contact info or dev comments.
