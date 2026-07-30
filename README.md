<p align="center">
  <h1 align="center">
      AWS Static Portfolio Website Hosting Architecture
  </h1>

  <p align="center">
      A production-inspired serverless static website hosted on Amazon Web Services using Amazon S3 and Amazon CloudFront.
  </p>
</p>

# AWS Static Portfolio Website Hosting Architecture

> A serverless static website hosting solution built on Amazon Web Services (AWS) using Amazon S3 and Amazon CloudFront, with detailed architecture documentation and deployment guidance.

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)

![Amazon S3](https://img.shields.io/badge/Amazon-S3-red)

![CloudFront](https://img.shields.io/badge/Amazon-CloudFront-blue)

![HTML](https://img.shields.io/badge/HTML-5-orange)

![CSS](https://img.shields.io/badge/CSS-3-blue)

![License](https://img.shields.io/badge/License-MIT-green)

![Status](https://img.shields.io/badge/Status-Completed-success)

## Table of Contents

- [Project Overview](#project-overview)
- [Project Objectives](#project-objectives)
- [Solution Architecture](#solution-architecture)
- [Architecture Diagram](#architecture-diagram)
- [Architecture Overview](#architecture-overview)
- [Request Flow](#request-flow)
- [AWS Services Used](#aws-services-used)
- [Key Features](#key-features)
- [Repository Structure](#repository-structure)
- [Documentation](#documentation)
- [AWS Well-Architected Framework Alignment](#aws-well-architected-framework-alignment)
- [Screenshots](#screenshots)
- [Lessons Learned](#lessons-learned)
- [Future Improvements](#future-improvements)
- [Author](#author)
- [License](#license)

## Project Overview

This project demonstrates the design and deployment of a static portfolio website on Amazon Web Services (AWS) using a serverless architecture. The solution leverages Amazon Simple Storage Service (Amazon S3) for static website hosting and Amazon CloudFront as a Content Delivery Network (CDN) to deliver website content with improved performance and reduced latency.

The project was developed to gain hands-on experience with AWS cloud services while applying architectural best practices for static website hosting. In addition to deploying the website, this repository documents the architecture, deployment process, design decisions, security enhancements, cost optimization strategies, and lessons learned throughout the implementation.

The solution incorporates Amazon S3 Versioning to improve data resilience and Server-Side Encryption using Amazon S3 managed keys (SSE-S3) to automatically encrypt objects at rest. These enhancements improve the reliability and security of the storage layer while maintaining a cost-effective, serverless architecture.

This repository serves as both technical documentation and a portfolio project demonstrating foundational AWS cloud architecture concepts.

---

## Project Objectives

The objectives of this project were to:

- Design and deploy a static portfolio website using AWS managed services.
- Gain practical experience with Amazon S3 static website hosting.
- Improve website performance using Amazon CloudFront.
- Apply selected AWS Well-Architected Framework principles.
- Implement object versioning for improved data protection.
- Protect stored objects using Server-Side Encryption (SSE-S3).
- Document the deployment process in a structured and reproducible manner.
- Build a professional cloud portfolio project demonstrating practical AWS skills.

---

# Solution Architecture

The solution uses a fully managed, serverless architecture for hosting static web content.

When a user requests the website, the request is routed through Amazon CloudFront. CloudFront retrieves website content stored in Amazon S3 and caches it at AWS edge locations to reduce latency for future requests.

The website consists entirely of static assets including HTML, CSS, images, and other client-side resources, eliminating the need for application servers or databases.

---

## Architecture Diagram

<p align="center">
  <img src="architecture/architecture.png" alt="AWS Architecture Diagram" width="900">
</p>

---

## Architecture Overview

The architecture consists of the following AWS services:

### Amazon S3

Amazon S3 serves as the origin for the static website and stores all website assets including:

- HTML files
- CSS stylesheets
- Images
- Static resources

The bucket has:

- Static Website Hosting enabled
- Bucket Versioning enabled
- Default Server-Side Encryption (SSE-S3) enabled
- Public read access configured to support static website hosting

---

### Amazon CloudFront

Amazon CloudFront provides global content delivery by caching website content at AWS edge locations.

Its responsibilities include:

- Faster content delivery
- Reduced latency
- Improved user experience
- Reduced load on the S3 origin
- Global content distribution

---

### AWS Identity and Access Management (IAM)

The project was deployed using an AWS IAM Administrator user following AWS security best practices by avoiding use of the root account for everyday administrative tasks.

---

## Request Flow

The following sequence describes how users access the hosted website:

1. A user enters the website URL.
2. The request is received by Amazon CloudFront.
3. CloudFront checks whether the requested content is available in its cache.
4. If the content is cached, CloudFront immediately returns the response.
5. If the content is not cached, CloudFront retrieves the requested object from the Amazon S3 website endpoint.
6. Amazon S3 returns the requested object.
7. CloudFront caches the object for future requests.
8. CloudFront returns the website content to the user.

---

# AWS Services Used

| AWS Service | Role in the Architecture |
|-------------|---------|
| Amazon S3 | Stores and hosts the static website files. |
| Amazon CloudFront | Delivers website content globally with edge caching. |
| AWS IAM | Provides secure administrative access to AWS resources. |

---

# Key Features

- Static website hosting using Amazon S3
- Global content delivery using Amazon CloudFront
- Fully serverless architecture
- Amazon S3 Versioning enabled
- Server-Side Encryption (SSE-S3) enabled
- Low operational overhead
- Cost-effective hosting solution
- Deployment using AWS Management Console
- Comprehensive project documentation

---

# Repository Structure

```
aws-static-portfolio-hosting/
│
├── architecture/
│   ├── architecture.png               # Solution architecture diagram
│   ├── architecture-description.md    # Architecture explanation
│   └── request-flow.md                # Request lifecycle
│
├── deployment/
│   ├── deployment-guide.md            # Deployment steps
│   ├── aws-services-used.md           # Service descriptions
│   └── configuration.md               # Configuration details
│
├── security/
│   └── security.md                    # Security controls
│
├── cost/
│   └── cost-estimation.md             # Cost optimization
│
├── screenshots/
│
├── README.md
├── LICENSE
└── .gitignore
```

---

# Documentation

This repository contains detailed technical documentation for each aspect of the project.

| Document | Description |
|----------|-------------|
| Architecture Description | Explains each architectural component |
| Request Flow | Describes how requests travel through the architecture |
| Deployment Guide | Step-by-step deployment instructions |
| AWS Services Used | Overview of AWS services and their responsibilities |
| Configuration | Key AWS configuration decisions |
| Security | Security controls and implementation details |
| Cost Estimation | Cost considerations and optimization |
| Lessons Learned | Technical insights gained during the project |

---

# AWS Well-Architected Framework Alignment

| Pillar | Implementation |
|---------|---------------|
| Operational Excellence | Structured documentation and repeatable deployment process |
| Security | IAM administration, Server-Side Encryption (SSE-S3), AWS managed services |
| Reliability | Amazon S3 durability, Versioning, CloudFront global infrastructure |
| Performance Efficiency | CloudFront edge caching for low-latency content delivery |
| Cost Optimization | Fully serverless architecture with managed AWS services |
| Sustainability | Efficient resource utilization through managed cloud infrastructure |

---

# Screenshots

The repository includes screenshots documenting the deployment process, including:

- Amazon S3 bucket configuration
- Static Website Hosting configuration
- Bucket Versioning
- Server-Side Encryption settings
- CloudFront distribution
- Live portfolio website

---

# Lessons Learned

This project provided practical experience in designing and deploying a serverless static website architecture on AWS.

Key lessons included:

- Configuring Amazon S3 for static website hosting.
- Using Amazon CloudFront to improve website performance.
- Understanding the importance of Versioning for data recovery.
- Implementing encryption at rest using SSE-S3.
- Applying AWS security best practices during deployment.
- Documenting cloud architecture in a professional and reproducible manner.

---

## Future Improvements

- [ ] Migrate to Origin Access Control (OAC)
- [ ] Configure a private Amazon S3 bucket
- [ ] Register a custom domain using Amazon Route 53
- [ ] Add HTTPS using AWS Certificate Manager (ACM)
- [ ] Automate deployment using Terraform
- [ ] Build CI/CD with GitHub Actions
- [ ] Implement AWS CloudWatch monitoring
- [ ] Protect the application using AWS WAF

---

# Author

**Ann Githinji**

AWS Certified Cloud Practitioner

AWS Certified Solutions Architect – Associate

Cloud Solutions | AWS | Cloud Security | Infrastructure | Automation

---

# License

This project is licensed under the MIT License. See the `LICENSE` file for more information.