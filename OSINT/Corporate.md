# 🏬 Corporate & Business OSINT

## 1. Google Dorking (The "Golden" Queries)
* **Find sensitive files:** `site:target.com filetype:pdf OR filetype:doc OR filetype:xlsx`
* **Find config files:** `site:target.com extension:conf OR extension:env OR extension:ini`
* **Exposed Logins:** `site:target.com inurl:login OR inurl:admin`
* **Directory Listing:** `site:target.com "index of /"`

## 2. Tech Stack Discovery
* **BuiltWith:** [builtwith.com](https://builtwith.com/) (See what CMS, Frameworks, and Analytics a site uses).
* **Wappalyzer:** Browser extension for instant tech stack identification.

## 3. Organizational Charting
* **LinkedIn:** "People" tab on a company page to map out C-suite and IT staff.
* **Glassdoor:** Read reviews to find internal frustrations or clues about internal software versions.
* **OpenCorporates:** Search for legal filings, directors, and business addresses.

## 4. Metadata Extraction
* **FOCA:** Download documents from a site and extract metadata (Users, Folders, Software versions).
* **Exiftool:** `exiftool image.jpg` (Check for GPS coordinates or camera serial numbers in corporate photos).
