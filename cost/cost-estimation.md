# Cost Estimation

## Overview

This document provides a high-level overview of the expected operational costs for the static portfolio website hosted on Amazon Web Services (AWS). The architecture was intentionally designed using fully managed, serverless services to minimize operational expenses while maintaining scalability, reliability, and performance.

Because the website hosts only static content, there are no continuously running compute resources such as virtual machines or containers. As a result, the solution follows a pay-for-use pricing model where charges are based primarily on storage, requests, and data transfer.

Actual costs vary depending on website traffic, object storage, and AWS pricing at the time of deployment.

---

# Cost Drivers

The overall cost of the solution is influenced by the following AWS services.

## Amazon S3

Amazon S3 charges are primarily based on:

- Amount of data stored
- Number of requests
- Data transferred out of Amazon S3 (when applicable)

For this project, storage requirements are minimal because the website consists of static assets such as HTML, CSS, images, and icons.

Since static websites typically require very little storage, Amazon S3 contributes only a small portion of the overall monthly cost.

---

## Amazon CloudFront

Amazon CloudFront pricing depends primarily on:

- Data transferred to users
- Number of HTTP and HTTPS requests

Because CloudFront caches content at AWS edge locations, repeated requests are often served directly from the cache instead of Amazon S3.

This reduces origin requests while improving website performance.

For personal portfolio websites with low to moderate traffic, CloudFront operating costs are typically very low.

---

## AWS Identity and Access Management (IAM)

AWS Identity and Access Management (IAM) is provided at no additional cost.

The IAM Administrator user used to deploy this project does not incur separate usage charges.

---

# Cost Optimization Strategies

Several architectural decisions were made to minimize operational costs.

## Serverless Architecture

The solution relies entirely on managed AWS services.

No Amazon EC2 instances, load balancers, or databases are required.

This eliminates the ongoing compute costs associated with traditional web hosting.

---

## Static Website Hosting

Hosting static content directly in Amazon S3 removes the need for application servers.

Because there is no server-side processing, infrastructure management and operational expenses remain low.

---

## CloudFront Caching

Amazon CloudFront caches frequently requested objects at edge locations.

Serving cached content reduces requests to the Amazon S3 origin while improving response times.

Caching also helps optimize data transfer between CloudFront and Amazon S3.

---

## Managed AWS Services

Both Amazon S3 and Amazon CloudFront are fully managed services.

AWS automatically handles:

- Infrastructure maintenance
- Capacity scaling
- Hardware management
- Service availability

This reduces operational overhead and eliminates the administrative costs associated with maintaining traditional web servers.

---

# AWS Free Tier Considerations

At the time this project was developed, the selected AWS services were suitable for learning, portfolio development, and low-traffic websites.

Users operating within AWS Free Tier limits may incur little or no cost depending on their account eligibility and monthly usage.

As website traffic grows beyond Free Tier allowances, charges will increase according to the current AWS pricing model.

For the latest pricing information, refer to the official AWS Pricing pages:

- Amazon S3 Pricing
- Amazon CloudFront Pricing

---

# Factors That May Increase Costs

Although the architecture is designed to be cost-efficient, operational expenses may increase under the following conditions:

- Significant growth in website traffic
- Large volumes of data transferred to users
- Frequent uploads of large media files
- Storage of multiple object versions over extended periods
- Increased CloudFront request volume

Monitoring usage regularly helps prevent unexpected charges.

---

# Cost Monitoring Recommendations

To maintain visibility into AWS spending, the following monitoring practices are recommended:

- Configure AWS Budgets to monitor monthly spending.
- Enable AWS Cost Explorer to analyze service usage.
- Review Amazon S3 storage growth periodically.
- Monitor CloudFront data transfer and request metrics.
- Remove unused objects and outdated resources when appropriate.

These practices help maintain a predictable and cost-effective cloud environment.

---

# Summary

The architecture was designed with cost optimization as a primary consideration. By combining Amazon S3 Static Website Hosting with Amazon CloudFront, the solution eliminates the need for traditional compute infrastructure while providing scalable and globally distributed content delivery.

For personal portfolio websites and other low-traffic static applications, this architecture offers an efficient balance between performance, reliability, and operational cost. As usage grows, AWS provides additional monitoring and budgeting tools that help maintain cost visibility and control.