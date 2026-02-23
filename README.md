# AWS Portfolio Website Deployment Architecture

## Project Overview
This project documents the architecture, design decisions, and deployment process for hosting my portfolio website on AWS using best practices from the AWS Well-Architected Framework.

The website is a static portfolio site built using HTML and CSS. The goal of this project is to deploy it securely, efficiently, and cost-effectively while documenting the entire process for learning and portfolio purposes.

This repository focuses on:
- Architecture design
- Deployment documentation
- Well-Architected compliance
- Setup screenshots
- Lessons learned

The website source code is stored in a separate repository.

---

## Project Goals
- Deploy a static portfolio website on AWS
- Follow AWS Well-Architected Framework principles
- Demonstrate cloud architecture skills
- Document deployment process step-by-step
- Provide architecture diagrams and screenshots
- Build a portfolio-ready cloud project

---

## Architecture Diagram

![Architecture Diagram](architecture-diagram/architecture.png)

---

## Architecture Overview
The architecture uses a serverless approach to host a static website with global content delivery.

### Request Flow
User → CloudFront CDN → S3 Storage → Website Response

---

