# Secure Static Website on AWS

A secure static site hosted on **AWS**, deployed and managed with **Terraform**.  
This project demonstrates best practices for cloud security and infrastructure as code.

## Architecture

> **Amazon S3**: Private bucket (no public access), encryption at rest, versioning enabled.  
> **CloudFront**: Global CDN with **Origin Access Control (OAC)** to enforce least privilege access to S3.  
> **AWS WAF**: Web Application Firewall attached to the CloudFront distribution, using managed rule sets and rate limiting.  
> **Terraform**: Infrastructure-as-Code for consistent, reproducible deployment.

### Request Flow

> Direct access to the S3 bucket is denied (returns 403).  
> Only CloudFront can fetch objects from S3.  
> All inbound requests are inspected at the edge by WAF.  

## Deployment

**Prerequisites**
- Terraform v1.5+
- AWS CLI configured
- An AWS account with permissions for S3, CloudFront, and WAF

**Steps**
```bash
# initialize Terraform
terraform init

# plan deployment
terraform plan -out=tfplan

# apply deployment
terraform apply tfplan
