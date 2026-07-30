# Architecture Description

## Overview

This document provides a detailed explanation of the architecture used to host the portfolio website on Amazon Web Services (AWS). The solution adopts a serverless architecture that uses fully managed AWS services to deliver static web content with minimal operational overhead.

The architecture is intentionally designed to demonstrate foundational cloud engineering concepts, including static website hosting, global content delivery, object versioning, data encryption, and Identity and Access Management (IAM). By relying on managed services instead of traditional web servers, the solution remains simple to operate, scalable, and cost-effective.

---

## Architecture Diagram

<p align="center">
  <img src="architecture.png" alt="Architecture Diagram" width="900">
</p>

---

## Architectural Design

The architecture consists of three primary components that work together to deliver the website to end users.

```
User
   │
   ▼
Amazon CloudFront
   │
   ▼
Amazon S3 Static Website Hosting
```

A user's request is first received by Amazon CloudFront. If the requested content is already cached at an edge location, CloudFront serves it immediately. Otherwise, CloudFront retrieves the object from the Amazon S3 website endpoint, caches it, and returns it to the user.

This approach reduces latency while minimizing requests to the origin.

---

# Architecture Components

## Amazon S3

### Purpose

Amazon S3 serves as the origin for the portfolio website and stores all static assets required to render the application.

These assets include:

- HTML pages
- CSS stylesheets
- Images
- Icons
- Other static resources

Because the website does not require server-side processing or a database, Amazon S3 provides an efficient and highly durable storage solution.

### Configuration

The S3 bucket is configured with:

- Static Website Hosting enabled
- Bucket Versioning enabled
- Default Server-Side Encryption (SSE-S3) enabled
- Public read access for website objects

### Why Amazon S3?

Amazon S3 was selected because it provides:

- High durability (99.999999999%)
- High availability
- Low operational overhead
- Automatic scalability
- Cost-effective object storage
- Native support for static website hosting

---

## Amazon CloudFront

### Purpose

Amazon CloudFront functions as the Content Delivery Network (CDN) for the website.

Instead of users accessing the Amazon S3 bucket directly, requests are routed through CloudFront, which caches website content at AWS edge locations around the world.

### Responsibilities

CloudFront improves the solution by:

- Reducing latency
- Improving page load performance
- Caching frequently requested content
- Reducing requests to the S3 origin
- Providing global content distribution

### Why CloudFront?

Using CloudFront provides several advantages over accessing the S3 website endpoint directly:

- Faster content delivery
- Better user experience
- Reduced origin traffic
- Improved scalability during traffic spikes

---

## AWS Identity and Access Management (IAM)

### Purpose

AWS Identity and Access Management (IAM) was used to securely administer AWS resources during deployment.

The project was deployed using an IAM Administrator user rather than the AWS root account, following AWS security best practices for day-to-day account management.

Using IAM allows administrative access to be managed separately from the root user while supporting accountability and controlled access to AWS resources.

---

# Architectural Decisions

## Serverless Architecture

A serverless architecture was selected because the website contains only static content and does not require compute resources such as Amazon EC2 or AWS Lambda.

This decision reduces operational complexity while eliminating the need to provision, manage, or patch servers.

---

## Static Website Hosting

Amazon S3 Static Website Hosting was chosen instead of running a web server because the application consists entirely of client-side assets.

This simplifies deployment while reducing both infrastructure management and hosting costs.

---

## Bucket Versioning

Bucket Versioning was enabled to improve object durability and simplify recovery from accidental overwrites or deletions.

Maintaining previous versions of objects provides an additional layer of protection during future website updates.

---

## Server-Side Encryption

Default Server-Side Encryption (SSE-S3) was enabled to ensure that all newly uploaded objects are automatically encrypted at rest using Amazon S3 managed encryption keys.

This provides data protection without requiring additional encryption management.

---

# Security Considerations

Several security practices were incorporated into the architecture.

- Administrative tasks were performed using an IAM user instead of the AWS root account.
- Server-Side Encryption (SSE-S3) protects stored objects at rest.
- Bucket Versioning improves recoverability of website assets.
- Amazon CloudFront serves as the primary access point for website content.

Because the architecture uses the Amazon S3 static website endpoint, public read access is required for website objects.

For production environments, a more secure architecture would replace the public bucket with a private Amazon S3 bucket protected by Amazon CloudFront Origin Access Control (OAC). This enhancement has been identified as future work for the project.

---

# Scalability

The architecture automatically scales without manual intervention.

Amazon S3 is designed to store virtually unlimited objects, while Amazon CloudFront automatically scales to accommodate increases in user traffic through its globally distributed edge network.

As website traffic grows, no infrastructure changes are required to support additional users.

---

# Reliability

The architecture benefits from the reliability characteristics of managed AWS services.

Amazon S3 provides industry-leading durability for stored objects, while Bucket Versioning improves recoverability in the event of accidental modifications.

CloudFront enhances availability by distributing cached content across multiple edge locations worldwide.

---

# Cost Optimization

The solution minimizes operational costs by using fully managed services.

No virtual machines, databases, or load balancers are required, eliminating ongoing compute costs.

Charges are based primarily on object storage, data transfer, and CloudFront requests, making the solution well suited for personal portfolio websites and low-traffic applications.

---

# Summary

This architecture demonstrates a practical implementation of static website hosting using managed AWS services. By combining Amazon S3 and Amazon CloudFront, the solution delivers a scalable, reliable, and cost-effective hosting platform while incorporating additional capabilities such as object versioning, encryption at rest, and secure account administration through AWS IAM.

Although intentionally simple, the architecture reflects core cloud engineering principles and provides a strong foundation for future enhancements such as private S3 origins, Origin Access Control (OAC), custom domains, HTTPS with AWS Certificate Manager, and Infrastructure as Code (IaC).