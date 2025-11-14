ICT171 Cloud Server Project — AWS EC2 + NGINX

Student Name: Kareem
Student Number: (enter your student number)
Public IP: (your EC2 public IP here)
Domain Name: (to be added later)
Video Link: (to be added after recording)
-----------------------------------------------------------------------------------------------------------------------------
1. Overview

This project demonstrates the setup and configuration of a cloud-based web server using Amazon EC2.
The server runs Ubuntu Server 22.04 LTS and uses NGINX to host a custom webpage.

All commands and configuration steps are included so that another ICT171 student can fully rebuild this server from scratch.

-----------------------------------------------------------------------------------------------------------------------------
2. Creating the EC2 Instance
2.1 AWS Instance Settings

  Cloud Provider: Amazon Web Services
  Service: EC2 (Elastic Compute Cloud)
  AMI: Ubuntu Server 22.04 LTS (x86_64)
  Instance Type: t2.micro
  Key Pair: ict171-key.pem
  Storage: 8GB gp2
  Security Group Rules:
    SSH (22) — My IP only
    HTTP (80) — Anywhere (0.0.0.0/0)
    
2.2 Connecting to the Server

From Windows PowerShell:

  ssh -i .\ict171-key.pem ubuntu@3.144.10.65
  
-----------------------------------------------------------------------------------------------------------------------------
3. Updating the Server

After logging into the instance, all packages were updated using:

sudo apt update
sudo apt upgrade -y

-----------------------------------------------------------------------------------------------------------------------------
4. Installing NGINX Web Server

NGINX was installed and enabled to start automatically on boot:

sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl status nginx

This returned Active: active (running).

The default NGINX webpage was visible by entering the server’s public IP in a browser.

-----------------------------------------------------------------------------------------------------------------------------
5. Deploying the Custom Website
5.1 Navigate to the hosting directory
cd /var/www/html

5.2 Remove the default NGINX page
sudo rm index.nginx-debian.html

5.3 Create and add a custom webpage
sudo nano index.html


A custom HTML file was added containing project information, including:

  Student name
  Student number
  Public IP
  Course name (ICT171)
  Server status

The new webpage loads successfully when visiting the EC2 public IP in a browser.

-----------------------------------------------------------------------------------------------------------------------------
6. DNS Setup (To Be Completed Later)

A domain name will be linked to the EC2 server with these steps:

  Register domain (Freenom or Namecheap)

  Create an A Record:
    Name: @
    Type: A
    Value: EC2 Public IP
    TTL: 300
  Wait for propagation (5–30 minutes)

This will allow the website to be accessible through a URL instead of an IP address.

-----------------------------------------------------------------------------------------------------------------------------
7. Custom Script (Required for ICT171)
7.1 Script Location

  /usr/local/bin/update-log.sh

7.2 Script Contents

  #!/bin/bash
  sudo apt update && sudo apt upgrade -y
  echo "Server updated on: $(date)" >> /var/log/update-history.txt

7.3 Make the script executable

  sudo chmod +x /usr/local/bin/update-log.sh

7.4 Run the script

  sudo /usr/local/bin/update-log.sh

This script performs system updates and logs the time and date to /var/log/update-history.txt.

-----------------------------------------------------------------------------------------------------------------------------
8. Testing

  Verified NGINX running with systemctl status nginx
  Confirmed public IP loads custom webpage
  Verified /var/log/update-history.txt is created after running script
  Server accessible externally via HTTP port 80
  
-----------------------------------------------------------------------------------------------------------------------------
9. Video Demonstration

The video (to be added) will demonstrate:
  EC2 instance creation
  SSH connection
  Server updates
  NGINX installation
  Custom webpage deployment
  Script execution
  Website accessibility
  
-----------------------------------------------------------------------------------------------------------------------------
10. References

AWS EC2 Documentation
Ubuntu Package Manager Docs
NGINX Official Documentation
ICT171 Unit Materials
