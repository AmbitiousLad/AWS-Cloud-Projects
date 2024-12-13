# Multi-Tier App Deployment on AWS Cloud

## Overview
This project demonstrates the deployment of a multi-tier application on AWS Cloud. The infrastructure includes a VPC with public and private subnets, an S3 bucket for storing necessary files, and three tiers: web, app, and database. The web tier is connected to an external load balancer, which handles incoming internet traffic. The app tier is connected to an internal load balancer, and the database tier utilizes an RDS instance. Auto-scaling groups are configured for the app and web tiers to ensure high availability and scalability.

## Architecture
### Components:
1. **VPC and Subnets:**
   - A VPC with six subnets (2 public and 4 private).

2. **S3 Bucket:**
   - An S3 bucket to store all necessary files.

3. **Three Tiers:**
   - **Web Tier:**
     - Connected to an external load balancer (open to the internet).
   - **App Tier:**
     - Connected to an internal load balancer.
   - **Database Tier:**
     - Utilizes an RDS instance.

4. **Auto Scaling Groups:**
   - Configured for both app tier and web tier with a minimum of 2 instances each.

5. **Security Groups:**
   - **web-sg:** Security group for the web tier instance.
   - **app-sg:** Security group for the app tier instances.
   - **int-app-sg:** Security group for the internal load balancer.
   - **web-lb-sg:** Security group for the web load balancer.
   - **rds-sg:** Security group for RDS.

## Deployment Steps

### 1. Create VPC and Subnets
   - Create a VPC.
   - Create 2 public subnets and 4 private subnets within the VPC.

### 2. Create S3 Bucket
   - Create an S3 bucket to store all necessary files.

### 3. Set Up Database Tier
   - Create an RDS instance within the private subnets.
   - Configure the `rds-sg` security group to allow access from the app tier.

### 4. Set Up App Tier
   - Launch EC2 instances within the private subnets for the app tier.
   - Configure the `app-sg` security group to allow access from the internal load balancer.
   - Create an internal load balancer and configure it with the `int-app-sg` security group.

### 5. Set Up Web Tier
   - Launch EC2 instances within the public subnets for the web tier.
   - Configure the `web-sg` security group to allow internet traffic.
   - Create an external load balancer and configure it with the `web-lb-sg` security group.
   - Ensure the external load balancer routes traffic to the internal load balancer.

### 6. Configure Auto Scaling Groups
   - Initialize auto-scaling groups for the app tier and web tier with a minimum of 2 instances each.

### 7. Testing and Validation
   - Ensure all instances are running and properly connected.
   - Validate the end-to-end connectivity and performance.

## Diagram
![Architecture Diagram]

![Screenshot 2024-12-13 171121](https://github.com/user-attachments/assets/ff328dd7-4f06-4eb9-8197-b60fc7613bcd)


## Files and Directories
- `conf.d`: Configuration files.
- `scripts`: Deployment scripts.
- `nginx.conf`: Nginx configuration file.

## Conclusion
This project showcases a robust and scalable multi-tier application deployment on AWS, utilizing best practices for high availability, security, and performance. 

## License
This project is licensed under the MIT License - see the LICENSE file for details.



