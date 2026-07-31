# Configuration Reference

## Overview

This document describes the final configuration of the AWS resources used to host the portfolio website. This document serves as the definitive technical reference for the deployed AWS environment, documenting the final configuration of each service after implementation.

The architecture follows current AWS best practices by using Amazon CloudFront with Origin Access Control (OAC) to securely serve content from a private Amazon S3 bucket.

---

# Amazon S3 Configuration

Amazon S3 stores the portfolio website's static assets and serves as the origin for the Amazon CloudFront distribution.

## Bucket Configuration

| Configuration          | Value                                                       |
| ---------------------- | ----------------------------------------------------------- |
| Bucket Type            | General Purpose                                             |
| Static Website Hosting | Disabled                                                    |
| Bucket Versioning      | Enabled                                                     |
| Default Encryption     | Enabled                                                     |
| Encryption Type        | Server-Side Encryption with Amazon S3 Managed Keys (SSE-S3) |
| Object Ownership       | Bucket owner enforced                                       |
| Block Public Access    | Enabled                                                     |
| Bucket Access          | Private (Accessible only through Amazon CloudFront)         |

---

## Object Storage

The bucket stores the static website assets, including:

* HTML files
* CSS stylesheets
* JavaScript files
* Images
* Icons
* Other static resources

Direct public access to these objects is disabled.

---

## Bucket Versioning

Bucket Versioning was enabled to preserve previous versions of objects.

Benefits include:

* Recovery from accidental deletion
* Recovery from unintended overwrites
* Simplified rollback during future website updates

---

## Default Encryption

Default encryption is configured using:

```text
Server-Side Encryption with Amazon S3 Managed Keys (SSE-S3)
```

All newly uploaded objects are automatically encrypted at rest.

---

# Amazon CloudFront Configuration

Amazon CloudFront serves as the global Content Delivery Network (CDN) and the public entry point for all website requests.

## Origin Configuration

| Setting         | Value                       |
| --------------- | --------------------------- |
| Origin Type     | Amazon S3 Bucket            |
| Origin Access   | Origin Access Control (OAC) |
| Origin Protocol | HTTPS (AWS Signed Requests) |
| Origin Domain   | anngithinji-webportfolio.s3.us-east-1.amazonaws.com |

---

## Distribution Configuration

The CloudFront distribution is configured to:

* Serve website content globally.
* Cache frequently requested objects at AWS edge locations.
* Retrieve objects securely from the Amazon S3 origin.
* Authenticate origin requests using Origin Access Control (OAC).
* Improve website performance through edge caching.
---

## Default Root Object

```text
index.html
```

---

# Origin Access Control (OAC)

Origin Access Control is enabled to allow Amazon CloudFront to securely access the private Amazon S3 bucket.

With OAC enabled:

* Amazon S3 objects remain private.
* CloudFront signs all origin requests using AWS Signature Version 4 (SigV4).
* The bucket policy allows access only from the authorized CloudFront distribution.
* Users cannot bypass CloudFront and access Amazon S3 directly.

---

# AWS Identity and Access Management (IAM)

AWS resources were provisioned and managed using an IAM Administrator user in accordance with AWS security best practices. The AWS account root user was reserved exclusively for account-level administrative tasks.

The AWS account root user was not used for routine administrative tasks.

---

# Security Configuration

The following security controls were implemented.

| Configuration                   | Status     |
| ------------------------------- | ---------- |
| IAM Administrator User          | Configured |
| Block Public Access             | Enabled    |
| Bucket Versioning               | Enabled    |
| Server-Side Encryption (SSE-S3) | Enabled    |
| Origin Access Control (OAC)     | Enabled    |
| CloudFront Distribution         | Configured |
| HTTPS Content Delivery          | Enabled    |

---

# Configuration Summary

| AWS Service       | Configuration Highlights                                |
| ----------------- | ------------------------------------------------------- |
| Amazon S3         | Private Bucket, Versioning, SSE-S3, Block Public Access |
| Amazon CloudFront | Global CDN with Origin Access Control (OAC)             |
| AWS IAM           | IAM Administrator User for Deployment                   |

---

# Summary

The final configuration follows modern AWS architectural best practices by combining Amazon CloudFront with a private Amazon S3 bucket using Amazon CloudFront with Origin Access Control (OAC) to securely access a private Amazon S3 origin.

Amazon CloudFront acts as the public entry point for all website requests, while Amazon S3 securely stores the website assets without exposing them directly to the internet.

This architecture improves security, scalability, performance, and operational simplicity while maintaining a cost-effective solution for hosting static website content.

# Deployment State

At the time this documentation was created, the deployed environment reflects the production configuration of the portfolio website.

The documented settings represent the final operational state of the AWS resources and provide a reference for future maintenance, troubleshooting, and enhancement of the solution.
