# AWS DynamoDB Configuration for Serverless Web Application

This document provides an overview of the DynamoDB configuration used in the serverless web application project, which stores form data submitted through an API Gateway and processed by AWS Lambda.

## Overview

Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. In this project, DynamoDB is used to store form submissions from a "Contact Us" page, which are processed and saved by a Lambda function.

![Screenshot 2024-08-24 173039](https://github.com/user-attachments/assets/141d32f2-81aa-48ea-afcb-d371d3737820)


### Key Features:
- **NoSQL Database**: DynamoDB supports flexible data models, allowing you to store and retrieve structured and semi-structured data.
- **Serverless Integration**: Seamlessly integrates with AWS Lambda and API Gateway for serverless applications.
- **Automatic Scaling**: DynamoDB automatically scales to handle your application's throughput and storage requirements.

## DynamoDB Table Configuration

### 1. **Table Creation**

#### **Table Name**
- **Table Name**: Choose a meaningful name for your table, such as `serverlessTable`.

#### **Primary Key**
- **Partition Key**: Use a unique identifier for each submission, such as `email` (String).

#### **Attributes**
- **email**: A unique string identifier for each form submission.
- **fname**: The first name of the submitter.
- **lname**: The last name of the submitter.
- **Message**: The message content submitted through the form.

  
![Screenshot 2024-08-24 173103](https://github.com/user-attachments/assets/d1f5e9f7-6b69-41d6-86f1-1c90dcb6eda7)


### 2. **Provisioned Capacity**
- **Read Capacity Units**: Set based on your application's read requirements.
- **Write Capacity Units**: Set based on your application's write requirements.
- **Auto Scaling**: Enable Auto Scaling to automatically adjust capacity based on demand.

## Lambda Function Integration

### 1. **IAM Role Configuration**
- **Role Permissions**: The Lambda function that interacts with DynamoDB should have the following permissions:
  - **AmazonDynamoDBFullAccess**: To perform all CRUD (Create, Read, Update, Delete) operations on the DynamoDB table.
  - **AWSLambdaBasicExecutionRole**: To allow the Lambda function to write logs to CloudWatch.

### 2. **Insert Data into DynamoDB**
- **Data Insertion**: The Lambda function parses the incoming form data and inserts a new item into the DynamoDB table.
- **Error Handling**: Ensure that the Lambda function includes error handling logic to manage potential issues during data insertion.

### 3. **Querying DynamoDB**
- **Data Retrieval**: The Lambda function can also query DynamoDB to retrieve form submissions, if needed, for additional processing or reporting.

## Best Practices

### 1. **Data Security**
- **IAM Policies**: Use least privilege principles when assigning IAM roles and policies to your Lambda functions and users.

### 2. **Performance Optimization**
- **Indexing**: Use appropriate indexes (GSI, LSI) to optimize query performance.
- **Batch Operations**: For bulk operations, use DynamoDB's batch write and batch get operations to reduce the number of API calls.


This documentation outlines the essential aspects of configuring and using DynamoDB in your serverless web application. By following these guidelines, you can ensure that your data is securely stored, efficiently accessed, and scalable to meet your application's needs.
