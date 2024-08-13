

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS, utilizing various AWS resources for optimal security, scalability, and reliability. The project leverages a variety of AWS services, including EC2, VPC, Internet Gateway, NAT Gateway, Application Load Balancer, Auto Scaling Group, and more.

## Project Overview

The static website is hosted on an EC2 instance within a Virtual Private Cloud (VPC) configured with both public and private subnets across two different availability zones. This setup ensures high availability and fault tolerance. The web app is deployed on EC2 instances located in private subnets for enhanced security, while a NAT Gateway and Application Load Balancer manage traffic and external access.

### Architecture Components:

1. **Virtual Private Cloud (VPC)**: Configured with public and private subnets across two availability zones to ensure reliability and fault tolerance.
2. **Internet Gateway**: Facilitates connectivity between the VPC instances and the internet.
3. **Security Groups**: Act as a network firewall to control inbound and outbound traffic.
4. **Availability Zones**: Used to enhance system reliability and fault tolerance.
5. **Public Subnets**: Used for infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Ensures secure connections to assets within both public and private subnets.
7. **Private Subnets**: Hosts the web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Allows instances in private subnets to access the internet.
9. **EC2 Instances**: Hosts the static website.
10. **Application Load Balancer**: Distributes web traffic evenly to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. **Auto Scaling Group**: Manages EC2 instances to ensure website availability, scalability, and fault tolerance.
12. **GitHub**: Used for version control and collaboration.
13. **AWS Certificate Manager**: Secures application communications.
14. **Simple Notification Service (SNS)**: Alerts about activities within the Auto Scaling Group.
15. **Route 53**: Used for domain name registration and DNS configuration.

## Prerequisites

- AWS Account
- GitHub repository with the website files
- Domain name registered with Route 53

## Deployment Instructions

1. **VPC and Subnets Configuration**:
    - Set up a VPC with both public and private subnets across two availability zones.
    - Deploy an Internet Gateway and associate it with the VPC.
    - Create security groups to control access to the EC2 instances.

2. **EC2 Instance Setup**:
    - Launch EC2 instances within the private subnets.
    - Ensure the instances can access the internet through a NAT Gateway.

3. **Install and Configure Apache Web Server**:

    Use the following bash script to install and configure the Apache HTTP Server on your EC2 instances:

    ```bash
    #!/bin/bash 
    sudo su 
    yum update -y 
    yum install -y httpd 
    cd /var/www/html 
    yum install git -y 
    git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git 
    cp -R host-a-static-website-on-aws/. /var/www/html/ 
    rm -rf host-a-static-website-on-aws 
    systemctl enable httpd  
    systemctl start httpd 
    ```

4. **Application Load Balancer and Auto Scaling Group**:
    - Set up an Application Load Balancer to distribute traffic across multiple EC2 instances.
    - Configure an Auto Scaling Group to manage the number of EC2 instances automatically.

5. **Domain and DNS Configuration**:
    - Register your domain with Route 53.
    - Configure DNS records to point to the Application Load Balancer.

6. **SSL Certificate**:
    - Use AWS Certificate Manager to secure your website with an SSL certificate.

7. **Monitoring and Notifications**:
    - Configure SNS to send alerts about activities in the Auto Scaling Group.

## Project Repository

All reference diagrams, deployment scripts, and additional resources are available in the [GitHub repository](https://github.com/aosnotes77/host-a-static-website-on-aws).

## License

This project is licensed under the MIT License.

---
