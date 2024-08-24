# AWS Lambda Configuration for Serverless Web Application

This document provides an overview of the AWS Lambda function utilized in the serverless web application project, which processes form data from an API Gateway and stores it in DynamoDB.

## Overview

The AWS Lambda function is a core component of the serverless architecture, responsible for executing backend logic in response to HTTP requests sent via API Gateway. In this project, the Lambda function handles both GET and POST requests to manage the "Contact Us" form submissions.


![Screenshot 2024-08-24 173010](https://github.com/user-attachments/assets/aae0d014-95fb-4975-b3df-0180f41891f7)


![Screenshot 2024-08-24 173023](https://github.com/user-attachments/assets/8395551a-29d8-414f-b1a4-0bc0e1ce43f5)


### Key Features:
- **Event-Driven Execution**: The Lambda function is triggered by API Gateway events.
- **Stateless Processing**: Each invocation of the Lambda function is independent, allowing for scalable, distributed processing.
- **Integrated with DynamoDB**: The function reads and writes data to DynamoDB based on incoming requests.

## Configuration Details

### 1. **Function Trigger**
The Lambda function is triggered by an API Gateway, which routes HTTP requests to the function. The API Gateway is configured to handle both GET and POST methods, sending the corresponding event payload to the Lambda function.

### 2. **IAM Roles and Permissions**
The Lambda function is assigned an IAM role with specific permissions:

- **AWSLambdaBasicExecutionRole**: 
  - Provides permissions to write logs to CloudWatch, enabling monitoring and debugging.
  
- **AmazonDynamoDBFullAccess**:
  - Grants the function full access to the DynamoDB table used to store the form data.

### 3. **Function Code**
The function is written in Python and processes both GET and POST requests:

- **GET Request Handling**:
  - Returns the HTML content of the "Contact Us" page.

- **POST Request Handling**:
  - Extracts form data from the incoming request, formats it, and inserts it into the DynamoDB table.
  
lambda_function.py Code Snippet:
```python
import json
import os
import boto3

def lambda_handler(event, context):
    try:
        mypage = page_router(event['httpMethod'], event['queryStringParameters'], event['body'])
        return mypage
    except Exception as e:
        return {
            'statusCode': 500,
            'body': json.dumps({'error': str(e)})
        }

def page_router(httpmethod, querystring, formbody):
    if httpmethod == 'GET':
        try:
            with open('contactus.html', 'r') as htmlFile:
                htmlContent = htmlFile.read()
            return {
                'statusCode': 200,
                'headers': {"Content-Type": "text/html"},
                'body': htmlContent
            }
        except Exception as e:
            return {
                'statusCode': 500,
                'body': json.dumps({'error': str(e)})
            }

    elif httpmethod == 'POST':
        try:
            insert_record(formbody)
            with open('success.html', 'r') as htmlFile:
                htmlContent = htmlFile.read()
            return {
                'statusCode': 200,
                'headers': {"Content-Type": "text/html"},
                'body': htmlContent
            }
        except Exception as e:
            return {
                'statusCode': 500,
                'body': json.dumps({'error': str(e)})
            }

def insert_record(formbody):
    formbody = formbody.replace("=", "' : '")
    formbody = formbody.replace("&", "', '")
    formbody = "INSERT INTO serverlessTable value {'" + formbody + "'}"

    client = boto3.client('dynamodb')
    response = client.execute_statement(Statement=formbody)
    # Assuming the execute_statement call returns successfully
    return response
```
Contactus.html Code Snippet(Used for GET Method):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact Form</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      height: 100vh;
    }

    form {
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s ease-in-out;
    }

    h2 {
      text-align: center;
      color: #333;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin: 10px 0 5px;
      color: #555;
    }

    input,
    textarea {
      width: 100%;
      padding: 10px;
      margin-bottom: 10px;
      box-sizing: border-box;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    input[type="submit"] {
      background-color: #4caf50;
      color: #fff;
      cursor: pointer;
      font-size: 16px; /* Increased text size for submit button */
    }

    input[type="submit"]:hover {
      background-color: #45a049;
    }

    /* Additional styles for animation */
    form:hover {
      transform: scale(1.05);
    }

    /* Additional styles for footer */
    footer {
      margin-top: 20px;
      font-size: 18px;
      text-align: center;
    }
  </style>
</head>
<body>

  <h2>Welcome to my AWS Project Task</h2>

  <form action="/dev" method="post">
    <h2>Contact Us</h2>
    <label for="fname">First Name:</label>
    <input type="text" id="fname" name="fname" required>

    <label for="lname">Last Name:</label>
    <input type="text" id="lname" name="lname" required>

    <label for="email">Email ID:</label>
    <input type="text" id="email" name="email" required>

    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="4" cols="50" required></textarea>

    <input type="submit" value="Submit">
  </form>

  <footer>
    An AWS Project by Avinash Reddy Thipparthi
  </footer>

  <!-- Simple JavaScript for animation -->
  <script>
    const form = document.querySelector('form');

    form.addEventListener('mouseover', () => {
      form.style.transform = 'scale(1.05)';
    });

    form.addEventListener('mouseout', () => {
      form.style.transform = 'scale(1)';
    });
  </script>

</body>
</html>
```

Success.html Code Snippet(Used for POST Method):
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Thank You</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    h2 {
      text-align: center;
      color: #333;
      padding: 20px;
      background-color: #fff;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      opacity: 0;
      transform: translateY(20px);
      transition: opacity 0.5s ease-in-out, transform 0.5s ease-in-out;
    }

    /* Additional styles for animation */
    .visible {
      opacity: 1;
      transform: translateY(0);
    }
  </style>
</head>
<body>

  <h2 id="thankYouMessage">Thanks for trying this Project. you can verify data in DynamoDB Table.</h2>

  <!-- Simple JavaScript for animation -->
  <script>
    const thankYouMessage = document.getElementById('thankYouMessage');

    // Adding a delay before showing the message
    setTimeout(() => {
      thankYouMessage.classList.add('visible');
    }, 500);
  </script>

</body>
</html>
```
