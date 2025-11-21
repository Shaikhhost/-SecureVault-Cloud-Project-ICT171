# SecureVault – Encrypted Cloud File Storage Prototype  
**ICT171 Assignment 3 – 2025**  
**Student Name:** Shaikh Mohammad Elahi  
**Student Number:** 35800944  

**VM Name:** SecureVault  
**Username:** securevault (or whatever you used)  
**Public IP:** 20.193.145.172  
**Domain:** https://securevault.online  
**Contact Email (for SSL):** [your email or Murdoch email]  

**Video Explainer:** [Paste YouTube/Drive link here after recording]  
**Total Cost of Ownership IaaS vs SaaS:** https://murdochuniversity-my.sharepoint.com/:p:/g/personal/35800944_student_murdoch_edu_au/ETMSNmlXJQhBmWpCHvem4bIBdh1WvSPf1XcagYAfBr4nIg  

### Project Overview
This project demonstrates the deployment of a privacy-first encrypted cloud file storage prototype using **Microsoft Azure IaaS**, Ubuntu 24.04, Apache2 web server, custom HTML/CSS/JavaScript, a custom domain purchased from Namecheap, and Let’s Encrypt HTTPS — all configured **100% via SSH**.

### Website Contents
- `index.html` – Home page with upload box  
- `uploaded.html` – Success page with live client-side AES-256 encryption/decryption demo (CryptoJS)  
- Custom dark-themed responsive design  
- All assets in `/var/www/html/`

**Purpose:** To prove secure cloud file handling concepts using real IaaS while simulating encrypted storage in a working prototype.

**Outcome:** Fully functional site accessible at https://securevault.online with valid HTTPS.

### Before Starting the Project
- Azure for Students subscription  
- Domain purchased from Namecheap (securevault.online)  
- Local tools: Terminal (or PowerShell), browser  
- Website files ready locally  

### Phase 1 – Azure VM Setup
- Created Ubuntu 24.04 LTS VM (Standard B1s, Central India)  
- NSG rules opened:  
  - SSH (22)  
  - HTTP (80)  
  - HTTPS (443)  
<img width="1879" height="1020" alt="image" src="https://github.com/user-attachments/assets/1c88fbbe-4432-4ca5-96b8-0ddec468122e" />


### Phase 2 – Connect & Update System
```bash
ssh securevault@20.193.145.172
sudo apt update && sudo apt upgrade -y
