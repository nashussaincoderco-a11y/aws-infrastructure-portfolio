# Assignment 3: Serverless DevOps Stack - S3 Static Hosting + CloudFront CDN + Route 53 



## Overview 


### What I built: 


I built a production-ready, serverless web infrastructure that hosts a static website on Amazon S3 and accelerates it globally via an Amazon Cloudfront CDN (Content Delivery Network). 


### Why it Matters: 


This Architecture matters because it eliminates server management overhead, takes global latency through edge caching, and pushes enterprise-grade HTTPS transport security via Route 53. 


### Infrastructure impact: 


* Zero-Server Maintenance Overhead: Less manual management of server patch management, OS upgrades and running maintenance costs unlie dedicated compute instances (EC2).
* Global Content delivery - Amazon CDN brings assets directly to edge locations closest to users reducing network latancy worldwide.
* Security & Compliance - Bundling an AWS Certificate Manager SSL/TLS certificate and CloudFront pushes modern HTTPS transport security. This allows data in transit to be encrypted for browser security.
* Automated scalability that is infinite - This serverless stack scales seamlessly being able to flawlessly handle millions of simulaneous web requests without the need for complex Auto-scaling or over-provisioning infrastructure. Standard servers crash under heavy amounts of traffic requiring adjustments to the scaling.



## Architecture Diagram 



<img width="1259" height="848" alt="AWS Assignment 3 Diagram" src="https://github.com/user-attachments/assets/9e54bfa8-1599-4d1c-a647-d31d9490e0ab" />



### Request Lifecycle Breakdown: 



1. DNS Resolution: Client enters the custom domain into their browser > Amazon Route 53 processes the request via an alias A-record > The domain is directly resolved to the CDN distribution.
2. Secure Global Connection: User establishes an encrypted connection over HTTPS (Port 443) > Connect via the closes edge location > Secure transport is validated using an SSL/TLS Certificate managed by AWS certiicate manager
3. Edge Cache Optimization & Delivery: Cloudfront liaises cached assets instantly from the closest global edge location. Whenever there is a cached miss, it securely grabs the objects from the backend Amazon S3 hosting bucket.

Test
