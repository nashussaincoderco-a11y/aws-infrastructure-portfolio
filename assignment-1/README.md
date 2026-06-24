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








## NAT Gateway 






<img width="940" height="457" alt="image" src="https://github.com/user-attachments/assets/0197203c-d41b-4b49-9e03-8d82a5f05180" />







<img width="1306" height="456" alt="image" src="https://github.com/user-attachments/assets/d09ae2b2-88dc-434b-8350-bdff1453daba" />










## Route Tables 




<img width="1246" height="369" alt="image" src="https://github.com/user-attachments/assets/0200ab1d-5767-4136-b8df-bdc07793285a" />






<img width="1236" height="336" alt="image" src="https://github.com/user-attachments/assets/9259f1b2-6bad-487c-973e-8f4b6defb6e0" />







<img width="1078" height="189" alt="image" src="https://github.com/user-attachments/assets/4ead494c-e993-4335-b6a0-deca61d24a96" />








<img width="1221" height="199" alt="image" src="https://github.com/user-attachments/assets/ebb480de-c282-4bcf-b418-fd2e69ed86a0" />






## Public EC2 and Private EC2 Instances 




<img width="1532" height="251" alt="image" src="https://github.com/user-attachments/assets/6b15914c-8577-49d0-bf8b-247b8915590d" />








## Instances running 



Instance running via the local terminal using SSH over the public internet using an Elastic IP address. 


<img width="1514" height="293" alt="image" src="https://github.com/user-attachments/assets/d46e4873-515e-46bf-b891-cbb88ab14a4c" />







Accessing my instance using the SSH protocol over the public internet connecting via the standard passwordless key-pair authentication. 



<img width="1020" height="462" alt="image" src="https://github.com/user-attachments/assets/6d5c8ef2-fe2a-40c2-af34-f8de08a40cca" />








## 🧠 Lessons Learned & Troubleshooting







* **What I Learnt:**

I learnt the importance of route tables and how it plays a part in network segmentation subnets. Subnets are either public or private based on how their default traffic routes are defined. 




* **The Challenge:**

After provisioning the private instance, it was completely isolated and unable to run system package updates (sudo apt update), as it lacked an outbound internet connection. 




* **The Fix:**


I updated the private subnet's route table to explicitly forward all outbound internet traffic (0.0.0.0/0) through the newly deployed NAT Gateway instead of trying to hit an Internet Gateway directly. 






## Key Takeaways

### Security - The power of data protection 


I learnt how to effectively protect data within infrastructure by placing the app instance in a private subnet with no public IP. This gave me the understanding of creating a security boundary by not exposing databases and application layers to the public internet. 



### NAT Gateway - The One-way Network Traffic Control


I was effectively able to put the NAT Gateway to action by isolating resources and ensure they can securely reach out to the internet for updates and patches. Whilst this is in process, NAT Gateeway also ensures that no other users on the internet is able to initiate a connection back into the instances to exploit it. 



### Route Tables - The traffic controllers and directors 


Configuring Route Tables gave me more control of data flow for my subnets and resources. It is what enabled me to create the public and private boundaries. For example:


*  I set a rule on the Public Subnet for any destination on 0.0.0.0/0 (the internet) to send it directly to the internet Gateway. This allows the Web Server to freely communicate back and forth with external users over the web. 
*  Whereas for the private subnet route table, I set a configuration if traffic is looking for 0.0.0.0/0 (the internet), it will direct it straight to the internal NAT Gateway. This will block hackers from getting into the App instance while allowing it to safely request outbound files or updates. 




