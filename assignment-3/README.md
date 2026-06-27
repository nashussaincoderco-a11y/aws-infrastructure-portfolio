# Assignment 3: Serverless DevOps Stack - S3 Static Hosting + CloudFront CDN + Route 53 



## Overview 


### What I built: 


I built a production-ready, serverless web infrastructure that hosts a static website on Amazon S3 and accelerates it globally via an Amazon Cloudfront CDN (Content Delivery Network). 


### Why it Matters: 


This Architecture matters because it eliminates server management overhead, takes global latency through edge caching, and pushes enterprise-grade HTTPS transport security via Route 53. 


### Infrastructure impact: 


* Zero-Server Maintenance Overhead: Less manual management of server patch management, OS upgrades and running maintenance costs unlie dedicated compute instances (EC2).
* Global Content delivery - Amazon CDN brings assets directly to edge locations closest to users reducing network latancy worldwide.
* Security & Compliance - Utilizing Amazon CloudFront’s native SSL/TLS capabilities delivers modern HTTPS transport security out of the box, ensuring all data in transit is encrypted for browser security.
* Automated scalability that is infinite - This serverless stack scales seamlessly being able to flawlessly handle millions of simulaneous web requests without the need for complex Auto-scaling or over-provisioning infrastructure. Standard servers crash under heavy amounts of traffic requiring adjustments to the scaling.



## Architecture Diagram 



<img width="1260" height="848" alt="AWS Assignment 3 Diagram 2" src="https://github.com/user-attachments/assets/4e1dce7c-5181-4793-83e7-1a0647cae157" />




### Request Lifecycle Breakdown: 



1. DNS Resolution: Client enters the custom domain into their browser > Amazon Route 53 processes the request via an alias A-record > The domain is directly resolved to the CDN distribution.
2. Secure Global Connection: The user establishes an encrypted connection over HTTPS (Port 443) via the closest global edge location, utilizing CloudFront's default wildcard SSL/TLS certificate to secure the transport layer.
3. Edge Cache Optimization & Delivery: Cloudfront liaises cached assets instantly from the closest global edge location. Whenever there is a cached miss, it securely grabs the objects from the backend Amazon S3 hosting bucket.



## Key Components: 


### S3 Bucket

#### Amazon S3 Bucket storing the static website source files (index.html and error.html). 


<img width="1827" height="667" alt="image" src="https://github.com/user-attachments/assets/2cb71653-228a-4b52-a359-b8718b568f91" />






### Cloudfront Distribution 


#### An active Cloudfront CDN distribution configured to cache and speed up the website globally. 


<img width="1865" height="244" alt="image" src="https://github.com/user-attachments/assets/49470c65-3ece-45ab-8d02-055d9487b4c9" />




### Route 53 Records 


#### Route 53 hosted zone displaying the DNS records set up for the domain. 



<img width="1553" height="500" alt="image" src="https://github.com/user-attachments/assets/33ea97a4-a95e-46c2-bf03-6dcb7359e7fa" />



### Cloudfront Cache Invalidation 


#### A successful cache invalidation used to clear old data and instantly push website updates live. 

<img width="940" height="277" alt="image" src="https://github.com/user-attachments/assets/291f7460-8df5-4d9b-bc0a-56720de320f2" />





### Site Loading over HTTP


#### The live website loading successfully and securely over HTTPs via the Cloudfront URL. 

<img width="1310" height="679" alt="image" src="https://github.com/user-attachments/assets/fbbdd8aa-abf5-4981-90c9-809e2249217c" /> 





## 🧠 Lessons Learned & Troubleshooting



* **What I Learnt:**



I learned how to link an Amazon S3 Bucket to Cloudfront to cache my website globally, speed up loading times and automatically secure it with HTTPS. 





* **The Challenge:**



When updating the HTML source code files in the S3 Bucket, the live website failed to display the updates. This was due to CloudFront caching the old version of the site at its edge locations preventing the new changes from rendering immediately for users. 




* **The Fix:**


I created a global cache invalidation request inside the CloudFront console. This forced AWS to clear the outdated cached files from all edge locations globally and instantly fetch the freshly updated files from the S3 origin bucket. 



## What I'd do differently: 


Next time, I would buy a custom domain on a standard AWS account instead of using a restricted sandbox making the productive environment isolated. This would let me create a real custom AWS Certificate Manager certificate and use a personalized, secure HTTP web address for my site. 

