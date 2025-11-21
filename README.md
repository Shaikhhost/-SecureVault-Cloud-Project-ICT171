# SecureVault – Encrypted Cloud File Storage Prototype
**ICT171 Assignment 3 – 2025**  
**Shaikh Mohammad Elahi – 35800944**

**Live Website:** https://securevault.online  
**Public IP:** 20.193.145.172  
**Domain Provider:** Namecheap  
**SSL:** Let’s Encrypt (auto-renew)  
**VM:** Azure Ubuntu 24.04 (B1s) – Central India

**Video Explainer (8 minutes):** [Upload this now and paste link here]

### Project Overview
SecureVault is a fully functional prototype of a privacy-first encrypted cloud storage platform deployed 100% via SSH on Microsoft Azure IaaS.

- Custom domain + real SSL
- Apache2 web server
- Responsive HTML/CSS/JS site
- Upload → fake encryption success + redirect to uploaded.html
- Client-side AES-256 encryption demo (CryptoJS)
- No backend needed – pure static site with JavaScript simulation

### Setup Summary (all via SSH)
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 certbot python3-certbot-apache -y
sudo systemctl enable apache2 && sudo systemctl start apache2

# Upload files via SCP
sudo mv files /var/www/html/
sudo chown -R www-data:www-data /var/www/html/
sudo systemctl restart apache2

# Let’s Encrypt
sudo certbot --apache -d securevault.online -d www.securevault.online
