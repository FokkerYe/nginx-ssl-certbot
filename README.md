# nginx-ssl-certbot
nginx-ssl-certbot
# Nginx Setup with SSL on Ubuntu

This guide walks you through installing Nginx, setting up a website, and securing it with a free SSL certificate using Certbot.

---

## Step 1: Install Nginx

Update your package index and install Nginx:

```bash
sudo apt update
sudo apt install -y nginx
```
## Enable and start Nginx to run at boot:
```
sudo systemctl enable --now nginx
```
# Optional: Configure UFW Firewall

# If using UFW, allow Nginx traffic:
```
sudo ufw allow 'Nginx Full'
sudo ufw status
```
# Verify Nginx Installation

# Check the service status:
```
sudo systemctl status nginx
```
## Test Nginx configuration:
```
sudo nginx -t
```
## Step 2: Create Website Root & Nginx Server Block
Create Website Directory
```
sudo mkdir -p /var/www/test.ayk.beauty.com
sudo chown -R $USER:$USER /var/www/test.ayk.beauty.com
```
Create a simple index page:
```
echo "Hello from test.ayk.beauty.com" | sudo tee /var/www/test.ayk.beauty.com/index.html
```
Create Nginx Server Block

Open a new Nginx configuration file:
```
sudo nano /etc/nginx/sites-available/test.ayk.beauty.com
```
Add the following content:
```
server {
    listen 80;
    server_name test.ayk.beauty;

    root /var/www/test.ayk.beauty.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

```
Enable the site by creating a symbolic link:
```
sudo ln -sf /etc/nginx/sites-available/test.ayk.beauty.com /etc/nginx/sites-enabled/
```
Test Nginx configuration and reload:
```
sudo nginx -t
sudo systemctl reload nginx
```
Check the website using curl:
```
curl -i http://test.ayk.beauty
```
## Step 3: Install Certbot

Update packages and install Certbot for Nginx:
```
sudo apt update
sudo apt install -y certbot python3-certbot-nginx
```
Check Certbot version:
```
certbot --version
```
## Step 4: Obtain SSL Certificate

Use Certbot to automatically configure SSL for your Nginx site:
```
sudo certbot --nginx -d test.ayk.beauty -m you@example.com --agree-tos --no-eff-email --redirect --noninteractive
```
## Check SSL Certificate Details
```
sudo certbot certificates
```
## Test Automatic Renewal

Perform a dry run to ensure automatic renewal works:
```
sudo certbot renew --dry-run
```


