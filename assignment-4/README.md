# Assignment 4 - AWS, API Gateway, Lambda- DynamoDB 



##  Overview


### What I built: 

For this project, I built a Serverless REST API that securely accepts user requests, processes data using a cloud function and saves the information into a database. The REST API is what allows two different applications to communicate with other over the internet using standard web rules (HTTP). It enables a website or app to send a request over te internet and then cleanly delivers that data to a server or database. 


### Why it matters: 

This project is an important concept in DevOps and Cloud Architecture. Serverless Architecture is how modern tech organizations build fast, scalable apps removing the need and cost to manage traditional servers. Here are some of the benefits and usages: 


* Cost effective & Scalable: The entire system only runs when needed so it automatically scales to handle millions of users while costing practically nothing when not in use (Idle).
* Standard operating procedure : Combining API Gateway, Lambda and DynamoDB is the conventional AWS trio used almost everywhere in the cloud industry.
* Secure by design: Write secure cloud code by giving your app the exact permissions only it needs to stay away from hackers. 


### Infrastructure Impact: 


* No server management - Because it is serveress, there is no need to manage a virtual server with it's patches and updates. AWS does all the heavy lifting by handling all the underlying hardware automatically.
* You only pay for what you use - With the setup of DynamoDB, Lambda, API Gateway & IAM Permissions, you only pay the exact milliseconds the code runs when a user submits data. Unlike tradtional servers, it costs money even when they are not in use.
* Instant Scaling - If 5 to 50,000 users access the API at the exact time, the infrastructure automatically spins up resources to handle the traffic spike without crashing.
* Immense Security Boundaries - By utilizing IAM minimal-privilege, the infrastructure is locked down so the code can only write to its specific database table and nothing else which prevents widespread security breaches.



  ## Architecture Diagram:


  
<img width="1152" height="918" alt="AWS Assignment 4 diagram" src="https://github.com/user-attachments/assets/82c56f78-8a91-4f66-a5e9-c5b66b634a02" />

