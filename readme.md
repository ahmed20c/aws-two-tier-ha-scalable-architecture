# Two-Tier Highly Available and Highly Scalable Architecture on AWS

**Author:** Ahmed Ali  
**AWS Region:** US East (N. Virginia) — `us-east-1`  
**Case Study:** Cloudforall.in Cloud Migration

## Project Overview
This project implements a production-grade, two-tier web application architecture on Amazon Web Services (AWS) to replace an on-premises setup, delivering high availability, automatic scaling, low latency, and layered network security.

## AWS Services Used
- **Networking & Security:** Amazon VPC (`Demo-vpc`, `10.0.0.0/16`), Public & Private Subnets across 2 Availability Zones (`us-east-1a`, `us-east-1b`), Internet Gateway, NAT Gateways, Security Groups (`ALB-SG`, `WEB-SG`, `DB-SG`)
- **Compute & Load Balancing:** Amazon EC2 (Ubuntu, Apache2, PHP 8.5), Custom AMI (`TEST-WEB-SERVER-AMI`), Launch Template (`Labdemo`), Auto Scaling Group (`Lab-ASG`, Min: 2, Desired: 2, Max: 3), Application Load Balancer (`Lab-ALB-1`), Target Group (`Lab-TG-1`)
- **Database & Storage:** Amazon RDS (MySQL `db.t3.micro`, private access only), Amazon S3 (`labdemotask-1-capstone-2026`)
- **Edge Delivery & Protection:** Amazon CloudFront (`Labdemo-CloudFront`), AWS WAF (Core protections & Rate limiting)
- **Operations & Monitoring:** AWS IAM (`SSMRole`), VPC Interface Endpoint (`SSMMessages-Endpoint`), AWS Systems Manager Patch Manager (`Demo-Patch`), Amazon CloudWatch (`CPUUtilization`)

## Implementation Summary (12 Tasks)
1. **VPC Networking:** Created `Demo-vpc` across two Availability Zones with 2 public subnets, 2 private subnets, an Internet Gateway, and 2 NAT Gateways.
2. **Security Groups:** Configured `WEB-SG` and `DB-SG` to isolate the web and database tiers.
3. **Test EC2 Instance:** Launched `TEST-WEB-SERVER`, installed Apache2, PHP, and `php-mysql`, and created `/var/www/html/index.php`.
4. **RDS MySQL Database:** Provisioned `database-1` in a private network configuration with `DB-SG`.
5. **Database Connectivity:** Connected `index.php` to the RDS endpoint and verified `"Database connection succeeded."`
6. **S3 Static Media Hosting:** Created an S3 bucket, uploaded `AWS.jpg`, enabled public read via ACL, and embedded it in `index.php`.
7. **Golden AMI:** Captured `TEST-WEB-SERVER-AMI` from the configured instance.
8. **Security Hardening:** Created `ALB-SG` and restricted `WEB-SG` HTTP traffic to `ALB-SG` and SSH to `10.0.0.0/16`.
9. **High Availability & Auto Scaling:** Deployed `Labdemo` Launch Template, `Lab-ASG`, `Lab-ALB-1`, and `Lab-TG-1` with 2 healthy targets across `us-east-1a` and `us-east-1b`.
10. **CloudFront & AWS WAF:** Configured `Labdemo-CloudFront` with HTTPS redirection, `Managed-CachingOptimized`, and AWS WAF protections.
11. **Secure Patching:** Created `SSMRole`, deployed `SSMMessages-Endpoint`, and configured `Demo-Patch` in Systems Manager Patch Manager.
12. **CloudWatch Monitoring:** Configured `CPUUtilization` graphs for all running ASG instances.

## Documentation
Full step-by-step documentation with 48 implementation screenshots is available in:  
`Two_Tier_HA_Scalable_AWS_Architecture_Documentation.pdf`
