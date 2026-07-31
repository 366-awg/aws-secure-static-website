# Security Review

## Overview

This document evaluates the security posture of the deployed AWS architecture. It documents the security controls implemented during deployment, explains how those controls protect the solution, and identifies additional AWS services that could further enhance the architecture in a production environment.

The solution was designed to demonstrate current AWS security best practices by combining Amazon CloudFront with a private Amazon S3 bucket protected through Origin Access Control (OAC).

---

# Security Objectives

The primary security objectives for this project were to:

* Secure administrative access to AWS resources.
* Protect website assets stored in Amazon S3.
* Prevent direct public access to the storage layer.
* Encrypt data at rest.
* Deliver content securely through Amazon CloudFront.
* Follow AWS security best practices using managed AWS services.

---

# Identity and Access Management

## Administrative Access

Administrative access to the AWS environment was performed using an IAM Administrator user rather than the AWS account root user.

The root account was reserved exclusively for account-level administrative tasks that require root privileges, aligning with AWS identity and access management best practices.

### Benefits

* Improved account security
* Better accountability for administrative actions
* Separation of privileged identities
* Reduced exposure of the root account

---

# Storage Security

## Private Amazon S3 Bucket

The portfolio website assets are stored in a private Amazon S3 bucket.

Block Public Access remains enabled, preventing users from accessing objects directly through Amazon S3.

Website content is accessible only through Amazon CloudFront.

### Benefits

* Eliminates direct public access to stored objects
* Reduces the attack surface
* Aligns with AWS recommended security practices

---

# Origin Access Control (OAC)

Amazon CloudFront is configured with Origin Access Control (OAC).

Origin Access Control (OAC) authenticates requests from Amazon CloudFront to the private Amazon S3 origin. Amazon S3 authorizes only requests originating from the associated CloudFront distribution according to the configured bucket policy.

### Benefits

* Secure communication between CloudFront and Amazon S3
* Prevents bypassing CloudFront
* Protects the private S3 origin
* Eliminates the need for publicly accessible bucket objects

---

# Data Protection

## Server-Side Encryption

Default Server-Side Encryption is enabled using Amazon S3 Managed Keys (SSE-S3).

All newly uploaded objects are automatically encrypted while stored in Amazon S3.

### Benefits

* Automatic encryption at rest
* No manual encryption management
* Native AWS-managed encryption

---

## Bucket Versioning

Amazon S3 Versioning is enabled to preserve previous versions of uploaded objects.

Although primarily a resilience feature, Versioning contributes to overall data protection.

### Benefits

* Recovery from accidental deletion
* Recovery from unintended overwrites
* Simplified rollback during website updates

---

# Content Delivery Security

Amazon CloudFront serves as the public entry point for all website traffic.

The CloudFront distribution provides:

* Global edge caching
* HTTPS content delivery
* Secure communication with Amazon S3 through OAC
* Improved performance
* Reduced origin requests

Because users interact only with CloudFront, the Amazon S3 bucket remains protected from direct public access.

---

# Current Security Controls

The following security controls were implemented.

| Security Control                     | Status      |
| ------------------------------------ | ----------- |
| IAM Administrator User               | Implemented |
| Root Account Avoided for Daily Tasks | Implemented |
| Amazon S3 Block Public Access        | Enabled     |
| Private Amazon S3 Bucket             | Implemented |
| Server-Side Encryption (SSE-S3)      | Enabled     |
| Amazon S3 Versioning                 | Enabled     |
| Amazon CloudFront Distribution       | Configured  |
| Origin Access Control (OAC)          | Enabled     |
| HTTPS Content Delivery               | Enabled     |

---

# Security Assessment

The implemented architecture follows modern AWS security best practices for hosting static websites.

Key strengths include:

* Private object storage
* No direct public access to Amazon S3
* Secure origin authentication using Origin Access Control
* Encryption of data at rest
* Global content delivery through Amazon CloudFront
* Reduced operational overhead through managed AWS services
* Enforced private origin architecture using Amazon CloudFront and Origin Access Control

These controls significantly improve the security posture compared to architectures that rely on publicly accessible Amazon S3 website endpoints.

---

# Production Recommendations

Although the implemented architecture is secure for a portfolio website, additional services could further strengthen a production deployment.

## Amazon Route 53

Configure a custom domain and DNS management using Amazon Route 53.

---

## AWS Certificate Manager (ACM)

Use a custom domain secured with an AWS Certificate Manager (ACM) SSL/TLS certificate.

---

## AWS Web Application Firewall (AWS WAF)

Protect the application against common web attacks and malicious traffic.

---

## AWS CloudTrail

Enable AWS CloudTrail to record account activity and API calls for auditing and security investigations.

---

## Amazon CloudWatch

Monitor CloudFront and Amazon S3 metrics, configure alarms, and improve operational visibility.

---

## CloudFront Logging

Enable CloudFront access logging to analyze request patterns, troubleshoot issues, and support security monitoring.

---

# Security Principles

The implemented architecture is based on several core AWS security principles:

- Least privilege access through IAM.
- Private object storage using Amazon S3.
- Origin protection using Amazon CloudFront and Origin Access Control (OAC).
- Encryption of stored data using Server-Side Encryption (SSE-S3).
- Secure content delivery over HTTPS.
- Use of fully managed AWS services to reduce operational risk.

These principles provide a strong security foundation while minimizing administrative complexity.

# Summary

Security was a primary design consideration throughout this project.

By combining Amazon CloudFront with a private Amazon S3 bucket protected by Origin Access Control (OAC), the architecture prevents direct public access to stored website assets while providing secure, scalable, and highly available content delivery.

Additional AWS services such as AWS WAF, CloudTrail, CloudWatch, and Route 53 can further enhance the solution for production workloads, but the implemented architecture already reflects current AWS recommendations for securely hosting static website content.
