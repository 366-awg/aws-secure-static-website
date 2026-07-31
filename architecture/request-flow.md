# Request Flow

## Overview

This document describes the lifecycle of a user request as it travels through the AWS architecture. It explains how Amazon CloudFront processes incoming requests, serves cached content from edge locations, securely retrieves objects from a private Amazon S3 bucket using Origin Access Control (OAC) when necessary, and delivers the website to end users.

Understanding this request flow demonstrates how the individual AWS services work together to provide a secure, scalable, and high-performance static website hosting solution.

---

# Request Lifecycle

The following diagram illustrates the logical flow of a user request.

```text
                User
                  │
                  ▼
      Amazon CloudFront
                  │
          Cache Hit / Miss
                  │
         ┌────────┴────────┐
         │                 │
    Cache Hit         Cache Miss
         │                 │
         ▼                 ▼
 Return Cached      Authenticated Origin Request
    Content         (Origin Access Control)
                           │
                           ▼
                 Private Amazon S3 Bucket
                           │
                           ▼
                  Retrieve Requested Object
                           │
                           ▼
            Cache Object in CloudFront
                           │
                           ▼
                 Return Content to User
```

---

# Step-by-Step Request Flow

## Step 1 – User Requests the Website

A user enters the website URL into their browser or clicks a link to the portfolio website.

The browser sends an HTTPS request to the Amazon CloudFront distribution.

---

## Step 2 – Amazon CloudFront Receives the Request

Amazon CloudFront receives the request at the nearest AWS Edge Location.

CloudFront checks whether the requested object is already stored in its cache.

Serving cached content from edge locations reduces latency and improves website performance.

---

## Step 3 – Cache Evaluation

CloudFront determines whether the requested object already exists in its cache.

### Cache Hit

If the object is already cached:

* CloudFront immediately returns the object to the user's browser.
* No request is sent to the Amazon S3 origin.
* The response is delivered with minimal latency.

This provides the fastest possible user experience.

---

### Cache Miss

If the object is not cached:

* CloudFront forwards a signed request to the private Amazon S3 bucket.
* The request is authenticated using Origin Access Control (OAC).
* If the object is not cached:

- CloudFront forwards an authenticated request to the private Amazon S3 bucket.
- Origin Access Control (OAC) authorizes CloudFront to retrieve the requested object.
- Amazon S3 returns the object to CloudFront.

---

## Step 4 – Amazon S3 Returns the Object

Amazon S3 retrieves the requested object and returns it to Amazon CloudFront.

Examples include:

- HTML pages
- CSS files
- JavaScript files
- Images
- Icons
- Other static website assets

---

## Step 5 – CloudFront Caches the Object

Before sending the response to the user, CloudFront stores the object in its edge cache.

Future requests for the same object can be served directly from the cache without contacting Amazon S3.

This reduces origin requests and improves response times.

---

## Step 6 – Content is Delivered to the User

CloudFront returns the requested object to the user's browser.

The browser downloads any additional assets required to render the website, such as CSS, JavaScript, images, and icons.

Each subsequent request follows the same cache evaluation process.

---

# Security Flow

The architecture incorporates several AWS security best practices.

1. Users cannot access the S3 bucket directly.
2. CloudFront is the only service permitted to retrieve objects from the bucket.
3. CloudFront authenticates origin requests using Origin Access Control (OAC).
4. The Amazon S3 bucket policy validates that requests originate only from the authorized CloudFront distribution.
5. Website content is delivered securely over HTTPS.

---

# Example Request Sequence

The following example illustrates a request for the website home page.

1. A user enters the website URL.
2. The browser sends an HTTPS request to Amazon CloudFront.
3. CloudFront checks its edge cache.
4. The requested page is not found in the cache.
5. CloudFront signs the origin request using Origin Access Control.
6. Amazon S3 validates the signed request.
7. Amazon S3 returns the requested object.
8. CloudFront stores the object in its cache.
9. CloudFront returns the object to the user's browser.
10. Future requests for the same object are served directly from CloudFront until the cached object expires or is invalidated.

---

# Benefits of the Request Flow

## Improved Security

The Amazon S3 bucket remains private and is not directly accessible from the internet.

Only the authorized Amazon CloudFront distribution can retrieve objects through Origin Access Control.

---

## Reduced Latency

Frequently requested content is served from the nearest CloudFront edge location, reducing response times for users worldwide.

---

## Reduced Origin Load

CloudFront caches frequently requested objects, significantly reducing the number of requests sent to Amazon S3.

---

## Automatic Scalability

Amazon CloudFront and Amazon S3 automatically scale to support increasing traffic without requiring manual infrastructure management.

---

## Improved User Experience

By combining global edge caching with secure origin access, users experience faster page loads while benefiting from a more secure architecture.

---

# Cache Invalidation

When website files are updated in Amazon S3, CloudFront may continue serving cached versions until the configured cache lifetime expires.

To make updated content available immediately, a CloudFront cache invalidation can be created. This removes cached objects from edge locations, allowing CloudFront to retrieve the latest versions from Amazon S3 during the next request.

---

# Request Flow Characteristics

The request flow reflects several key architectural characteristics of the solution:

- CloudFront acts as the single public entry point.
- Amazon S3 functions as a private origin for static website assets.
- Origin Access Control (OAC) restricts direct access to the S3 bucket.
- Frequently requested content is cached at AWS edge locations.
- Managed AWS services automatically scale to accommodate changes in traffic without requiring infrastructure management.

# Summary

Amazon CloudFront serves as the public entry point for all website requests, delivering cached content from AWS edge locations whenever possible. When an object is not available in the cache, CloudFront securely retrieves it from the private Amazon S3 origin using Origin Access Control (OAC), caches the response, and returns it to the user.

This request flow combines low latency, automatic scalability, and strong origin protection, ensuring that website content is delivered efficiently while preventing direct public access to the Amazon S3 bucket.
