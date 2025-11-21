# SecureVault – Encrypted Cloud File Storage Prototype
**ICT171 Assignment 3 – 2025**  
**Student Name:** Shaikh Mohammad Elahi  
**Student Number:** 35800944

**VM Name:** SecureVault  
**Username:** securevault  
**Public IP:** 20.193.145.172  
**Domain:** https://securevault.online  
**Contact Email (for SSL):** 35800944@student.murdoch.edu.au

**Video Explainer (8–10 min):** [Paste your YouTube / Google Drive link here after upload]  
**Total Cost of Ownership IaaS vs SaaS:** https://murdochuniversity-my.sharepoint.com/:p:/g/personal/35800944_student_murdoch_edu_au/ETMSNmlXJQhBmWpCHvem4bIBdh1WvSPf1XcagYAfBr4nIg

### Project Overview:
This project demonstrates the deployment of a privacy-first encrypted cloud file storage prototype using **Microsoft Azure IaaS**, Ubuntu 24.04 LTS, Apache2 web server, custom HTML/CSS/JavaScript, a custom domain purchased from Namecheap, and Let’s Encrypt HTTPS — **100% configured via SSH only** (no GUI, no RDP, no WordPress).

### Website Contents:
The website includes:

- `index.html` (Home page with drag-and-drop upload area)  
- `uploaded.html` (Success page with live client-side AES-256 encryption/decryption demo using CryptoJS)  
- Fully responsive dark cyber-security theme  
- All files served from `/var/www/html/`

**Purpose:** To prove secure file handling and encryption concepts on real IaaS infrastructure while simulating end-to-end encrypted cloud storage.  
**Outcome:** Fully functional prototype accessible at https://securevault.online with valid HTTPS and working encryption demo.

### Before Starting the project:
Ensure you have:

- Azure for Students account  
- Domain purchased from Namecheap (securevault.online)  
- Local terminal ( Windows PowerShell)  
- Website files ready locally in one folder

<img width="1006" height="372" alt="image" src="https://github.com/user-attachments/assets/1f015ce5-2982-4253-b030-1f52f0868b5b" />
 Your local folder should be showing `index.html` and all other necessary files 

### Phase 1 – Azure VM Setup:
Steps  
Logged into Azure portal  
Created a new Ubuntu VM:  
- VM Name: SecureVault  
- OS: Ubuntu 24.04 LTS  
- Size: Standard B1s (cost-efficient)  
- Region: Central India (Zone 1)  
Configured Network Security Group (NSG) to allow:  
- SSH (port 22)  
- HTTP (port 80)  
- HTTPS (port 443)  
  Screenshot references:
<img width="1814" height="935" alt="image" src="https://github.com/user-attachments/assets/d6d719ba-4f0a-4232-8898-6975ef5a0fc4" />
 My Azure portal showing VM running and  my public IP 20.193.145.172

<img width="1577" height="669" alt="image" src="https://github.com/user-attachments/assets/996bea8d-4922-4f72-bbf0-b9593a148d59" />
  inbound rules showing the following ports 22, 80, 443 open  
  

SSH Connection Established:  
<img width="1141" height="533" alt="image" src="https://github.com/user-attachments/assets/46edfc2b-5387-4d28-87b2-3269beba45db" />
 This Terminal shows successful login `securevault@20.193.145.172`

### Phase 2 – Connect to VM and Update System:
Connected via SSH this can also be seen above 
ssh securevault@20.193.145.172 (login)

The  System needs to be updated after logging in:
sudo apt update
sudo apt upgrade -y
<img width="1235" height="903" alt="image" src="https://github.com/user-attachments/assets/c1bc8fb1-6eb2-4e69-af5b-d1c294c7e260" />

Installed Apache2 web server and Certbot for SSL  
  `sudo apt install apache2 certbot python3-certbot-apache -y`  
  `sudo systemctl enable apache2`  
  `sudo systemctl start apache2`

- Verified Apache is running correctly  
  `sudo systemctl status apache2`
<img width="952" height="350" alt="image" src="https://github.com/user-attachments/assets/ad6420a4-f118-4a5c-84be-19524baa2dba" />

- Tested default Apache page in browser:
-  http://20.193.145.172 → Apache welcome page appeared
-  <img width="733" height="554" alt="image" src="https://github.com/user-attachments/assets/b1200edc-30e2-4458-a72e-da4967de2852" />



### Phase 3 – Upload Website Files to VM:
- Opened WinSCP and connected to securevault@20.193.145.172  
- Navigated local folder: `SecureVault_html`  
- Dragged all files to remote `/tmp/` directory  

<img width="1079" height="689" alt="image" src="https://github.com/user-attachments/assets/2c62183a-132a-4ca6-a307-74cd6e5cef9f" />
 ← WinSCP showing files uploading 

- Transferred local website files using SCP  
  `scp SecureVaultWebsite/* securevault@20.193.145.172:/tmp/`

- Moved files to Apache web root and set correct permissions  
  `sudo rm -rf /var/www/html/*`  
  `sudo mv /tmp/* /var/www/html/`  
  `sudo chown -R www-data:www-data /var/www/html/`  
  `sudo chmod -R 755 /var/www/html/`  
  `sudo systemctl restart apache2`

- Confirmed files are in place  
  `ls -l /var/www/html/`  
<img width="806" height="291" alt="image" src="https://github.com/user-attachments/assets/cb2f69d6-80b5-4319-b02c-a82d58dad380" />


- Tested site via public IP  
  http://20.193.145.172 → SecureVault home page loaded perfectly  
 <img width="1832" height="844" alt="image" src="https://github.com/user-attachments/assets/abe987a6-31d5-4647-93e1-c961d0b241b3" />


	### Phase 4 – Domain Setup (Namecheap):
- Logged into Namecheap
- Changed nameservers at registrar to Cloudflare’s  
- Added two A records in Cloudflare dashboard:

| Type | Name              | Content         | Proxy Status | TTL  |
|------|-------------------|-----------------|--------------|------|
| A    | securevault.online| 20.193.145.172  | Proxied (Orange Cloud) | Auto |
| A    | www               | 20.193.145.172  | Proxied (Orange Cloud) | Auto |

  DNS records configured through cloudfare after buying the domain
<img width="1730" height="946" alt="image" src="https://github.com/user-attachments/assets/ae2c1cb7-f7a6-4d8b-ad78-41e4287e3a0f" />

 To verify I searched up, https://securevault.online which is working
<img width="1833" height="995" alt="image" src="https://github.com/user-attachments/assets/e7dca889-c47a-470b-a3e5-d3a93f1ecfda" />

### Phase 5 – Enable HTTPS with Let’s Encrypt:
- Ran Certbot  
  `sudo certbot --apache -d securevault.online -d www.securevault.online`
   Certbot completion 
<img width="1271" height="300" alt="image" src="https://github.com/user-attachments/assets/57f5baf2-1bc1-469d-909b-c4fb4e49101e" />


<img width="1008" height="643" alt="image" src="https://github.com/user-attachments/assets/2ae1e27a-a05d-4488-8b45-e55e078fa04f" />
 The lock in browser showing its secure 

### Final Verification & Testing:
All working perfectly:  
- http://20.193.145.172 → redirects to HTTPS  
- https://securevault.online
  <img width="1826" height="956" alt="image" src="https://github.com/user-attachments/assets/0cb28fab-f99d-46b2-a688-d01866d6c45b" />

- https://www.securevault.online
 <img width="1866" height="966" alt="image" src="https://github.com/user-attachments/assets/734b7bbd-ef53-4a64-93e7-84fee1206352" />

- After user selects files and uploads them it successfully takes them to a live AES-256 encryption demo that runs instantly
<img width="810" height="713" alt="image" src="https://github.com/user-attachments/assets/6fdf2299-6742-44dd-99d5-472b91e9250f" />

<img width="1681" height="993" alt="image" src="https://github.com/user-attachments/assets/475977fe-977c-462d-a777-aaaf247911f6" />
As you can see above the Message encrypted and decrypted

### Scripting Component:
`uploaded.html` uses **CryptoJS AES-256-CBC** with a 256-bit key and 128-bit IV.  
Encryption/decryption is **100% client-side** — no data ever touches the server.  
This demonstrates real cryptographic protection for future file storage.

**Project Completed and Live – November 2025**  
**Shaikh Mohammad Elahi – 35800944**  
**100% IaaS | Custom domain | Let’s Encrypt SSL | WinSCP + SSH deployment | Real AES-256 demo**






