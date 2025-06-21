# VPS setup Guides
VPS_setup_guides


# 🚀 Multi-Site Docker Deployment Guide for Hostinger VPS

This guide explains how to install and run the `multi-site-docker-mariadb-template.zip` on your Hostinger VPS using Docker and Docker Compose.

---

## ✅ Prerequisites

- Linux VPS (Ubuntu/Debian)
- `sudo` or `root` access
- Domain names pointing to your VPS IP

---

## 🧭 Step-by-Step Installation

### **1. Connect to your VPS**
```bash
ssh root@your-vps-ip
```

---

### **2. Install Docker and Docker Compose**
```bash
apt update
apt install -y docker.io docker-compose unzip
systemctl enable docker
systemctl start docker
```

---

### **3. Upload the ZIP to your VPS**

#### Option A: From local computer
```bash
scp multi-site-docker-mariadb-template.zip root@your-vps-ip:/root/
```

#### Option B: Use Hostinger File Manager or SFTP

---

### **4. Extract the ZIP file**
```bash
cd /root
unzip multi-site-docker-mariadb-template.zip
cd multi-site
```

---

### **5. Update Domain Names**
Edit `docker-compose.yml` and replace:
- `site1.com`, `site2.com`
- `dbadmin.local` → `dbadmin.yourdomain.com`

---

### **6. Point DNS to VPS**
Set these A-records:
```
site1.com             → [VPS IP]
www.site1.com         → [VPS IP]
site2.com             → [VPS IP]
dbadmin.yourdomain.com → [VPS IP]
```

---

### **7. Start Docker Services**
```bash
docker-compose up -d
```

---

## 🌐 Access Your Sites

- [https://site1.com](https://site1.com)
- [https://site2.com](https://site2.com)
- [https://dbadmin.yourdomain.com](https://dbadmin.yourdomain.com) (phpMyAdmin)

---

## 🔐 Security Notes

| Task                          | Command / Note                                     |
|-------------------------------|----------------------------------------------------|
| Change DB credentials         | Use phpMyAdmin or mysql CLI inside container       |
| Enable UFW firewall           | `ufw allow` for 22, 80, 443                        |
| Create DB backups             | `docker exec mariadb mysqldump` or use volumes    |
| Enforce HTTPS only            | Automatically done with Let's Encrypt + NGINX     |

---

## 🧰 Docker Management Commands

```bash
docker-compose ps            # Status of services
docker-compose logs -f       # Real-time logs
docker-compose down          # Stop and remove all
docker-compose restart       # Restart all services
```

---

## 📜 Automated Install Script

Run this after uploading both files:
```bash
chmod +x install-multisite-docker-vps.sh
./install-multisite-docker-vps.sh
```

This script will:
- Install Docker
- Unzip the project
- Start your services

---

## 📎 Files

- `multi-site-docker-mariadb-template.zip` → Docker + Site Template
- `install-multisite-docker-vps.sh` → Full installer

---

> Let me know if you'd like to add **WordPress**, **Next.js frontend**, or **CI/CD** pipelines next!
