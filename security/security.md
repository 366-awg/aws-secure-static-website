# Security Review

## Overview

This document reviews the security posture of the static portfolio website hosted on Amazon Web Services (AWS). It outlines the security measures implemented during the project, identifies architectural trade-offs, and highlights improvements that would be recommended for a production environment.

The objective of this review is to demonstrate an understanding of AWS security best practices while acknowledging the differences between an educational portfolio project and a production-grade deployment.

---

# Security Objectives

The primary security objectives for this project were to:

- Secure administrative access to AWS resources.
- Protect website assets stored in Amazon S3.
- Encrypt data at rest.
- Minimize operational risk while maintaining a simple serverless architecture.
- Follow AWS security best practices where applicable.

---

# Identity and Access Management

## Administrative Access

All deployment and management activities were performed using an AWS Identity and Access Management (IAM) user with administrative permissions.

The AWS root account was not used for routine administrative tasks.

This approach aligns with AWS best practices by limiting the use of the root account to tasks that explicitly require root-level privileges.

### Benefits

- Improved account security
- Better accountability for administrative actions
- Separation of privileged identities
- Reduced risk associated with root account usage

---

# Data Protection

## Server-Side Encryption

Default Server-Side Encryption was enabled on the Amazon S3 bucket using Amazon S3 Managed Keys (SSE-S3).

This ensures that all newly uploaded objects are automatically encrypted at rest without requiring additional configuration during uploads.

### Benefits

- Automatic encryption of stored objects
- No encryption management overhead
- Native AWS-managed encryption
- Protection of data at rest

---

## Bucket Versioning

Amazon S3 Versioning was enabled to preserve previous versions of uploaded objects.

Although Versioning is primarily a data protection feature rather than an access control mechanism, it contributes to the overall security posture by improving recoverability.

### Benefits

- Recovery from accidental object deletion
- Recovery from unintended overwrites
- Improved resilience during future website updates

---

# Storage Security

This project uses Amazon S3 Static Website Hosting as the origin for the website.

Because the Amazon S3 website endpoint requires public access to website objects, the bucket was configured with public read permissions.

Although this configuration is appropriate for educational projects and publicly accessible static websites, it is not considered the most secure architecture for production workloads.

---

# Content Delivery Security

Amazon CloudFront serves as the primary entry point for users accessing the website.

Using CloudFront provides several indirect security benefits:

- Reduces direct interaction with the Amazon S3 origin
- Supports integration with additional AWS security services
- Provides a foundation for future HTTPS implementation
- Enables more secure production architectures using Origin Access Control (OAC)

While this project uses the Amazon S3 website endpoint as the CloudFront origin, CloudFront remains an important component of the overall security architecture.

---

# Current Security Posture

The following security controls were implemented during the project.

| Security Control | Status |
|------------------|--------|
| IAM User for Administration | Implemented |
| Root Account Avoided for Daily Tasks | Implemented |
| Server-Side Encryption (SSE-S3) | Enabled |
| Amazon S3 Versioning | Enabled |
| Amazon CloudFront Distribution | Configured |

---

# Security Trade-Offs

Every architecture involves trade-offs between simplicity, functionality, and security.

For this project, the primary trade-off is the use of a public Amazon S3 bucket to support Static Website Hosting.

This approach simplifies deployment and aligns with the learning objectives of the project, but it exposes website objects for public read access.

For a personal portfolio website containing only static public content, this level of exposure is acceptable.

However, sensitive or private data should never be stored in a publicly accessible bucket.

---

# Production Recommendations

If this solution were deployed in a production environment, the following improvements would be recommended.

## Use a Private Amazon S3 Bucket

Replace public bucket access with a private Amazon S3 bucket.

---

## Implement CloudFront Origin Access Control (OAC)

Configure Amazon CloudFront Origin Access Control so that CloudFront becomes the only service permitted to access the S3 bucket.

This prevents direct public access to bucket objects.

---

## Configure HTTPS

Use AWS Certificate Manager (ACM) to provision an SSL/TLS certificate and configure CloudFront to serve all traffic over HTTPS.

---

## Register a Custom Domain

Use Amazon Route 53 together with CloudFront to provide a professional custom domain.

---

## Enable AWS WAF

Deploy AWS Web Application Firewall (AWS WAF) to provide additional protection against common web attacks.

---

## Continuous Monitoring

Enable AWS CloudTrail and Amazon CloudWatch to improve visibility into account activity and resource changes.

---

# Security Assessment

The implemented security controls are appropriate for a public-facing static portfolio website intended for educational and portfolio purposes.

The architecture follows several AWS security best practices, including:

- Using an IAM user instead of the root account.
- Encrypting objects at rest using SSE-S3.
- Enabling Bucket Versioning.
- Using managed AWS services to reduce operational risk.

While the solution intentionally prioritizes simplicity, it also establishes a clear path toward a production-ready architecture through the use of private storage, Origin Access Control, HTTPS, and additional monitoring services.

---

# Summary

Security was considered throughout the design and deployment of this project.

The implemented controls provide an appropriate balance between simplicity, maintainability, and protection for a static portfolio website.

The identified production recommendations demonstrate how the architecture can evolve into a more secure, enterprise-ready solution while continuing to leverage AWS managed services and cloud security best practices.