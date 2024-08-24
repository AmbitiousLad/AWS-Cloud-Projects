# AWS API Gateway Configuration for Serverless Web Application

This document provides an overview of the API Gateway configuration used in the serverless web application project, which processes HTTP requests and triggers Lambda functions for form data submission to DynamoDB.

## Overview

Amazon API Gateway acts as the entry point for your serverless application, routing HTTP requests to the appropriate backend services. In this project, API Gateway is configured to handle GET and POST requests, forwarding them to an AWS Lambda function for processing.


### Key Features:
- **RESTful API Interface**: Allows HTTP methods such as GET and POST to interact with backend services.
- **Integration with AWS Lambda**: Routes incoming HTTP requests directly to the Lambda function for execution.
- **Customizable Security and Throttling**: Supports API keys, authorizers, and request throttling to manage access and protect resources.

## API Gateway Configuration

### 1. **API Gateway Setup**
![Screenshot 2024-08-24 173120](https://github.com/user-attachments/assets/68d061e1-0cd2-4042-b12d-6ae457ac238e)
#### **Create a REST API**
- **API Type**: Choose REST API.
- **API Name**: Provide a meaningful name for the API (e.g., `ContactFormAPI`).
- **Endpoint Type**: Select Regional or Edge-Optimized based on your application's needs.

#### **Define Resources and Methods**
![Screenshot 2024-08-24 173128](https://github.com/user-attachments/assets/28ba6d58-7a00-4b7b-bec5-f0772d5e6d8e)


- **Root Resource `/`**: Serves as the base path for the API.
  - **GET Method**: Returns the HTML content of the "Contact Us" page.
   ![Screenshot 2024-08-24 173153](https://github.com/user-attachments/assets/d1c44682-7998-4663-948e-763a68bfa643)

  
  - **POST Method**: Submits form data to the backend for processing.
 
   ![Screenshot 2024-08-24 173206](https://github.com/user-attachments/assets/f848010f-000c-4f5b-a2eb-dc3c13cf8f93)

    

### 2. **Integration with AWS Lambda**

#### **Lambda Proxy Integration**
- **Enable Lambda Proxy Integration**: This option allows the entire HTTP request to be passed as a single event to the Lambda function, which processes it and returns the response.
- **Lambda Function Name**: Select the Lambda function created for handling form submissions.
- **Execution Role**: Ensure that the Lambda function has the necessary IAM role with `AWSLambdaBasicExecutionRole` and `AmazonDynamoDBFullAccess` permissions.
![Screenshot 2024-08-24 173235](https://github.com/user-attachments/assets/63b024e7-3e9a-41d7-b67c-e82d4976751d)

### 3. **Method Request and Response**

#### **Request Validation**
- **Content-Type Headers**: Ensure that the `Content-Type` header for POST requests is set to `application/x-www-form-urlencoded` if form data is being submitted.
- **Request Parameters**: Optionally, you can define request parameters that must be included in the query string or headers.

#### **Response Integration**
- **Default Response**: Configure the API Gateway to return a default HTML response or JSON payload based on the Lambda function's output.
- **Error Handling**: Map specific error codes from the Lambda function to HTTP status codes (e.g., 400 for bad requests, 500 for server errors).

### 4. **Security and Access Control**

#### **API Keys and Usage Plans**
- **API Keys**: Optionally create API keys to restrict access to the API.
- **Usage Plans**: Define usage plans that set throttling limits (requests per second) and quota limits (requests per month).

### 5. **Deployment**

#### **Create a Deployment Stage**
- **Stage Name**: Create a deployment stage (e.g., `prod`, `dev`).
- **Stage Variables**: Use stage variables to configure different environments without changing the API configuration.
- **Invoke URL**: The URL generated for the API endpoint will be used to invoke the API Gateway from the frontend or testing tools.


### 2. **Security Considerations**
Always enable HTTPS for your API Gateway to ensure secure communication. Consider integrating AWS WAF (Web Application Firewall) for additional security measures.

### 3. **Optimize for Cost**
Review API Gateway pricing, especially for high-traffic APIs, and consider using caching or deploying Lambda@Edge for cost optimization.

---

This documentation outlines the essential aspects of configuring and deploying an API Gateway for your serverless web application. By following these guidelines, you can ensure that your API is secure, efficient, and scalable.
