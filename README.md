# Host a Static Website on AWS

This project demonstrates how to host a static HTML web app on AWS using a variety of AWS resources and DevOps practices. The website is deployed on EC2 instances within a Virtual Private Cloud (VPC) with enhanced security, scalability, and fault tolerance mechanisms.

## Project Overview

This setup leverages the following AWS resources:
1. **Virtual Private Cloud (VPC):** Configured with both public and private subnets across two different availability zones to enhance system reliability.
2. **Internet Gateway:** Facilitates connectivity between VPC instances and the Internet.
3. **Security Groups:** Used as a network firewall mechanism to control inbound and outbound traffic.
4. **Availability Zones:** Utilized across two zones for increased fault tolerance.
5. **Public Subnets:** Used for components such as the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect:** Securely connects to EC2 instances in both public and private subnets.
7. **Private Subnets:** Hosts web servers (EC2 instances) for enhanced security.
8. **NAT Gateway:** Allows instances in private subnets to access the Internet.
9. **EC2 Instances:** Hosts the static website.
10. **Application Load Balancer (ALB):** Evenly distributes web traffic across an Auto Scaling Group of EC2 instances.
11. **Auto Scaling Group:** Automatically manages EC2 instances, ensuring high availability and scalability.
12. **GitHub:** Stores project files for version control and collaboration.
13. **Certificate Manager:** Secures application communication using SSL/TLS certificates.
14. **Simple Notification Service (SNS):** Sends alerts about activities in the Auto Scaling Group.
15. **Route 53:** Used to register a domain and set up DNS records.
![Alt text](/Host-a-static-website-on-aws.jpg)

## Prerequisites
- AWS Account
- EC2 instances with proper IAM roles and permissions
- A registered domain name
- GitHub repository with the static website files
- Proper security group configurations

## Deployment Steps

1. **VPC Configuration:**
   - Create a VPC with public and private subnets across two availability zones.
   - Attach an Internet Gateway to the VPC for external connectivity.
   - Establish Security Groups for the instances and load balancer.

2. **EC2 Setup:**
   - Launch EC2 instances in the private subnets for web server hosting.
   - Ensure EC2 instances are able to connect to the Internet via the NAT Gateway.
   - Use an Auto Scaling Group to manage the number of instances.

3. **Load Balancer Configuration:**
   - Deploy an Application Load Balancer in the public subnets to distribute traffic across instances.
   - Configure a target group for the load balancer to ensure high availability.

4. **DNS Configuration:**
   - Register a domain name via Route 53 and configure DNS records to point to the load balancer.

5. **SSL/TLS Setup:**
   - Use AWS Certificate Manager to secure communications with an SSL certificate.

## Script for EC2 Instance Setup

The following script can be used to set up an EC2 instance to host the static website:

```bash
#!/bin/bash
# Switch to the root user to gain full administrative privileges
sudo su
# Update all installed packages to their latest versions
yum update -y
# Install Apache HTTP Server
yum install -y httpd
# Change the current working directory to the Apache web root
cd /var/www/html
# Install Git
yum install git -y
# Clone the project GitHub repository to the current directory
git clone https://github.com/Shawnty-z/Host-a-static-website-on-aws.git
# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-a-static-website-on-aws/. /var/www/html/
# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-a-static-website-on-aws
# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd
# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

## Monitoring & Notifications
- **SNS Alerts:** Configured to notify when significant events happen in the Auto Scaling Group, such as scaling activities.
  
## Conclusion
This project demonstrates how to host a static website on AWS using EC2 instances, load balancing, auto-scaling, and VPC configuration for security and scalability. The complete setup ensures high availability, fault tolerance, and secure communication for web traffic.
