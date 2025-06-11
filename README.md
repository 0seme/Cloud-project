# Cloud-project  

AltSchool Cloud Engineering 2nd Semester Project

# CareLink – The Future of Family Health

**CareLink** is an innovative health management platform that empowers families to coordinate care from anywhere. By combining real-time updates, secure communication, and centralized tools for appointments, prescriptions, and emergency alerts, CareLink transforms how families stay connected to their health needs.

---

## Table of Contents

- [Screenshot of Page](#screenshot-of-page)
- [Features](#features)
- [Live Project URL](#live-project-url)
- [Server Setup](#server-setup)
- [Web Server Setup](#web-server-setup)
- [Deployment](#deployment)
- [HTTPS Setup (Let's Encrypt + DuckDNS)](#https-setup-lets-encrypt--duckdns)
- [Technologies Used](#technologies-used)
- [Conclusion](#conclusion)

---

## Screenshot of Page

![CareLink Landing Page](https://raw.githubusercontent.com/0seme/Cloud-project/main/joyce-landing-page.png)

---

## Features

- **Unified Dashboard**: Track doctor appointments, prescriptions, and health notes across all family members.  
- **Smart Alerts**: Receive reminders for medication, vaccinations, and upcoming checkups.  
- **Secure Data**: All data is encrypted and protected by industry-grade protocols.

---

## Live Project URL

**Hosted at:** [https://cloudbyjoyce.duckdns.org](https://cloudbyjoyce.duckdns.org)

---

## Server Setup

I had already provisioned an EC2 instance from a previous setup. Below are the details and steps I took to prepare the server environment:

- **Instance Type**: t2.micro (Free Tier)  
- **Operating System**: Ubuntu 22.04 LTS  
- **Public IP Address**: `176.34.250.79`  
- **Elastic IP**: Enabled for persistent IP  

### Steps Taken

**Access the Server via SSH**

**Command Run:**
```bash
ssh -i <key-name>.pem ubuntu@176.34.250.79
```

**Opened Required Ports via AWS Security Group:**
- TCP Port 22 (SSH)
- TCP Port 80 (HTTP)
- TCP Port 443 (HTTPS)

## Web Server Setup

Initially, Apache2 was running on the server from a previous configuration. Since I planned to use Nginx, I had to stop and disable Apache first.

### Stop and Disable Apache2

**Commands Run:**
```bash
sudo systemctl stop apache2
sudo systemctl disable apache2
```

### Install Nginx

**Commands Run:**
```bash
sudo apt update
sudo apt install nginx -y
```

### Start and Enable Nginx

**Commands Run:**
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Verify Nginx Installation

Open in browser:
```
http://176.34.250.79
```

## Deployment

I wrote the HTML for the landing page (index.html) based on the CareLink project and deployed it to the server.

### Steps Taken

**Navigate to the Web Root Directory**

**Command Run:**
```bash
cd /var/www/html
```

**Replace Default index.html**

**Command Run:**
```bash
sudo nano index.html
```

I pasted the HTML code for the CareLink landing page and saved the file.

**Verify Deployment**

Refreshed the browser to confirm that the custom CareLink landing page was live at:
```
http://176.34.250.79
```

## HTTPS Setup (Let's Encrypt + DuckDNS)

Since I did not own a custom domain, I used DuckDNS, a free dynamic DNS service, to secure the site with HTTPS.

### Steps Taken

1. Registered a free subdomain at https://www.duckdns.org
   - **Subdomain chosen:** cloudbyjoyce
   - **Full domain:** cloudbyjoyce.duckdns.org
   - Linked it to my EC2 instance's public IP

### Install Certbot and Nginx Plugin

**Command Run:**
```bash
sudo apt install certbot python3-certbot-nginx -y
```

### Request SSL Certificate

**Command Run:**
```bash
sudo certbot --nginx -d cloudbyjoyce.duckdns.org
```

Followed the interactive prompts, accepted the terms, and the SSL certificate was issued and automatically configured.

### Verify HTTPS

Visit in browser:
```
https://cloudbyjoyce.duckdns.org
```

Certbot also scheduled automatic SSL renewal using a system timer.

## Technologies Used

- **AWS EC2** – Cloud compute instance
- **Ubuntu 22.04** – Server operating system
- **Nginx** – Web server
- **DuckDNS** – Free dynamic DNS provider
- **Let's Encrypt + Certbot** – For SSL certificates
- **HTML5** – For landing page content

## Conclusion

This project demonstrates my ability to provision cloud resources, set up web servers, deploy applications, and secure web traffic using SSL, all of which i did with free-tier tools. Thank you to AltSchool for the hands-on learning opportunity and exposure to real-world DevOps practices.