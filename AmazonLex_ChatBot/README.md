# Dental Appointment Chatbot 🦷💬

This project demonstrates how to build a **serverless chatbot** for booking dental appointments using **Amazon Lex**, **AWS Lambda**, **Cognito**, and **S3**. It showcases the integration of AWS services to create an intelligent, scalable chatbot hosted as a static website.

---

## 🛠 Features
- Conversational interface powered by **Amazon Lex**.
- Automated backend using **AWS Lambda**.
- User authentication and access control via **AWS Cognito**.
- Deployed as a static website hosted on **Amazon S3**.
- Fully responsive and styled with modern **CSS**.

---

## 🌟 Architecture Overview

1. **Amazon Lex**: A Dental Appointment Chatbot built to handle user intents like booking or canceling appointments.
2. **AWS Lambda**: A function to automate responses and manage the backend logic.
3. **AWS Cognito**: An Identity Pool for secure access and authentication.
4. **Amazon S3**: Static website hosting for the chatbot's frontend.

---

## 📜 How It Works

### Step 1: Create the Chatbot
- Built the **Dental Appointment Chatbot** in Amazon Lex.
- Defined intents like `BookAppointment`, `CancelAppointment`, and `Greeting`.
- Configured sample utterances and response messages.

### Step 2: Add a Lambda Function
- Created an **AWS Lambda** function to automate the chatbot's backend logic.
- Linked the Lambda function to Amazon Lex for dynamic responses.

### Step 3: Configure Cognito
- Created an **AWS Cognito Identity Pool** to handle secure access for the chatbot.

### Step 4: Deploy Frontend
- Developed the chatbot interface using **HTML**, **CSS**, and **JavaScript**.
- Uploaded `index.html` and `error.html` to an **Amazon S3** bucket.
- Configured S3 for **Static Website Hosting** and added bucket policies for permissions.

---

## 🖥 Setup Instructions

### Prerequisites
- AWS Account
- Basic knowledge of Amazon Lex, Lambda, Cognito, and S3.

### Deployment Steps

1. Clone the repository:
   ```bash
   git clone [https://github.com/yourusername/dental-appointment-chatbot.git](https://github.com/AmbitiousLad/AWS-Cloud-Projects.git)
   cd AmazonLex_ChatBot
