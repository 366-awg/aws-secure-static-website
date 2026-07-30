# Configuration Reference

## Overview

This document describes the final configuration of the AWS resources used to host the static portfolio website. It serves as a reference for the deployed environment by documenting the configuration applied to each AWS service.

The configurations described here represent the final state of the project after deployment and include enhancements made to improve security, reliability, and maintainability.

---

# Amazon S3 Configuration

Amazon S3 serves as the origin for the static website and stores all website assets.

## Bucket Configuration

| Configuration | Value |
|--------------|-------|
| Bucket Type | General Purpose |
| Static Website Hosting | Enabled |
| Bucket Versioning | Enabled |
| Default Encryption | Enabled |
| Encryption Type | Server-Side Encryption with Amazon S3 Managed Keys (SSE-S3) |
| Object Ownership | Bucket owner enforced (if applicable) |
| Public Read Access | Enabled for website hosting |

---

## Static Website Hosting

Static Website Hosting was enabled to allow Amazon S3 to serve website assets directly through its website endpoint.

The website bucket stores:

- HTML files
- CSS files
- Images
- Icons
- Other static resources

The index document was configured as:

```
index.html

```

---

## Bucket Versioning

Bucket Versioning was enabled to preserve previous versions of objects.

Benefits include:

- Recovery from accidental deletion
- Recovery from unintended overwrites
- Improved change management during future updates

---

## Default Encryption

Default encryption was configured using:

```
Server-Side Encryption with Amazon S3 Managed Keys (SSE-S3)
```

This ensures that all newly uploaded objects are automatically encrypted at rest without requiring manual encryption during uploads.

---

# Amazon CloudFront Configuration

Amazon CloudFront was configured as the Content Delivery Network (CDN) for the website.

## Origin

| Setting | Value |
|---------|-------|
| Origin Type | Amazon S3 Website Endpoint |
| Protocol | HTTP |
| Origin Domain | S3 Website Endpoint |

---

## Distribution

The CloudFront distribution was configured to:

- Serve website content globally
- Cache static assets
- Forward requests to the Amazon S3 website endpoint
- Improve website performance through edge caching

---

## Default Root Object

```
index.html
```

---

# AWS IAM Configuration

Deployment activities were performed using an IAM Administrator user.

The AWS root account was not used for routine deployment tasks.

This approach aligns with AWS security best practices by separating administrative activities from the root identity.

---

# Security Configuration

The following security-related configurations were applied.

| Configuration | Status |
|--------------|--------|
| IAM User for Administration | Enabled |
| Bucket Versioning | Enabled |
| Default Encryption (SSE-S3) | Enabled |
| CloudFront CDN | Configured |

---

# Configuration Summary

| AWS Service | Configuration Highlights |
|-------------|-------------------------|
| Amazon S3 | Static Website Hosting, Versioning, SSE-S3 |
| Amazon CloudFront | Global CDN with S3 Website Endpoint |
| AWS IAM | Administrator user for deployment |

---

# Summary

The deployed configuration combines Amazon S3 Static Website Hosting with Amazon CloudFront to provide a serverless hosting solution for static web content.

Configuration choices such as Bucket Versioning and Server-Side Encryption improve data resilience and security, while CloudFront enhances performance through global content caching.

This configuration provides a scalable, reliable, and cost-effective platform for hosting a static portfolio website.