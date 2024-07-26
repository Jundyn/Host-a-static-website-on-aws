---

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web app on AWS using various services and configurations. The project includes a reference diagram, deployment scripts, and a detailed description of the AWS resources utilized.

## Project Overview

In this project, a static website is deployed on AWS using an EC2 instance within a well-architected VPC. The deployment leverages multiple AWS services to ensure scalability, reliability, and security. The primary components used are EC2 instances, an Application Load Balancer, an Auto Scaling Group, a NAT Gateway, and Route 53.

## Reference Diagram

The reference diagram illustrating the architecture is included in the GitHub repository.
![Uploading WhatsApp Image 2024-07-24 at 21.58.17.jpeg…]()

## Architecture

The architecture consists of:

1. **Virtual Private Cloud (VPC)**:
   - Configured with public and private subnets across two availability zones.
   - An Internet Gateway is deployed to facilitate connectivity between VPC instances and the Internet.
   
2. **Security Groups**:
   - Implemented as network firewalls to control inbound and outbound traffic to EC2 instances.

3. **Subnets and Availability Zones**:
   - Public subnets host infrastructure components like the NAT Gateway and Application Load Balancer.
   - Private subnets house the web servers (EC2 instances) for enhanced security.
   - Leveraged two Availability Zones to ensure system reliability and fault tolerance.

4. **EC2 Instances**:
   - Hosted in private subnets and managed using an Auto Scaling Group to ensure high availability and scalability.
   - An Application Load Balancer distributes traffic to EC2 instances across multiple Availability Zones.

5. **NAT Gateway**:
   - Allows instances in private subnets to access the Internet.

6. **Certificate Manager**:
   - Used for securing application communications.

7. **Simple Notification Service (SNS)**:
   - Configured to alert about activities within the Auto Scaling Group.

8. **Route 53**:
   - Used for DNS management and domain name registration.

## Deployment Instructions

The following script sets up an Apache HTTP server on an EC2 instance and deploys the static website from a GitHub repository.

### EC2 Instance Setup Script

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
git clone https://github.com/Jundyn/Host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Instructions

1. Launch an EC2 instance in a private subnet within your VPC.
2. SSH into the EC2 instance.
3. Run the script above to install and configure the Apache HTTP server and deploy your static website.

## GitHub Repository

- **Repository URL**: [Host-a-static-website-on-aws](https://github.com/Jundyn/Host-a-static-website-on-aws)

## Conclusion

This project demonstrates a complete setup for hosting a static website on AWS, leveraging a range of AWS services to ensure high availability, scalability, and security. For more detailed instructions and configuration, please refer to the files and diagrams provided in the GitHub repository.

---
