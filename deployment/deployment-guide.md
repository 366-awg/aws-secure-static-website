# Deployment Guide

## Overview

This document describes the deployment process used to publish the static portfolio website on Amazon Web Services (AWS).

The deployment was performed through the AWS Management Console using managed AWS services. The process consists of configuring Amazon S3 for static website hosting, uploading the website assets, enabling additional storage features, and configuring Amazon CloudFront to distribute content globally.

---

# Deployment Prerequisites

Before deployment, the following requirements were met:

- An active AWS account
- An IAM Administrator user
- Static website files (HTML, CSS, images, and other assets)
- Basic understanding of AWS Management Console navigation

---

# Deployment Steps

## Step 1 – Create the Amazon S3 Bucket

A new Amazon S3 bucket was created to store the website assets.

The bucket name was selected to be globally unique.

---

## Step 2 – Upload Website Assets

The website files were uploaded to the bucket.

Uploaded assets included:

- HTML files
- CSS files
- Images
- Icons
- Other static resources

---

## Step 3 – Enable Static Website Hosting

Static Website Hosting was enabled for the bucket.

The following documents were configured:

- Index document: `index.html`
- Error document: `error.html`

This generated the Amazon S3 website endpoint used to serve the website.

---

## Step 4 – Configure Bucket Access

The bucket was configured to allow public read access to website objects, enabling Amazon S3 Static Website Hosting to deliver content to users.

---

## Step 5 – Enable Bucket Versioning

Bucket Versioning was enabled to preserve previous versions of uploaded objects and improve recoverability during future website updates.

---

## Step 6 – Enable Default Encryption

Default encryption was enabled using Server-Side Encryption with Amazon S3 Managed Keys (SSE-S3).

This configuration ensures that all newly uploaded objects are automatically encrypted at rest.

---

## Step 7 – Create the CloudFront Distribution

An Amazon CloudFront distribution was created using the Amazon S3 website endpoint as the origin.

CloudFront was configured to cache website content at AWS edge locations, improving website performance and reducing latency.

---

## Step 8 – Verify Website Accessibility

After deployment completed, the website was accessed through the CloudFront distribution domain to verify:

- Successful content delivery
- Correct page rendering
- Accessibility of static assets
- End-to-end functionality

---

# Post-Deployment Validation

The following checks were performed after deployment:

- Website loaded successfully through CloudFront
- Static assets rendered correctly
- Bucket Versioning was enabled
- Default encryption (SSE-S3) was enabled
- Website content was accessible from the CloudFront distribution

---

# Deployment Outcome

The completed deployment resulted in a serverless architecture capable of hosting a static website using managed AWS services.

The final solution provides:

- Global content delivery
- Automatic scalability
- Encrypted object storage
- Object versioning
- Low operational overhead
- Cost-effective static website hosting

---

# Summary

The deployment process demonstrates how Amazon S3 and Amazon CloudFront can be combined to build a scalable and efficient static website hosting solution without requiring traditional web servers.

