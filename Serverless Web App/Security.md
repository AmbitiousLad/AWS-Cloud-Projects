# Security Configuration for AWS Serverless Web Application

This document outlines the security configurations applied to the AWS Lambda function and other related services in the serverless web application project. The project involves creating a "Contact Us" form that collects user inputs and stores them in an Amazon DynamoDB table.

## AWS IAM Roles and Permissions

![Screenshot 2024-08-24 172943](https://github.com/user-attachments/assets/1e88a01d-237f-48fd-8654-7af5964e146c)


### 1. **AWSLambdaBasicExecutionRole**

#### **Purpose:**
The `AWSLambdaBasicExecutionRole` provides the necessary permissions for the Lambda function to log its execution details to Amazon CloudWatch. This is essential for monitoring and debugging the function.

#### **Permissions Granted:**
- **CloudWatch Logs:** 
  - `logs:CreateLogGroup`: Allows the creation of a new log group.
  - `logs:CreateLogStream`: Allows the creation of a new log stream.
  - `logs:PutLogEvents`: Allows the function to send log events to the log stream.

### 2. **AmazonDynamoDBFullAccess**

#### **Purpose:**
The `AmazonDynamoDBFullAccess` policy is attached to the Lambda function to allow it to perform necessary operations on the DynamoDB table where the form data is stored.

#### **Permissions Granted:**
- **DynamoDB:** 
  - Full access to create, read, update, and delete items in the DynamoDB table.

### 3. **Custom Security Practices**

#### **Principle of Least Privilege:**
- Only the essential permissions needed for the Lambda function to operate correctly are granted. This minimizes the attack surface by ensuring that the function cannot perform actions outside its intended scope.

#### **Role-Based Access Control (RBAC):**
- IAM roles are used to define what each AWS service and function can and cannot do. This ensures that security is managed centrally and that permissions are only given where necessary.

## Monitoring and Logging

### 1. **CloudWatch Monitoring:**
- The `AWSLambdaBasicExecutionRole` ensures that all Lambda execution logs are sent to CloudWatch. This allows you to monitor the function's performance and catch any potential issues early.

### 2. **Error Handling and Alerts:**
- Error handling is implemented in the Lambda function to capture exceptions and return appropriate HTTP status codes. Any significant issues can trigger alerts via CloudWatch.


By following these security practices, the project ensures that the application is secure, scalable, and reliable, leveraging the best of AWS's security features.

