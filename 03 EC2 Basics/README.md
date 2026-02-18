## Objective
To deploy and manage a basic web server on an Amazon EC2 instance by configuring compute resources, security groups, and remote access via SSH.

## Services Used
- Amazon EC2
- Amazon VPC (default networking)
- Security Groups

## Architecture Overview
User → Internet → EC2 Instance (Apache Web Server Running)

This project demonstrates how a virtual server can be deployed in the cloud and configured to host a basic web application accessible over the internet.

## Steps
1. Launched an EC2 instance using Amazon Linux 2023
2. Selected a t2.micro/t3.micro instance type
3. Created and downloaded a key pair for secure SSH access
4. Configured security group rules:
   - SSH (22) restricted to My IP
   - HTTP (80) open to the internet (0.0.0.0/0)
5. Connected to the instance using SSH from a local Mac terminal
6. Updated the system packages using dnf
7. Installed Apache (httpd) web server
8. Enabled and started the Apache service
9. Created a basic HTML page in /var/www/html/index.html
10. Accessed the website using the EC2 public IPv4 address

## Key Concepts Demonstrated
- Compute services using Amazon EC2
- Secure remote access using SSH and key pairs
- Network security using security groups
- Difference between public and private access
- Hosting a web server on a virtual machine
- Basic Linux command usage (dnf, systemctl)

## What I Learned
- EC2 instances act as virtual servers that can run applications in the cloud
- SSH access requires correct key pair permissions and security group configuration
- Security groups act as virtual firewalls controlling inbound traffic
- Web servers such as Apache can be installed and managed using systemctl
- Public accessibility requires both a public IP and correct inbound rules
- Troubleshooting connectivity often involves checking security groups and network settings

## Debugging & Issue Resolution
When attempting to connect using EC2 Instance Connect, access failed when SSH was restricted to My IP.

## Investigation Process
- Verified that the instance was running and passed all status checks
- Confirmed that a public IPv4 address was assigned
- Reviewed security group inbound rules

## Root Cause
EC2 Instance Connect does not always originate from the user’s local IP address. Restricting SSH access to My IP blocked the connection.

## Resolution
Used SSH from a local Mac terminal with a key pair:
```bash
ssh -i ~/.ssh/scott-ec2-basics-2026.pem ec2-user@YOUR_PUBLIC_IP
```
This allowed secure access while keeping SSH restricted to My IP.

## Key Learning
EC2 Instance Connect may require broader SSH access depending on AWS source IPs
Using SSH locally provides more control and aligns with security best practices
Security group rules must be carefully configured to balance access and security

## Security Considerations
SSH access was restricted to My IP to reduce exposure
HTTP access was open to the internet to allow public access to the website
Key pair permissions were secured using chmod 400
In production, additional controls such as HTTPS, load balancers, and IAM roles would be implemented

## Evidence
EC2 Instance Overview
Security Group Rules
SSH Connection
Apache Installation
Live Website
