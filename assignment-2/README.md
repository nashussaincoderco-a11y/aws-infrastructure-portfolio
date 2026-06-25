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

Here is a list of the key components and a breakdown of what they are and there function within the architecture: 


### 2x Amazon EC2 instances - Compute Nodes running Amazon Linux 2023 to serve web content


<img width="1666" height="853" alt="image" src="https://github.com/user-attachments/assets/70602e07-55bb-48a2-91f9-1ce7a4e54226" />




<img width="1676" height="731" alt="image" src="https://github.com/user-attachments/assets/2be040cc-584c-4ff4-9fb3-9abcd9f4f95b" />



#### User Data for instances

Both instances were bootstrapped automatically on boot using custom User Data bash scripts to display unique landing pages. 




<img width="940" height="443" alt="image" src="https://github.com/user-attachments/assets/b0cddb77-0cdd-4d85-92da-85b591f5814e" />




### AWS Application Load Balancer (ALB) 


Load balancing service that distributes across the two public subnets to manage, route and balance incoming traffic 



<img width="940" height="454" alt="image" src="https://github.com/user-attachments/assets/66dea220-6838-4b00-aeec-0f7c6f4def98" />



### Multi-AZ Architecture - 2x public subnets and 1x private subnet


Multi-Availability Zone design (AZ1 & AZ2) to achieve high availability and data center fault tolerance. Integrated to dual public subnets to host the public-facing ALB, while isolating compute workloads inside a private subnet to prevent direct public internet exposure. Fully isolated network boundaries that host the EC2 web servers away from direct public internet exposure 




<img width="1638" height="102" alt="image" src="https://github.com/user-attachments/assets/ef888800-733f-4b8e-a6da-eb99c321b91c" />





### 1x Internet Gateway  


The edge component allowing the VPC to communicate with the outside world. 



<img width="1865" height="449" alt="image" src="https://github.com/user-attachments/assets/bc4f36c8-c5c2-4537-a2da-44ba98f85751" />



### AWS Security groups  


Virtual firewalls that are linked implementing strict isolation rules so the servers only accept traffic explicitly forwarded by the ALB. Configured HTTP (Port 80) to accept traffic from the Application Load Balancer's security group while restricting SSH (Port 22) administrative access to a single authorized IP address. 


<img width="1792" height="505" alt="image" src="https://github.com/user-attachments/assets/52d8f653-34de-488c-8aa9-11da635033a2" />




* ** ALB Target group - A grouping resource used to manage backend instances and track system stability through automated health check. 



## Instances running 





## Lesson learned & Troubleshooting 



### What I Learnt:




### The Challenge: 




### The Fix: 
