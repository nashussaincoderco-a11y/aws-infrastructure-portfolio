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




<img width="940" height="305" alt="image" src="https://github.com/user-attachments/assets/e8afbacd-7b03-4684-9b7d-460e3730ace6" />





### ALB Target group 



A grouping resource used to manage backend instances and track system stability through automated health check. 


Configured an HTTP (Port 80) target group associated with the ALB. Successfully registered backend compute instances across seperate Availability Zones enabling automated active health check to ensure traffic is only routed to operational web nodes. 




<img width="1812" height="774" alt="image" src="https://github.com/user-attachments/assets/5f352c8a-65ed-47a6-8ff6-2fe639b0ad88" />




## Instances running 


<img width="940" height="488" alt="image" src="https://github.com/user-attachments/assets/36e4a040-643a-44dc-b02d-eee2875e40e2" />




<img width="940" height="491" alt="image" src="https://github.com/user-attachments/assets/6c906202-2a3a-49f0-9750-ca8dc9a3254f" />




## Lesson learned & Troubleshooting 



### What I Learnt:



#### High Availabiity & Fault Tolerant Design 


Distributing target nodes across multiple availability zones showcases the core cloud concepts of designing for failure. It taught me a lesson of how the ALB automatically monitors target group health and moves away from anything unhealthy in the infrastructure. 



#### Automated Infrastructure 


I used the EC2 User Data to write initialization Bash Scripts and taught me the value of fixed infrastructure. I was able to orchestrate automated updates and package deployments (httpd) at the configuration phase which ensures consistent server states without manual intervention. 


### The Challenge: 


During the initial deployment testing, I attempted to connect to the public Application Load Balancer DNS endpoint but was resulting in a **"Server Not Found" / Connection Timeout** error in the browser, despite the backend targets showing as healthy.



<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/0649dea1-b602-4b19-8283-ba8c03d36152" />





### The Fix: 


I isolated the network boundary by editing the backend web server's security group inbound rules:
1. Navigated to the Security Group configuration (`Naseem-webserver-ig`).
2. Added a rule for **HTTP (Port 80)** traffic.
3. Connected the security groups together by setting the **Source** exclusively to the Application Load Balancer's specific Security Group ID (`sg-094d0a426698d6181`)




<img width="940" height="305" alt="image" src="https://github.com/user-attachments/assets/ac199291-395a-4b9b-b444-4ceff26a76c5" />




### The Result (Successful Verification): 



Saving the correct security group rule fixed the issue, allowing the load balancer to successfully toggle traffic between Web Server 1 and Web Server 2.



<img width="940" height="491" alt="image" src="https://github.com/user-attachments/assets/cc37d4a4-7701-4dce-b101-5cfc332564bc" />






