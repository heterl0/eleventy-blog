---
title: My Journey in Setting Up WordPress with Nginx and SSL
description: My first Wordpress project I and my team has been work at University, Deloy on DigitalOcean free plan for student on three months.
date: 2025-02-12
tags:
  - experience
  - devOps
pageType: blog
---
## Introduction

As a front-end developer, I’ve always focused on building great user interfaces, but recently, I’ve been diving deeper into server management and deployment. In this blog, I’ll share my personal experience setting up WordPress on an Nginx server with SSL, a journey that has helped me understand web hosting, security, and performance optimization. Check me project [here](https://github.com/heterl0/vovinam-fusion-wp)!.

## Why I Chose This Setup

I wanted a reliable and secure setup for hosting WordPress sites, and after researching, I decided to use:

- **Ubuntu 22.04 LTS** for stability and security
- **Nginx** for better performance compared to Apache
- **SSL (Let’s Encrypt)** for security and HTTPS support

This combination ensures that my WordPress sites are fast, secure, and scalable.

## Step-by-Step Guide

### 1. Setting Up the Server

I started by updating my system and installing necessary packages:

```sh
sudo apt update && sudo apt upgrade -y
```

Then, I installed PHP, Nginx, and MySQL:

```sh
sudo apt install -y nginx mysql-server php-fpm php-mysql
```

This provided the foundation for running WordPress.

### 2. Installing and Configuring WordPress

I downloaded and extracted WordPress:

```sh
wget https://wordpress.org/latest.tar.gz
tar -xvzf latest.tar.gz
sudo mv wordpress /var/www/wordpress
```

I set the correct file permissions:

```sh
sudo chown -R www-data:www-data /var/www/wordpress/
sudo chmod -R 755 /var/www/wordpress/
```

### 3. Setting Up the Database

Using MySQL, I created a new database and user:

```sql
CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'securepassword';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
```

### 4. Configuring Nginx

I configured Nginx to serve WordPress efficiently. I edited the configuration file:

```sh
sudo nano /etc/nginx/sites-available/wordpress
```

Added the following configuration:

```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/wordpress;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

After saving, I enabled the configuration and restarted Nginx:

```sh
sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

### 5. Enabling SSL with Let’s Encrypt

To secure the site with HTTPS, I installed Certbot:

```sh
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
```

I obtained an SSL certificate and configured Nginx:

```sh
sudo certbot --nginx -d example.com -d www.example.com
```

To ensure automatic renewal:

```sh
sudo certbot renew --dry-run
```

## Lessons Learned

- **File Permissions Matter**: WordPress won’t work correctly if permissions are wrong.
- **Database Security Is Important**: Using a secure password and restricting privileges is crucial.
- **Nginx Configuration Can Be Tricky**: Testing with `nginx -t` before restarting saved me a lot of debugging time.
- **SSL Is a Must**: Modern websites need HTTPS for security and SEO benefits.

## Conclusion

Setting up WordPress with Nginx and SSL was a rewarding experience. Not only did it help me understand backend technologies, but it also made me appreciate the work that goes into web hosting and security. I hope this guide helps anyone looking to set up their own WordPress site with a strong, secure foundation.

This is just the beginning—next, I plan to explore performance optimizations and caching strategies. Stay tuned! 🚀