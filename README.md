# ICT171 Cloud Server Project — AWS EC2 + NGINX

**Student Name:** Kareem Khalil  
**Student Number:** 35729084  
**Public IP:** 13.48.26.137  
**Domain Name:** https://kareemcloudserver.online  
**Video Link:**  https://screenrec.com/share/XfFqHcWBZ5

---

## 1. Overview
This project demonstrates the complete setup and deployment of a cloud-based web server using Amazon EC2, Ubuntu 22.04, NGINX, a custom webpage, Namecheap DNS, and HTTPS using Certbot.  
The project includes:

- Launching and configuring a real EC2 cloud server  
- Using Linux and command-line tools  
- Installing and configuring NGINX  
- Deploying a custom HTML website  
- Registering and connecting a domain name  
- Enabling HTTPS using SSL/TLS  
- Creating and running a custom Bash script  
- Documenting the full process  

This documentation is detailed enough so that another ICT171 student can fully recreate this server from scratch.

---

## 2. Creating the EC2 Instance

### 2.1 Instance Configuration
- **Cloud Provider:** AWS  
- **Service:** EC2  
- **AMI:** Ubuntu Server 22.04 LTS  
- **Instance Type:** t2.micro  
- **Storage:** 8GB gp2  
- **Key Pair:** ict171-key.pem  
- **Security Group Inbound Rules:**  
  - SSH (22): My IP  
  - HTTP (80): 0.0.0.0/0  
  - HTTPS (443): 0.0.0.0/0  

### 2.2 Connecting to the Server (SSH)
Using Windows PowerShell:

```
ssh -i .\ict171-key.pem ubuntu@13.48.26.137
```

---

## 3. Updating the Server

```
sudo apt update
sudo apt upgrade -y
```

---

## 4. Installing and Enabling NGINX

Install NGINX:

```
sudo apt install nginx -y
```

Enable and verify:

```
sudo systemctl enable nginx
sudo systemctl status nginx
```

The status should show **active (running)**.

---

## 5. Deploying the Custom Website

### 5.1 Navigate to hosting directory
```
cd /var/www/html
```

### 5.2 Remove default NGINX page
```
sudo rm index.nginx-debian.html
```

### 5.3 Create custom HTML page
```
sudo nano index.html
```

A custom HTML website was added containing:

- Student name  
- Student number  
- Public IP  
- ICT171 course details  
- Server information  

The webpage loads correctly via browser.

---

## 6. Domain Name Setup (Namecheap)

A domain was registered:

**kareemcloudserver.online**

DNS settings:

| Type | Host | Value        | TTL  |
|------|------|--------------|------|
| A    | @    | 13.48.26.137 | Auto |
| A    | www  | 13.48.26.137 | Auto |

After propagation, the domain successfully pointed to the NGINX server.

Website accessible at:

```
http://kareemcloudserver.online
```

---

## 7. Enabling HTTPS with Certbot (SSL/TLS)

Install Certbot:

```
sudo apt install certbot python3-certbot-nginx -y
```

Generate SSL certificates:

```
sudo certbot --nginx -d kareemcloudserver.online -d www.kareemcloudserver.online
```

Test auto-renewal:

```
sudo certbot renew --dry-run
```

Website now accessible securely at:

```
https://kareemcloudserver.online
```

---

## 8. Custom Script (Update & Log)

A Bash script was created to automate server updates and log the timestamp.

### 8.1 Script Location
`/usr/local/bin/update-log.sh`

### 8.2 Script Contents

```
#!/bin/bash
sudo apt update && sudo apt upgrade -y
echo "Server successfully updated on: $(date)" >> /var/log/update-history.txt
```

### 8.3 Make script executable
```
sudo chmod +x /usr/local/bin/update-log.sh
```

### 8.4 Run script
```
sudo /usr/local/bin/update-log.sh
```

### 8.5 Verify log file
```
sudo cat /var/log/update-history.txt
```

---

## 9. Testing

- NGINX running and enabled  
- Custom HTML website loads over HTTP and HTTPS  
- SSL certificate installed and auto-renew tested  
- DNS resolves globally  
- Custom script logs update events  
- Website reachable using domain name  

---

## 10. Video Demonstration

The video will demonstrate:

- Creating the EC2 instance  
- Connecting via SSH  
- Updating the server  
- Installing NGINX  
- Deploying the custom website  
- Setting up Namecheap DNS  
- Installing HTTPS using Certbot  
- Running the custom script  
- Verifying everything works  

**Video Link:** https://screenrec.com/share/XfFqHcWBZ5

---

## 11. References

- AWS EC2 Documentation  
- NGINX Documentation  
- Certbot Documentation  
- Namecheap DNS Guide  
- ICT171 Unit Material  

---

# End of Documentation
This README meets the ICT171 requirements for cloud server documentation.
