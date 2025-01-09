# Day 3: NBA Data Lake Setup

This repository contains the `setup_nba_data_lake.py` script, designed to automate the creation of a data lake for NBA analytics. The script leverages AWS services, including Amazon S3, AWS Glue, and Amazon Athena, to establish a complete infrastructure for storing, managing, and querying NBA-related data.

---

## Overview

The `setup_nba_data_lake.py` script performs the following key functions:

1. Creates an Amazon S3 bucket to store raw and processed NBA data.
2. Uploads sample NBA data in JSON format to the S3 bucket.
3. Sets up an AWS Glue database and external table for data exploration.
4. Configures Amazon Athena to query data stored in the S3 bucket.

---

## Prerequisites

### SportsData.io API Key

To retrieve the required API key:

1. Visit [SportsData.io](https://sportsdata.io) and create a free account.
2. Navigate to the "Developers" section and select "API Resources."
3. Choose "Introduction & Testing" and sign up for the "SportsDataIO API Free Trial," selecting NBA as the sport.
4. Check your email for a link to access the Developer Portal and click "Launch Developer Portal."
5. Switch to the NBA section, find the "Standings" endpoint, and copy the API key provided in the "Query String Parameters" dropdown.

### AWS IAM Role Permissions

Ensure the IAM user or role executing the script has the following permissions:

- **Amazon S3**: 
  - `s3:CreateBucket`
  - `s3:PutObject`
  - `s3:DeleteBucket`
  - `s3:ListBucket`
- **AWS Glue**: 
  - `glue:CreateDatabase`
  - `glue:CreateTable`
  - `glue:DeleteDatabase`
  - `glue:DeleteTable`
- **Amazon Athena**: 
  - `athena:StartQueryExecution`
  - `athena:GetQueryResults`

---

## Instructions

### Step 1: Open AWS CloudShell

1. Log in to your AWS account at [aws.amazon.com](https://aws.amazon.com).
2. Launch CloudShell by clicking the icon with `>_` near the top navigation bar.

---

### Step 2: Create the Python Script

1. Open the CloudShell editor and create a new file:
   ```bash
   nano setup_nba_data_lake.py
   ```
2. In another window, go to [GitHub](https://github.com/ohjeffkuston/30-DAY-DEVOPS-CHALLENGE.git)

- Copy the contents inside the setup_nba_data_lake.py file

- Go back to the Cloudshell window and paste the contents inside the file.

# Step 3: Create .env file
1. In the CLI (Command Line Interface), type
```bash
nano .env
```
2. paste the following line of code into your file, ensure you swap out with your API key
```bash
SPORTS_DATA_API_KEY=your_sportsdata_api_key
NBA_ENDPOINT=https://api.sportsdata.io/v3/nba/scores/json/Players
```

3. Press ^X to exit, press Y to save the file, press enter to confirm the file name 


# Step 4: Run the script
1. In the CLI type
```bash
python3 setup_nba_data_lake.py
```
-You should see the resources were successfully created, the sample data was uploaded successfully and the Data Lake Setup Completed

# Step 5: Manually Check For The Resources
1. In the Search Bar, type S3 and click blue hyper link name

-You should see 2 General purpose bucket named "Sports-analytics-data-lake"

-When you click the bucket name you will see 3 objects are in the bucket

2. Click on raw-data and you will see it contains "nba_player_data.json"

3. Click the file name and at the top you will see the option to Open the file

-You'll see a long string of various NBA data

### **What We Learned**
1. Securing AWS services with least privilege IAM policies.
2. Automating the creation of services with a script.
3. Integrating external APIs into cloud-based workflows.
