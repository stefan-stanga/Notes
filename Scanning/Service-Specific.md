# 🛠️ Service-Specific Enumeration

## 📂 Port 21: FTP
*Look for anonymous access and file uploads.*
* **Anonymous Login:** `ftp $IP` (User: `anonymous` | Pass: `anonymous`)
* **Nmap Scripts:** `nmap --script ftp-anon,ftp-bounce,ftp-syst -p 21 $IP`
* **Download All Files:** `wget -r ftp://anonymous:anonymous@$IP`

---

## 📂 Port 22: SSH
*Check for weak versions or try credentials.*
* **Banner Grab:** `nc -vn $IP 22`
* **Brute Force:** `hydra -l root -P /usr/share/wordlists/rockyou.txt $IP ssh`
* **Audit:** `ssh-audit $IP`

---

## 📂 Port 80/443: HTTP/HTTPS
*Web discovery and vulnerability hunting.*
* **Directory Brute Force:** `gobuster dir -u http://$IP -w /usr/share/wordlists/dirb/common.txt`
* **Vulnerability Scan:** `nuclei -u http://$IP`
* **Subdomain Search:** `ffuf -w wordlist.txt -u http://FUZZ.target.com`

---

## 📂 Port 139/445: SMB
*Common on Windows; look for open shares and user info.*
* **List Shares:** `smbclient -L //$IP/` (Press Enter for no password)
* **Check Vulnerabilities:** `nmap --script smb-vuln* -p 445 $IP`
* **Enum Everything:** `enum4linux -a $IP`
* **Connect to Share:** `smbclient //$IP/SHARENAME`

---

## 📂 Port 161: SNMP
*Often leaks system info and running processes.*
* **Brute Force Community String:** `onesixtyone $IP`
* **Full Walk:** `snmpwalk -v2c -c public $IP`
* **Check Users/Processes:** `snmp-check $IP`

---

## 📂 Port 3306: MySQL
*Check for remote access or default root creds.*
* **Remote Connect:** `mysql -h $IP -u root`
* **Nmap Scripts:** `nmap --script mysql-info,mysql-empty-password,mysql-users -p 3306 $IP`

---

## 📂 Port 3389: RDP
*Windows Remote Desktop.*
* **Check for BlueKeep:** `nmap -p 3389 --script rdp-vuln-ms12-020 $IP`
* **Brute Force:** `crowbar -b rdp -s $IP/32 -u admin -C password_list.txt`

---

## 📂 Port 5985/5986: WinRM
*Windows Remote Management (often how you get a shell).*
* **Execution:** `evil-winrm -i $IP -u user -p password`

---

## 📂 Port 111: RPCBind
*Look for NFS (Network File System) shares.*
* **Show Mounts:** `showmount -e $IP`
* **Mount a Share:** `mount -t nfs $IP:/share /mnt/local_dir -nolock`
