# Altschool Project

## Project Overview
This project involves provisioning a Linux server on AWS, installing a web server (Nginx), and deploying a simple HTML landing page to demonstrate my skills. The goal is to create a landing page with your name, project details, and a bio, accessible via the public IP of the server.

## Table of Contents
- [Provisioning the Server](#provisioning-the-server)
- [Installing Nginx Web Server](#installing-nginx-web-server)
- [HTML Page Deployment](#html-page-deployment)
- [Networking and Security](#networking-and-security)
- [Testing the Web Page](#testing-the-web-page)
- [Bonus Task: Configure HTTPS](#bonus-task-configure-https)
- [SSL Renewal via Cronjob](#ssl-renewal-via-cronjob)
- [Public IP Address](#public-ip-address)
- [Screenshot](#screenshot)

---

## Provisioning the Server
1. **Log in to AWS:**
   - Access [AWS Console](https://aws.amazon.com/console/).
   - Navigate to EC2 and launch a new instance.
2. **Choose AMI:**
   - Select Ubuntu 24.04 LTS.
3. **Instance Type:**
   - Choose t2.micro (free tier eligible).
4. **Configure Instance:**
   - Add necessary tags (Name: Altschool 2nd Semester Exam Server).
   - See to it that SSH key pair is created and downloaded.
5. **Security Group:**
   - Allow inbound traffic on ports 22 (SSH), 80 (HTTP), and 443 (HTTPS).
6. **Launch Instance:**
   - Download the private key (e.g., `Altschool-2nd-Semester-Exam-Server.pem`) for SSH access.

---

## Installing Nginx Web Server
1. **Connect to the Instance:**
   ```bash
   ssh -i Altschool-2nd-Semester-Exam-Server.pem ubuntu@<your-public-ip>
   ```
2. **Update the Server:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
3. **Install Nginx:**
   ```bash
   sudo apt install nginx -y
   ```
4. **Start Nginx:**
   ```bash
   sudo systemctl start nginx
   ```
5. **Enable Nginx to Start on Boot:**
   ```bash
   sudo systemctl enable nginx
   ```

---

## HTML Page Deployment
1. **Go over to the Web Root:**
   ```bash
   cd /var/www/html
   ```
2. **Create an HTML Page:**
   ```bash
   sudo nano index.html
   ```
3. **Add HTML Content:**
   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Welcome to [Oluwasegun Adepetu] Landing Page</title>
   </head>
   <body>
       <h1>Welcome to [Oluwasegun Adepetu] Landing Page</h1>
       <p>This is a simple landing page demonstrating server provisioning and deployment.</p>
       <p>[Full Bio]</p>
   </body>
   </html>
   ```
4. **Save and Exit:**
   ```bash
   CTRL + O, ENTER, CTRL + X
   ```
5. **Adjust Permissions:**
   ```bash
   sudo chmod 755 /var/www/html/index.html
   ```

---

## Networking and Security
1. **Security Group Configuration:**
   - Allow HTTP (port 80) and HTTPS (port 443) traffic.
   - Make sure SSH (port 22) is restricted to your IP for security.
2. **Verify Nginx Configuration:**
   ```bash
   sudo systemctl status nginx
   ```
3. **Restart Nginx if Needed:**
   ```bash
   sudo systemctl restart nginx
   ```

---

## Testing the Web Page
1. **Access the Web Page:**
   - Open a browser and visit `<your public-ip>`.
2. **Verify HTML Page Displays Properly.**

---

## Bonus Task: Configure HTTPS
1. **Install Certbot:**
   ```bash
   sudo apt install certbot python3-certbot-nginx -y
   ```
2. **Obtain SSL Certificate:**
   ```bash
   sudo certbot --nginx -d oluwasegun.me -d www.oluwasegun.me
   ```
3. **Verify SSL:**
   - Visit `https://oluwasegun.me` to confirm HTTPS is working.

---

## SSL Renewal via Cron job
1. **Edit Cron Jobs**
   ```bash
   sudo cronjob -e
2. **Add Renewal Cron job**
   ```bash
   0 0 * * * certbot renew --quiet && systemctl reload nginx

---

## Public IP Address
`http://54.229.90.2`
`https://oluwasegun.me`

---

## Screenshot
![Landing Page Screenshot](https://github.com/user-attachments/assets/fea8af91-3bd9-4ae7-9950-dc9c8adf80c6)



