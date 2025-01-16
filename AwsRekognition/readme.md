# AWS Rekognition Demo Project

This README file provides step-by-step instructions for setting up a demo project using AWS Rekognition, S3, DynamoDB, and Lambda. The project demonstrates how to create a Rekognition collection, upload images to an S3 bucket with metadata, automatically store image data in DynamoDB using a Lambda function, and test face recognition with a Python script.

## Prerequisites

Before you begin, ensure you have the following:
- An AWS account
- AWS CLI configured with necessary permissions
- Python installed on your local machine
- Boto3 library installed (`pip install boto3`)
- PIL library installed (`pip install pillow`)

## Steps

### 1. Create Rekognition Collection

First, create a Rekognition collection where face data will be stored.

### 2. Create S3 Bucket
![image](https://github.com/user-attachments/assets/88948f75-878b-4a12-ac9e-109c627ecf76)
Create an S3 bucket to store images.

1. Navigate to the S3 console.
2. Click "Create bucket".
3. Follow the prompts to create a bucket (e.g., `my-face-recognition-bucket`).

### 3. Create DynamoDB Table

Create a DynamoDB table to store metadata for recognized faces.
![image](https://github.com/user-attachments/assets/787a5e00-13ca-452d-b63c-bf5f05d545f1)

1. Navigate to the DynamoDB console.
2. Click "Create table".
3. Set `Table name` to `face_recognition`.
4. Set `Primary key` to `RekognitionId` (String).

### 4. Create Lambda Function

Create a Lambda function to process images uploaded to the S3 bucket and store metadata in DynamoDB.
![image](https://github.com/user-attachments/assets/2cf60b3b-0ba7-4963-ba49-99e3396445da)

1. Navigate to the Lambda console.
2. Click "Create function".
3. Choose "Author from scratch".
4. Set `Function name` to `ImageProcessor`.
5. Choose "Create a new role with basic Lambda permissions".
6. Click "Create function".

### 5. Add S3 Trigger to Lambda
![image](https://github.com/user-attachments/assets/17c03f1d-3596-4632-a3fd-724a2e970280)

1. Navigate to your Lambda function in the AWS console.
2. Click "Add trigger".
3. Select "S3" as the trigger source.
4. Choose the bucket you created (`my-face-recognition-bucket`).
5. Set the event type to "All object create events".
6. Click "Add".

### 6. Upload Images to S3 with Metadata


Upload images to your S3 bucket with metadata using the putimages.py[make sure to change the bucketname] (e.g., `fullname`).

### 7. Test Face Recognition
The code is in testing.py
Create a script to test face recognition by uploading another image of the same person to check if the face match is working.
![image](https://github.com/user-attachments/assets/1a9cc640-dbd1-4139-ac04-23ba5dbc70c8)


### Conclusion

You have successfully set up a demo project using AWS Rekognition, S3, DynamoDB, and Lambda. This project allows you to upload images with metadata to S3, automatically store image data in DynamoDB using a Lambda function, and test face recognition with another image of the same person.

Feel free to share any feedback or improvements for this project. Happy coding!

