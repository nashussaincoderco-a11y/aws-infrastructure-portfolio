# Assignment 2: Designing a secure and scalable Compute Architecture behind Application Load Balancers




## Overview 


For this project, I built a web infrastructure that is highy available and secure. I achieved this by deploying multiple Amazon EC2 instances across different Availability Zones seperated behind an AWS Application Load Balancer (ALB). What I did to enforce strict security boundaries is isolate the applications from direct public internet access restricting inbound web traffic exclusively to requests routed through and verified by the ALB. 


### Why does this matter and the Infrastructure Impact: 


* **High Availability & Fault Tolerance:** Distributing compute workloads across independent physical Availability Zones eliminates single points of failure. If an entire data center experiences an outage, the Application Load Balancer automatically re-routes traffic to the remaining healthy instance, guaranteeing maximum system uptime.
* **Hardened Security Architecture:** By implementing the least privileges through strict AWS Security Group binding, the backend servers remain completely hidden from public scanning and unauthorized entry attempts drastically reducing the infrastructure's attack surface.
* **Seamless Scalability & Observability:** Utilizing an ALB creates a designated gateway by routing all external incoming traffic that abstracts the backend server tier. This design allows infrastructure to scale seamlessly (adding or removing instances dynamically) while actively monitoring environment stability through automated path-based health checks.



## Architecture Diagram 



<img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/9076a448-4ca9-4fc4-adc6-9dbb4c5bfe7c" />




As you can see on my diagram, the architecture creates high availabiity by distributing users requests across isolated, private EC2 instances spanning multiple Avaiability Zones managed through an Application Load Balancer. 






## What I built and Key Components 





## Instances running 





## Lesson learned & Troubleshooting 



### What I Learnt:




### The Challenge: 




### The Fix: 
