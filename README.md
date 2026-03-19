# Linux Azure Web Server Project

## Overview
This project demonstrates the deployment and configuration of a Linux-based web server hosted on Microsoft Azure. The goal was to build, secure, and manage a public-facing server using real-world cloud and Linux administration practices.

## What I Built
* Deployed an Ubuntu Linux Virtual Machine on Azure
* Configured networking and access using Network Security Groups (NSG)
* Installed and configured Apache web server
* Hosted a custom HTML webpage
* Configured secure SSH access using key-based authentication
* Disabled password authentication and root login for improved security
* Managed file permissions and ownership using `chmod` and `chown`
* Enabled Apache to start automatically on system boot
* Configured HTTPS using SSL on Apache
  
## Technologies Used
* Microsoft Azure
* Linux (Ubuntu 22.04)
* Apache2
* SSH
* Bash
* OpenSSL
  
## Security Configuration
* Enforced SSH key-based authentication for secure remote access
* Disabled password authentication (`PasswordAuthentication no`)
* Disabled root login (`PermitRootLogin no`)
* Configured Network Security Group (NSG) rules:
  * Port 22 (SSH) restricted for administrative access
  * Port 80 (HTTP) allowed for web traffic
  * Port 443 (HTTPS) allowed for encrypted traffic
* Enabled Apache SSL module and configured HTTPS (port 443)
* Verified Apache is actively listening on port 443
* Implemented encrypted communication using SSL (self-signed / non-production setup)
  
## Web Server Setup
* Installed Apache using package manager (`apt`)
* Deployed custom `index.html` to `/var/www/html`
* Configured correct file permissions for web access
* Served website via public IP address

## HTTPS Configuration Details
* Generated a self-signed SSL certificate using OpenSSL
* Enabled Apache SSL module (`a2enmod ssl`)
* Configured Apache to use SSL certificate
* Enabled HTTPS (port 443)

## Validation Performed
* Verified Apache is listening on port 443:
  `sudo ss -tuln | grep 443`
  `sudo a2query -m ssl`

## Important Note
* This HTTPS setup uses a self-signed certificate and is accessed via a public IP address.

## As a result:
*Browsers display a "Not Secure" warning
*The certificate is not issued by a trusted Certificate Authority (CA)

## How It Works (Flow)
* User accesses the public IP via browser (HTTP/HTTPS)
* Azure NSG allows traffic on ports 80/443
* Apache web server receives the request
* Apache serves content from `/var/www/html`
* Browser displays the webpage

## Key Linux Commands Used
* System update and Apache installation
  `sudo apt update`
  `sudo apt install apache2`
* Apache service management
  `sudo systemctl start apache2`
  `sudo systemctl enable apache2`
  `sudo systemctl status apache2`
* File permissions and ownership
  `chmod 644 index.html`
  `chown azureuser:azureuser /var/www/html`
* SSH key security
  `chmod 400 azure-linux-key.pem`
* Enable SSL and restart Apache
  `sudo a2enmod ssl`
  `sudo systemctl restart apache2`
* Validation checks
  `sudo ss -tuln | grep 443`
  `sudo a2query -m ssl`

## Screenshots
### Website
![Website](images/website.png)
### Azure VM Overview
![VM Overview](images/vm-overview.png)
### Network Security Group Rules
![NSG Rules](images/nsg-rules.png)
### Azure Resources
![Resources](images/resources.png)
### SSH Access
![SSH Access](images/ssh-access.png)

## What I Learned
* How to deploy and manage a Linux VM in Azure
* How Network Security Groups control inbound traffic
* How SSH key-based authentication improves system security
* Linux file permissions and ownership concepts
* How Apache serves web content over HTTP/HTTPS
* The difference between encrypted HTTPS and trusted certificates
* How to validate services using real Linux commands

## Improvements (Next Steps)
* Use a real domain name instead of public IP
* Implement a trusted SSL certificate (e.g. Let’s Encrypt)
* Configure automatic SSL certificate renewal
* Redirect HTTP traffic to HTTPS
* Restrict SSH access to specific IP addresses
* Add firewall hardening (UFW)
* Deploy using Infrastructure as Code (Terraform or ARM/Bicep)
* Implement load balancing for high availability

## Result
A fully functional, publicly accessible Linux web server hosted in Azure, secured using best practices and supporting encrypted HTTPS traffic (self-signed configuration).

Built by Quentin

