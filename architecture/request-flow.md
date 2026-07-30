# Request Flow

## Overview

This document describes the sequence of events that occur when a user accesses the portfolio website. It explains how requests move through the AWS architecture, how Amazon CloudFront interacts with Amazon S3, and how content is delivered efficiently to the user's browser.

Understanding this request flow demonstrates how the individual AWS services work together to provide a scalable, high-performance static website hosting solution.

---

# Request Lifecycle

The following diagram illustrates the logical flow of a user request.

```text
User
   │
   ▼
Amazon CloudFront
   │
   ├───────────────┐
   │               │
Cache Hit      Cache Miss
   │               │
   ▼               ▼
Return Content  Amazon S3
                     │
                     ▼
              Retrieve Object
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

The browser sends an HTTP request to the Amazon CloudFront distribution.

---

## Step 2 – Amazon CloudFront Receives the Request

Amazon CloudFront receives the incoming request at the nearest AWS Edge Location.

Before contacting the origin, CloudFront checks whether the requested object already exists in its local cache.

This caching mechanism reduces latency and minimizes unnecessary requests to the origin.

---

## Step 3 – Cache Evaluation

CloudFront determines whether the requested object is already cached.

### Cache Hit

If the requested object is available in the cache:

- CloudFront immediately returns the object to the user's browser.
- No request is sent to Amazon S3.
- The response is delivered with very low latency.

This is the fastest possible path.

---

### Cache Miss

If the object is not available in the cache:

- CloudFront forwards the request to the Amazon S3 website endpoint.
- Amazon S3 processes the request and locates the requested object.

---

## Step 4 – Amazon S3 Returns the Object

Amazon S3 retrieves the requested file from the bucket.

Examples include:

- HTML pages
- CSS stylesheets
- Images
- Icons
- Other static website assets

The object is then returned to Amazon CloudFront.

---

## Step 5 – CloudFront Caches the Response

Before returning the object to the user, Amazon CloudFront stores a copy in its edge cache.

Future users requesting the same object can then be served directly from the cache without contacting Amazon S3 again.

This improves:

- Performance
- Scalability
- User experience

---

## Step 6 – Content is Delivered to the User

CloudFront sends the requested object back to the user's browser.

The browser downloads all required assets and renders the portfolio website.

If multiple assets are required (such as HTML, CSS, images, and icons), this process is repeated for each object.

---

# Example Request Sequence

The following example illustrates a typical request for the website's home page.

1. The user opens the website URL.
2. The browser sends a request to Amazon CloudFront.
3. CloudFront checks its cache.
4. The requested HTML page is not cached.
5. CloudFront requests the HTML page from Amazon S3.
6. Amazon S3 returns the HTML page.
7. CloudFront stores the page in its cache.
8. CloudFront returns the HTML page to the browser.
9. The browser requests additional resources such as CSS files and images.
10. CloudFront repeats the same process for each requested object.

---

# Benefits of the Request Flow

The architecture provides several operational advantages.

## Reduced Latency

Frequently requested objects are served from the nearest CloudFront edge location, reducing response times for users.

---

## Reduced Origin Load

Because CloudFront caches objects, Amazon S3 receives fewer requests.

This improves scalability while reducing the workload on the origin.

---

## Automatic Scalability

Amazon CloudFront automatically scales to accommodate increases in user traffic without requiring manual intervention.

Similarly, Amazon S3 automatically scales to store and serve large numbers of objects.

---

## Improved User Experience

By serving cached content from geographically distributed edge locations, users experience faster page load times and more consistent website performance.

---

# Cache Invalidation

When website files are updated in Amazon S3, Amazon CloudFront may continue serving older cached versions until the cache expires.

To make updates immediately available, a CloudFront cache invalidation can be performed.

Invalidation removes selected cached objects from edge locations, allowing CloudFront to retrieve the latest versions from Amazon S3 on the next request.

---

# Summary

When a user accesses the portfolio website, Amazon CloudFront acts as the entry point for all requests. Cached content is delivered directly from the nearest edge location whenever possible, while uncached content is retrieved from Amazon S3 and stored for future requests.

This request flow improves website performance, reduces latency, minimizes requests to the origin, and allows the architecture to scale efficiently without requiring traditional web servers.