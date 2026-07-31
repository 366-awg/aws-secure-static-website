# Cost Estimation

## Overview

This document provides a high-level overview of the operational cost considerations for the portfolio website hosted on Amazon Web Services (AWS).

The architecture was intentionally designed using fully managed services to deliver a secure, scalable, and cost-effective static website. The architecture was intentionally designed using fully managed AWS services to deliver a secure, scalable, and cost-effective static website. Amazon CloudFront distributes content globally while securely accessing a private Amazon S3 bucket through Origin Access Control (OAC), reducing operational overhead and aligning the solution with AWS security best practices.

Because the application consists entirely of static content, there are no continuously running compute resources such as Amazon EC2 instances, containers, or databases. Operational costs are therefore based primarily on storage, requests, and data transfer.

Actual costs vary depending on AWS pricing, website traffic, object storage, and geographic distribution of users.

---

# Cost Drivers

The overall cost of the solution is influenced by the following AWS services.

## Amazon S3

Amazon S3 stores the website's static assets, including HTML, CSS, JavaScript, images, and icons.

Costs are primarily influenced by:

- Amount of data stored
- Number of storage requests
- Data transferred out of Amazon S3

Since the portfolio website contains a relatively small number of static files, Amazon S3 storage costs are expected to remain minimal.

---

## Amazon CloudFront

Amazon CloudFront serves as the global content delivery network (CDN) for the website.

Pricing is primarily influenced by:

* Data transferred to users
* Number of HTTP and HTTPS requests

Because CloudFront caches frequently requested objects at AWS edge locations, many requests are served directly from the cache without contacting the Amazon S3 origin. This improves performance while reducing origin requests.

For personal portfolio websites with low to moderate traffic, CloudFront operating costs are generally low.

---

## AWS Identity and Access Management (IAM)

AWS Identity and Access Management (IAM) does not incur additional service charges.

IAM was used to securely administer AWS resources during deployment while following AWS best practices for identity and access management.

---

# Cost Optimization Strategies

The architecture incorporates several design decisions that help minimize ongoing costs.

## Static Content Delivery

Because the website consists entirely of static assets, no application servers or backend infrastructure are required.

This removes the operational costs associated with managing compute resources.

---

## Private Amazon S3 Origin

Using Amazon S3 as a private origin allows Amazon CloudFront to serve cached content efficiently while minimizing repeated origin requests.

Because frequently requested objects are delivered from CloudFront edge locations, Amazon S3 processes fewer requests, contributing to efficient resource utilization.

---

## CloudFront Edge Caching

Amazon CloudFront caches frequently requested objects at AWS edge locations.

Caching provides several benefits:

* Reduces latency
* Decreases requests to Amazon S3
* Improves scalability
* Optimizes content delivery

---

## Fully Managed Services

Both Amazon S3 and Amazon CloudFront are fully managed AWS services.

AWS automatically handles:

* Infrastructure provisioning
* Hardware maintenance
* Capacity scaling
* Service availability
* Global content delivery

This significantly reduces operational overhead compared to self-managed web servers.

---

# AWS Free Tier Considerations

This project was designed to support learning, portfolio development, and low-traffic website hosting.

Depending on AWS account eligibility and monthly usage patterns, a low-traffic portfolio website may incur little or no cost while operating within applicable AWS Free Tier or promotional usage allowances.

As website traffic increases beyond these allowances, charges are based on the current AWS pricing model.

For the latest pricing information, refer to the official AWS pricing pages for Amazon S3 and Amazon CloudFront.

---

# Factors That May Increase Costs

Operational costs may increase under the following conditions:

* Higher website traffic
* Increased data transferred to users
* Storage of additional website assets
* Long-term retention of multiple object versions
* Increased CloudFront request volume
* Frequent CloudFront cache invalidations

Regular monitoring helps maintain predictable operating costs.

---

# Cost Monitoring Recommendations

To maintain visibility into AWS spending, the following monitoring practices are recommended:

* Configure AWS Budgets to track monthly spending.
* Enable AWS Cost Explorer to analyze service usage trends.
* Monitor Amazon S3 storage growth and request activity.
* Review Amazon CloudFront request volume and data transfer metrics.
* Remove unnecessary objects and unused AWS resources when appropriate.
* Review CloudFront cache performance to maximize cache efficiency and reduce origin requests.

These practices help maintain a secure and cost-effective cloud environment.

---

# Cost Characteristics

The architecture exhibits several characteristics that contribute to its overall cost efficiency:

- No continuously running compute resources
- Fully managed AWS services
- Pay-for-use pricing model
- Automatic infrastructure scaling
- CloudFront edge caching reduces origin requests
- Minimal storage requirements for static website assets

These characteristics make the solution well suited for hosting personal portfolio websites and other low-traffic static applications.

# Summary

The architecture was intentionally designed to balance security, scalability, performance, and operational cost.

By combining Amazon CloudFront with a private Amazon S3 origin accessed through Origin Access Control (OAC), the solution securely delivers static website content while minimizing infrastructure management responsibilities.

For personal portfolio websites and other low-traffic static applications, this architecture provides a modern, highly available, and cost-efficient solution that aligns with current AWS best practices.
