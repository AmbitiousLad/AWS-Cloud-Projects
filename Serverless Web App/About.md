

### Architecture of the Project(Serverless Web App Deployment)

![Screenshot 2024-08-24 173450](https://github.com/user-attachments/assets/d7eb49d1-b7da-4368-8fda-cc0128b16dbc)

### 🛠️ Project Overview:
I developed a "Contact Us" form that collects user inputs and stores the data in a DynamoDB table. The entire backend is powered by AWS services:

AWS Lambda: Handles the server-side logic and processes incoming requests.
Amazon API Gateway: Provides a RESTful API endpoint for the web application, ensuring secure and scalable communication.
Amazon DynamoDB: A NoSQL database that stores the form data, ensuring high availability and low latency.
### 🔒 Security:
I applied the AmazonDynamoDBFullAccess and AWSLambdaBasicExecutionRole to the Lambda function. The former allows the function to perform necessary operations on the DynamoDB table, while the latter enables it to log execution details to CloudWatch for monitoring and debugging.

### 🌐 Key Features:
Serverless Architecture: Eliminates the need for managing servers, allowing the application to scale automatically with demand.
Cost-Efficient: Only pay for what you use, with no upfront costs.
Scalable: The architecture can handle an increasing number of requests without manual intervention.
### 🛠️ Tools & Technologies:
• AWS Lambda

• Amazon API Gateway

• Amazon DynamoDB

• AWS IAM for secure role management

### 📝 Learning Outcomes:
Understanding the intricacies of serverless architecture.
Hands-on experience with AWS services, including Lambda, API Gateway, and DynamoDB.
Applying security best practices in cloud environments.
This project was an incredible learning experience and a step forward in my cloud development journey. Looking forward to applying these skills in more complex, real-world scenarios!
