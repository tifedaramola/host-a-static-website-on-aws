# Host a Static Website on AWS

## Overview
This project demonstrates how to host a static HTML web application on Amazon Web Services (AWS) using various AWS services to ensure reliability, scalability, and security. The project is structured to deploy the web app on an EC2 instance within a Virtual Private Cloud (VPC) with a robust networking and security setup.

## Architecture
The architecture involves the following components:
1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different availability zones.
2. **Internet Gateway**: Facilitates connectivity between VPC instances and the wider Internet.
3. **Security Groups**: Act as a network firewall to control traffic.
4. **Availability Zones**: Enhance system reliability and fault tolerance.
5. **Public Subnets**: Used for infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Provides secure connections to assets within both public and private subnets.
7. **Private Subnets**: Host web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Allows instances in private subnets to access the Internet.
9. **EC2 Instances**: Host the static website.
10. **Application Load Balancer**: Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple availability zones.
11. **Auto Scaling Group**: Manages EC2 instances automatically, ensuring website availability, scalability, fault tolerance, and elasticity.
12. **GitHub**: Stores web files for version control and collaboration.
13. **Certificate Manager**: Secures application communications.
14. **Simple Notification Service (SNS)**: Sends alerts about activities within the Auto Scaling Group.
15. **Route 53**: Registers the domain name and sets up DNS records.

## Deployment Steps

### Prerequisites
- AWS account
- Registered domain name
- GitHub repository for the web files

### Step-by-Step Guide

1. **Configure VPC**
   - Create a VPC with public and private subnets across two availability zones.
   - Set up an Internet Gateway and attach it to the VPC.
   - Create Security Groups to control inbound and outbound traffic.

2. **Deploy Infrastructure Components**
   - Deploy a NAT Gateway in a public subnet.
   - Set up an Application Load Balancer in public subnets.

3. **Set Up EC2 Instances**
   - Launch EC2 instances in private subnets for web hosting.
   - Configure EC2 Instance Connect Endpoint for secure access.

4. **Set Up Auto Scaling and Load Balancing**
   - Create an Auto Scaling Group for EC2 instances.
   - Configure the Application Load Balancer and a target group.

5. **Deploy the Static Website**
   - Use the following script to set up the web server and deploy the website from GitHub.

### Deployment Script

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
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

6. **Configure Domain and SSL**
   - Register the domain name with Route 53 and set up the necessary DNS records.
   - Use AWS Certificate Manager to obtain and configure SSL certificates for secure communication.

7. **Set Up Monitoring and Notifications**
   - Configure SNS to send alerts about Auto Scaling Group activities.

## Repository
The reference diagram and deployment scripts are available in the GitHub repository for this project: [GitHub Repository](https://github.com/tifedaramola/host-a-static-website-on-aws)

## Conclusion
By following this guide, you can host a static website on AWS, leveraging various services to ensure high availability, scalability, and security. The setup is designed to be robust and fault-tolerant, making use of AWS best practices for deploying web applications.
