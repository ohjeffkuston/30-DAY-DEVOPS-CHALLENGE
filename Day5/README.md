# NCAA Game Highlights

## HighlightProcessor
This project leverages RapidAPI to fetch NCAA game highlights using a Docker container and utilizes AWS MediaConvert to process the media files.

## File Overview

### `config.py`
- Imports necessary environment variables and assigns them to Python variables.
- Provides default values for flexible configuration management across different environments (e.g., development, staging, production) without modifying the source code.

### `fetch.py`
- Sets the date and league to fetch highlights (using NCAA as an example since it's included in the free version).
- Fetches highlights from the API and stores them in an S3 bucket as a JSON file (`basketball_highlight.json`).

### `process_one_video.py`
- Connects to the S3 bucket and retrieves the JSON file.
- Extracts the first video URL from the JSON file.
- Downloads the video from the internet into memory using the requests library.
- Saves the video as a new file in the S3 bucket under a different folder (`videos/`).
- Logs the status of each step.

### `mediaconvert_process.py`
- Creates and submits a MediaConvert job.
- Configures MediaConvert to process the video file, setting the video codec, resolution, and bitrate, as well as audio settings.
- Stores the processed video back into an S3 bucket.

### `run_all.py`
- Runs the scripts in a sequential order and provides buffer time for the tasks to be completed.

### `.env`
- Stores all environment variables to avoid hardcoding them into the scripts.

### `Dockerfile`
- Provides step-by-step instructions to build the Docker image.

## Prerequisites
Before running the scripts, ensure you have the following:

### 1. Create a RapidAPI Account
- Sign up at RapidAPI.com to access highlight images and videos.
- Use the NCAA (USA College Basketball) highlights included in the free plan.
- [Sports Highlights API](https://rapidapi.com/highlightly-api-highlightly-api-default/api/sport-highlights-api/playground/apiendpoint_16dd5813-39c6-43f0-aebe-11f891fe5149) is the endpoint used.

### 2. Verify Prerequisites are Installed
- Docker: Verify installation with `docker --version`.
- AWS CLI: Verify installation with `aws --version`.
- Python3: Verify installation with `python3 --version`.

### 3. Retrieve AWS Account ID
- Log in to the AWS Management Console.
- Click on your account name in the top right corner to find your account ID.
- Copy and save your account ID for later use.

### 4. Retrieve Access Keys and Secret Access Keys
- Check the IAM dashboard for existing access keys.
- If you don't have a secret access key, create a new access key.

## Technical Diagram
![GameHighlightProcessor](https://github.com/user-attachments/assets/762c3582-c6fe-48b2-b7da-0ff5b86b7970)

## Project Structure
```bash
src/
├── Dockerfile           # Instructions to build the Docker image
├── config      # Configuration settings and environment variables
├── fetch.py    # Script to fetch NCAA highlights from RapidAPI
├── mediaconvert_process.py   # Script to process videos using AWS MediaConvert
├── process_one_video.py      # Script to download and store videos in S3
├── requirements.txt          # Python dependencies
├── run_all.py        # Orchestrates the execution of all scripts
├── .env            # Environment variables file
```

# START HERE - Local
## **Step 1: Clone The Repo**
```bash
git clone https://github.com/ohjeffkuston/30-DAY-DEVOPS-CHALLENGE.git
cd DAy5/src
```
## **Step 2: Add API Key to AWS Secrets Manager**
```bash
aws secretsmanager create-secret \
    --name my-api-key \
    --description "API key for accessing the Sport Highlights API" \
    --secret-string '{"api_key":"YOUR_ACTUAL_API_KEY"}' \
    --region us-east-1
```

## **Step 3: Create an IAM role or user**

In the search bar type "IAM" 

Click Roles -> Create Role

For the Use Case enter "S3" and click next

Under Add Permission search for AmazonS3FullAccess, MediaConvertFullAccess and AmazonEC2ContainerRegistryFullAccess and click next

Under Role Details, enter "HighlightProcessorRole" as the name

Select Create Role

Find the role in the list and click on it
Under Trust relationships
Edit the trust policy to this:
Edit the Trust Policy and replace it with this:
```bash
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": [
          "ec2.amazonaws.com",
          "ecs-tasks.amazonaws.com",
          "mediaconvert.amazonaws.com"
        ],
        "AWS": "arn:aws:iam::<"your-account-id">:user/<"your-iam-user">"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

## **Step 4: Update .env file**
1. RapidAPI_KEY: Ensure that you have successfully created the account and select "Subscribe To Test" in the top left of the Sports Highlights API
2. AWS_ACCESS_KEY_ID=your_aws_access_key_id_here
3. AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key_here
4. S3_BUCKET_NAME=your_S3_bucket_name_here
5. MEDIACONVERT_ENDPOINT=https://your_mediaconvert_endpoint_here.amazonaws.com
```bash
aws mediaconvert describe-endpoints
```
7. MEDIACONVERT_ROLE_ARN=arn:aws:iam::your_account_id:role/HighlightProcessorRole

## **Step 5: Secure .env file**
```bash
chmod 600 .env
```
## **Step 6: Locally Buikd & Run The Docker Container**
Run:
```bash
docker build -t highlight-processor .
```

Run the Docker Container Locally:
```bash
docker run --env-file .env highlight-processor
```
           
This will run fetch.py, process_one_video.py and mediaconvert_process.py and the following files should be saved in your S3 bucket:

Optional - Confirm there is a video uploaded to s3://<your-bucket-name>/videos/first_video.mp4

Optional - Confirm there is a video uploaded to s3://<your-bucket-name>/processed_videos/

### **What We Learned**
1. Working with Docker and AWS Services
2. Identity Access Management (IAM) and least privilege
3. How to enhance media quality 
