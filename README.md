# SecureVault – Encrypted Cloud File Storage Prototype
**ICT171 Assignment 3 – 2025**  
**Student Name:** Shaikh Mohammad Elahi  
**Student Number:** 35800944

**VM Name:** SecureVault  
**Username:** securevault  
**Public IP:** 20.193.145.172  
**Domain:** https://securevault.online  
**Contact Email (for SSL):** [your email or 35800944@student.murdoch.edu.au]

**Video Explainer:** [Paste your YouTube or Google Drive link here after recording]  
**Total Cost of Ownership IaaS vs SaaS:** https://murdochuniversity-my.sharepoint.com/:p:/g/personal/35800944_student_murdoch_edu_au/ETMSNmlXJQhBmWpCHvem4bIBdh1WvSPf1XcagYAfBr4nIg

### Project Overview:
This project demonstrates the deployment of a privacy-first encrypted cloud file storage prototype using **Microsoft Azure IaaS**, Ubuntu 24.04 LTS, Apache2 web server, custom HTML/CSS/JavaScript, a custom domain purchased from Namecheap, and Let’s Encrypt HTTPS — all configured **100% via SSH only**.

### Website Contents:
The website includes:

- `index.html` (Home page with drag-and-drop upload area)  
- `uploaded.html` (Success page with live client-side AES-256 encryption/decryption demo using CryptoJS)  
- Fully responsive dark-themed design  
- All files served from `/var/www/html/`

**Purpose:** To prove secure file handling concepts on real IaaS while simulating end-to-end encrypted cloud storage in a working prototype.  
**Outcome:** Website fully accessible via custom domain with valid HTTPS and working encryption demonstration.

### Before Starting the project:
Ensure you have:

- Azure for Students account  
- Domain purchased from Namecheap (securevault.online)  
- Local terminal (macOS/Windows PowerShell)  
- Website files ready locally (`index.html`, `uploaded.html`)  

### Phase 1 – Azure VM Setup:
Steps  
Log into Azure portal  
Create a new Ubuntu VM:  
- VM Name: SecureVault  
- OS: Ubuntu 24.04 LTS  
- Size: Standard B1s (cost-efficient)  
- Region: Central India  
Configure Network Security Group (NSG) to allow:  
- SSH (port 22)  
- HTTP (port 80)  
- HTTPS (port 443)  

**[Insert screenshot: azure-vm-overview.png]** ← Azure portal showing VM running + public IP 20.193.145.172  
**[Insert screenshot: nsg-rules.png]** ← NSG showing ports 22, 80, 443 open  

SSH Connection Established:  
**[Insert screenshot: ssh-login.png]** ← Terminal showing successful login as securevault@20.193.145.172

### Phase 2 – Connect to VM and Update System:
Connect via SSH  
```bash
ssh securevault@20.193.145.172
Update System
Bashsudo apt update && sudo apt upgrade -y
[Insert screenshot: system-updated.png] ← Terminal showing updates completed
Install Apache:
Bashsudo apt install apache2 certbot python3-certbot-apache -y
sudo systemctl enable apache2
sudo systemctl start apache2
Verify Apache is Running
Bashsudo systemctl status apache2
[Insert screenshot: apache-running.png] ← Green "active (running)" status
Then test default page with public IP in browser → http://20.193.145.172
Now Upload Website Files to VM:
Transferred files using SCP (no WinSCP needed):
Bashscp index.html uploaded.html securevault@20.193.145.172:/tmp/
Move Files to Apache Root:
Bashsudo rm -rf /var/www/html/*
sudo mv /tmp/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html/
sudo chmod -R 755 /var/www/html/
sudo systemctl restart apache2
[Insert screenshot: files-transferred.png] ← ls -l /var/www/html/ showing index.html and uploaded.html
Test website in browser: http://20.193.145.172 – SecureVault site loads perfectly
[Insert screenshot: site-via-ip.png]
Phase 3 – Domain Setup (Namecheap):
Configure DNS Records
Log into Namecheap
Add A records for your domain:
textHost       Value            TTL
@          20.193.145.172   Automatic
www        20.193.145.172   Automatic
[Insert screenshot: namecheap-dns.png] ← Namecheap Advanced DNS showing both A records
Website Accessible via Domain:
[Insert screenshot: site-via-domain.png] ← https://securevault.online working
Phase 4 – Enable HTTPS with Certbot (Let’s Encrypt):
Install Certbot and Apache Plugin
Bashsudo apt install certbot python3-certbot-apache -y
Run Certbot
Bashsudo certbot --apache
Follow Certbot Prompts

Enter email
Agree to terms
Select securevault.online and www.securevault.online
Choose redirect HTTP → HTTPS (recommended)

Test HTTPS
Visit in browser: https://securevault.online → green padlock appears
[Insert screenshot: https-padlock.png] ← Browser showing valid Let’s Encrypt certificate
Verify Auto-Renewal
Bashsudo systemctl status certbot.timer
Final Verification & Testing:
Verify Apache
Bashsudo systemctl status apache2
Verify Files in Web Root
Bashls -l /var/www/html/
Browser Checks – all working perfectly:

http://20.193.145.172 → redirects to HTTPS
https://securevault.online
https://www.securevault.online
Upload button → success page → live AES-256 encryption demo works instantly

[Insert screenshot: home-page.png] ← Full SecureVault home page
[Insert screenshot: encryption-demo.png] ← uploaded.html with message encrypted and decrypted
[Insert screenshot: mobile-view.png] ← Optional: show responsive design on phone
