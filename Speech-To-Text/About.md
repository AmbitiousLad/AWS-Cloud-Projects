# Speech to Text Conversion Using Python, Amazon S3, and Amazon Transcribe

This guide outlines the steps to convert speech to text using a Python script, Amazon S3 for storage, and Amazon Transcribe for transcription. The process involves uploading an MP3 file to an S3 bucket, fetching the file using its URL in a Python script, configuring AWS credentials, and using Amazon Transcribe to process the audio file.

## Prerequisites

Before you begin, ensure you have the following:

1. **AWS Account**: An active AWS account with the necessary permissions.
2. **AWS CLI**: Installed and configured with access keys on your local machine.
3. **Boto3 Library**: Installed in your Python environment.

## Step 1: Upload the MP3 File to S3

1. **Create an S3 Bucket**:
   - Log in to your AWS Management Console.
   - Navigate to the S3 service and create a new bucket.
   - Name your bucket (e.g., `my-audio-bucket`) and choose a region.   

2. **Upload the MP3 File**:
   - After creating the bucket, upload the MP3 file you want to transcribe.
   - Make note of the S3 object URL (e.g., `https://my-audio-bucket.s3.amazonaws.com/audiofile.mp3`).
  
   ![Screenshot 2024-08-29 233849](https://github.com/user-attachments/assets/136e66c9-f82d-472f-bf0e-4e2b757fc3fd)

## Step 2: Configure AWS CLI with Access Keys

1. **Generate Access Keys**:
   - In the AWS Management Console, go to the IAM service.
   - Create a new user or select an existing one, and generate Access Keys (Access Key ID and Secret Access Key).
  
     


2. **Configure AWS CLI**:
   - Open your terminal and run the following command to configure the AWS CLI:
     ```bash
     aws configure
     ```
   - Enter your Access Key ID, Secret Access Key, and select your preferred region.
  
     ![Screenshot 2024-08-29 233949](https://github.com/user-attachments/assets/0215c98a-93be-46ac-b71a-81b111f0e04b)

## Step 3: Write the Python Code

1. **Install Required Libraries**:
   - Ensure you have Boto3 installed:
     ```bash
     pip install boto3
     ```

2. **Python Script for Transcription**:


![Screenshot 2024-08-29 233912](https://github.com/user-attachments/assets/b9e540e3-b738-4948-94c3-f4cfa1e1d0cb)

   
   - Use the following Python script to start a transcription job:
  ```
import boto3
import time
import urllib
import json
    
transcribe_client = boto3.client('transcribe')

def transcribe_file(job_name, file_uri, transcribe_client):
    transcribe_client.start_transcription_job(
        TranscriptionJobName=job_name,
        Media={'MediaFileUri': file_uri},
        MediaFormat='mp3',
        LanguageCode='en-US'
    )

    max_tries = 60
    while max_tries > 0:
        max_tries -= 1
        job = transcribe_client.get_transcription_job(TranscriptionJobName=job_name)
        job_status = job['TranscriptionJob']['TranscriptionJobStatus']
        if job_status in ['COMPLETED', 'FAILED']:
            print(f"Job {job_name} is {job_status}.")
            if job_status == 'COMPLETED':
                response = urllib.request.urlopen(job['TranscriptionJob']['Transcript']['TranscriptFileUri'])
                data = json.loads(response.read())
                text = data['results']['transcripts'][0]['transcript']
                print("========== below is output of speech-to-text ========================")
                print(text)
                print("=====================================================================")
            break
        else:
            print(f"Waiting for {job_name}. Current status is {job_status}.")
        time.sleep(10)


def main():
    file_uri = 's3://speech-to-text-converter-sanket/The First Law of Robotics by Isaac Asimov： A robot should not hurt a human #robotics #history.mp3'
    transcribe_file('Example-job', file_uri, transcribe_client)


if __name__ == '__main__':
    main()
```
  

3. **Run the Script**:
   - Execute the script in your terminal:
     ```bash
     python transcribe_audio.py
     ```
   - This will start a transcription job in Amazon Transcribe.

## Step 4: Fetch the Transcription Results

1. **Check the Status**:
   - You can monitor the job status in the AWS Management Console under the Amazon Transcribe service.
   - Once the job is complete, the transcription will be saved in the specified S3 bucket.

     ![Screenshot 2024-08-29 233827](https://github.com/user-attachments/assets/15404b11-9a21-4d26-9b13-24b7031de3d1)


2. **Retrieve the Transcription**:
   - The output file will be in JSON format, containing the transcribed text.

## Best Practices

- **Security**: Ensure your S3 buckets are appropriately secured, and your access keys are not exposed.
- **File Naming**: Use unique names for transcription jobs to avoid conflicts.
- **Error Handling**: Incorporate error handling in your Python script to manage potential issues during the transcription process.

## Conclusion

This guide provides a simple and effective way to convert speech to text using Amazon S3, Amazon Transcribe, and Python. By following these steps, you can automate the transcription process for audio files stored in S3, making it easier to manage and analyze spoken content.

---
