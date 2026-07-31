# Deployment Guide

## Overview

This document describes the deployment process used to publish the portfolio website on Amazon Web Services (AWS). It documents the sequence of configuration steps required to provision, secure, and validate the hosting environment using fully managed AWS services.

The solution was deployed using the AWS Management Console and follows current AWS security best practices by combining Amazon CloudFront with a private Amazon S3 bucket protected by Origin Access Control (OAC). This architecture provides secure, globally distributed delivery of static website content without exposing the Amazon S3 bucket directly to the internet.

---

# Deployment Prerequisites

Before deployment, the following requirements were met:

* An active AWS account
* An IAM Administrator user
* Static website assets (HTML, CSS, JavaScript, images, icons, and other supporting files)
* Permissions to create and manage Amazon S3 and Amazon CloudFront resources

---

# Deployment Steps

## Step 1 – Create the Amazon S3 Bucket

A new Amazon S3 bucket was created to store the website assets.

The bucket name was selected to be globally unique.

---

## Step 2 – Upload Website Assets

The static website assets were uploaded to the Amazon S3 bucket, forming the origin content that would later be distributed globally through Amazon CloudFront.

Uploaded assets included:

* HTML files
* CSS stylesheets
* JavaScript files
* Images
* Icons
* Other static resources

---

## Step 3 – Configure Bucket Security

The bucket was configured using AWS security best practices.

The following settings were applied:

* Block Public Access enabled
* Bucket Owner Enforced object ownership
* Bucket Versioning enabled
* Default Server-Side Encryption (SSE-S3) enabled

These configurations help protect website assets while improving recoverability and data security.

---

## Step 4 – Create the CloudFront Distribution

An Amazon CloudFront distribution was created using the private Amazon S3 bucket as the origin.

The distribution was configured to:

* Deliver website content globally.
* Cache frequently requested objects.
* Improve website performance.
* Distribute content through AWS edge locations to reduce latency.

---

## Step 5 – Configure Origin Access Control (OAC)

Origin Access Control (OAC) was enabled to allow Amazon CloudFront to securely access the private Amazon S3 bucket.

The associated Amazon S3 bucket policy was updated to allow object access only from the authorized CloudFront distribution.

---

## Step 6 – Configure the Default Root Object

The CloudFront distribution was configured to use:

```text
index.html
```

as the default root object, ensuring users can access the website without specifying the file name.

---

## Step 7 – Verify Website Accessibility

After the CloudFront distribution finished deploying, the website was accessed through the CloudFront distribution domain.

The following items were verified:

* Successful website loading
* Correct rendering of static assets
* HTTPS connectivity
* Successful content delivery through CloudFront
* Private access to the Amazon S3 origin

---

# Post-Deployment Validation

The following validation checks were completed after deployment:

* Website successfully loaded through Amazon CloudFront.
* Static assets rendered correctly.
* Amazon S3 Block Public Access remained enabled.
* Bucket Versioning was enabled.
* Server-Side Encryption (SSE-S3) was enabled.
* Origin Access Control (OAC) was successfully configured.
* Amazon S3 remained inaccessible through direct public access.
* CloudFront successfully retrieved content from the private Amazon S3 origin.
---

# Deployment Outcome

The completed deployment resulted in a secure, serverless architecture for hosting static website content using fully managed AWS services.

The final solution provides:

* Private Amazon S3 origin
* Amazon CloudFront global distribution
* Origin Access Control (OAC)
* HTTPS content delivery
* Edge caching
* Bucket Versioning
* Server-Side Encryption (SSE-S3)
* Automatic scalability
* Low operational overhead
* Cost-effective hosting

---

# Deployment Verification Checklist

The deployment was considered successful after confirming the following:

- Amazon S3 bucket created successfully.
- Static website assets uploaded successfully.
- Block Public Access remained enabled.
- Bucket Versioning enabled.
- Server-Side Encryption (SSE-S3) enabled.
- Amazon CloudFront distribution deployed successfully.
- Origin Access Control (OAC) configured correctly.
- Bucket policy restricted direct access to Amazon S3.
- Website accessible through the CloudFront distribution domain.
- Website content delivered securely over HTTPS.

# Summary

The deployment process demonstrates how Amazon CloudFront and a private Amazon S3 bucket can be combined to build a secure, scalable, and highly available static website hosting solution.

By using Origin Access Control (OAC), the architecture eliminates direct public access to Amazon S3 while allowing CloudFront to securely retrieve and deliver website content. This approach aligns with current AWS best practices for hosting static websites in production environments.
