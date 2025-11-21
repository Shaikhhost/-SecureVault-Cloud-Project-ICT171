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
- Local terminal (macOS Terminal / Windows PowerShell)  
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
 My Azure portal showing VM running + my public IP 20.193.145.172  
<img width="1577" height="669" alt="image" src="https://github.com/user-attachments/assets/996bea8d-4922-4f72-bbf0-b9593a148d59" />
  inbound rules showing the following ports 22, 80, 443 open  

SSH Connection Established:  
<img width="1141" height="533" alt="image" src="https://github.com/user-attachments/assets/46edfc2b-5387-4d28-87b2-3269beba45db" />
 This Terminal shows successful login `securevault@20.193.145.172`

### Phase 2 – Connect to VM and Update System:
Connected via SSH  
```bash
ssh securevault@20.193.145.172
