# Assignment 1: EC2 Infrastructure Deployment



## Overview 


[1-2 sentences: What did you build, and why does it matter?]


For this project, I built a multi-tier cloud network using Amazon VPC. This is an important concept in cloud computing because it requires the skill to implement real-world security practices seperating infrastructure, restricting network access and automating server provisioning. This is an IT process of setting up and configurating phyical or virtual servers to make them ready for network and cloud operations. 



## Project Summary 


### What I built: 
#### I built a full custom network where I was demonstrating the use of cloud networking, routing and segmentation all through AWS services.

These are the components that I had utilized on AWS to carry out this project: 


* A custom VPC (10.0.0.0/16)
* Public and Private Subnet
* Internet Gateway
* Created an Elastic IP
* Created a NAT Gateway in the public Subnet
* A Public Route table with a default route via the Internet Gateway
* A Private Route table with a default route via the NAT gateway
* A Public EC2 instance that would be launched in a public subnet with a public IP
* A Private EC2 instance that would be launced in a private Subnet without a public IP
* A Public EC2 Security group that will only allow SSH/HTTP only from the IP
* A Private EC2 Security group that will allow only internal access such as a public EC2 or Bastion host



## Architecture Diagrams and decisions: 



<img width="850" height="734" alt="AWS Assignment 1 diagram" src="https://github.com/user-attachments/assets/b4b13ab9-1bf1-4abc-9e5e-3be485b7a5af" />



### Breakdown of my diagram: 


1. Public internet traffic enters the custom VPC (10.0.0.0/16) via the internet gateway
2. Then it is directed by the public route table straight to the Web Server in the public subnet. 
3. To enhance security, the App instanced is completely isolated inside a private subnet with no direct public access.
4. When this private instance needs to run updates, its outbound requests travel safely through a NAT Gateway located in the public subnet
5. This grants it one-way internet communication while blocking any malicious inbound traffic from initiating a connection. 



## VPC Created: 

<img width="940" height="450" alt="image" src="https://github.com/user-attachments/assets/240dda4d-aa6f-4e1d-a0c9-230eed47ef3e" />




## Subnets 


<img width="940" height="825" alt="image" src="https://github.com/user-attachments/assets/fe82e128-be83-4974-9fdd-6ae05d54fc38" />








<img width="940" height="825" alt="image" src="https://github.com/user-attachments/assets/0bf78ee5-7892-4db8-ae4f-596298ae8cc2" />








<img width="940" height="174" alt="image" src="https://github.com/user-attachments/assets/7e5b325e-16bb-4dd8-9d0a-d2b142872e1c" />









## Internet Gateway 



<img width="940" height="425" alt="image" src="https://github.com/user-attachments/assets/d9e73fb9-3c8d-47f2-bd0e-c0110810b05e" />




## Elastic IP 

One of the mandatory fields for a NAT gateway is an Elastic IP because a static public address is required to be reserved and it is a strict configuration dependency. 





<img width="940" height="277" alt="image" src="https://github.com/user-attachments/assets/e75a9361-5bbd-4657-9708-eeefb98c66ec" />









