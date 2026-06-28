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


### Breakdown for what is happening in the Architecture: 

1. The Trigger: A User uses curl/Postman to send a web request ( POST ) containing data on the API Gateway
2. The Bridge: API Gateway acts as the front door by securely obtaining the request and passing it directly to AWS Lambda.
3. The Brains: AWS Lambda runs a quick script to process the incoming data and assigns it a unique ID number.
4. The Storage: Lambda automatically pushes that processed information into a DynamoDB database called students.
5. Behind the Scenes: AWS IAM ensures the code only has permission to do its specific job while CloudWatch watches for and logs any errors.




## Key Components: 


### Lambda Function

Confirmation of the API Gateway being successfully configured for the live trigger to execute the backend code within the Lambda Console. So the API Gateway is set up as the front-door trigger to execute the backend code that receives data sent from the web request, processes it by generating a unique ID number along with marking the exact current time and then saves all the formatted information directly into the database called "students".  



<img width="1550" height="410" alt="image" src="https://github.com/user-attachments/assets/9f962f31-3029-4651-b977-2279fd5abf35" />



### Lambda Function Policy 


This is the JSON code inside the security policy. I created a custom security permission policy named student-api-dynamo-write directly to the function's execution role. 


I am giving the Lambda function permission only to write data (dynamodb:PutItem) specifically into your students database table and nowhere else. 




<img width="940" height="329" alt="image" src="https://github.com/user-attachments/assets/881cd9bb-d8cf-4459-8016-4fbadf0fd531" />






This is the AWS IAM Role dashboard for my Lambda function which shows that the custom security permission policy named student-api-dynamo-write has been created and attached to the function's execution role. This allows the configuration my AWS Lambda function to have the exact security permissions it needs to talk to the database by securely connecting to the Amazon DynamoDB and save the student records into the table while blocking it out from other databases and services wihin my AWS account. 


<img width="940" height="327" alt="image" src="https://github.com/user-attachments/assets/78dda682-f592-47f6-a7a3-edfaa66c917d" />





### Lambda Function Overview 




<img width="1510" height="844" alt="image" src="https://github.com/user-attachments/assets/65fe16a1-0ace-4ad4-bd80-d758bf0ae11a" />





### Lambda Code


Below is the clean Python script deployed inside the AWS Lambda environment to handle API execution and payload ingestion:


```python
import json
import boto3
import uuid
from datetime import datetime

dynamodb = boto3.resource('dynamodb', region_name='eu-west-2')
table = dynamodb.Table('students')

def lambda_handler(event, context):
    print("Received API Gateway event: ", json.dumps(event))
    
    try:
        body = event.get('body', None)
        if body is not None:
            payload = json.loads(body) if isinstance(body, str) else body
        else:
            payload = event
            
        name = payload.get('name', 'Unknown')
        module = payload.get('module', 'AWS')
        
        student_id = str(uuid.uuid4())
        current_time = datetime.utcnow().isoformat() + 'Z'
        
        db_item = {
            'id': student_id,
            'timestamp': current_time,
            'payload': {
                'name': name,
                'module': module
            }
        }
        
        table.put_item(Item=db_item)
        
        return {
            'statusCode': 201,
            'headers': {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'
            },
            'body': json.dumps({
                'message': 'Student data successfully saved!',
                'generated_id': student_id,
                'saved_item': db_item
            })
        }
        
    except Exception as e:
        print(f"CRITICAL FAULT: {str(e)}")
        return {
            'statusCode': 500,
            'headers': {
                'Content-Type': 'application/json',
                'Access-Control-Allow-Origin': '*'
            },
            'body': json.dumps({
                'error': 'Internal Server Error',
                'error_details': str(e)
            })
        }
```




### DynamoDB 




<img width="1852" height="797" alt="image" src="https://github.com/user-attachments/assets/71c37b57-c2b0-432e-9bab-d8201f20b7eb" />




### API Gateway 





<img width="1833" height="792" alt="image" src="https://github.com/user-attachments/assets/da2e42e0-8dfe-4804-9e35-02d26f998cd7" />


