# Game Day Notifications / Sports Alerts System

## **Project Overview**
This project is an alert system that delivers real-time NBA game day score notifications to users via SMS/Email. It utilizes **Amazon SNS**, **AWS Lambda and Python**, **Amazon EventBridge**, and **NBA APIs** to keep sports fans updated with the latest game information. The project showcases the use of Infrastructure as Code with Terraform to automate the deployment and teardown of the solution quickly.

---

## **Features**
- Retrieves live NBA game scores from an external API.
- Sends formatted score updates to subscribers via SMS/Email using Amazon SNS.
- Automates regular updates with Amazon EventBridge.
- Designed with security best practices, implementing least privilege for IAM roles.

## **Prerequisites**
- Free account with subscription and API Key from [sportsdata.io](https://sportsdata.io/)
- Personal AWS account with basic knowledge of AWS and Python
- AWS CLI installed and configured
- Terraform CLI version 1.10.5 installed locally

---

## **Technical Architecture**
![nba_API](https://github.com/user-attachments/assets/5e19635e-0685-4c07-9601-330f7d1231f9)

---

## **Technologies**
- **Cloud Provider**: AWS
- **Infrastructure as Code**: Terraform
- **Core Services**: SNS, Lambda, EventBridge
- **External API**: NBA Game API (SportsData.io)
- **Programming Language**: Python 3.x
- **IAM Security**:
  - Least privilege policies for Lambda, SNS, EventBridge, and Systems Manager

---

## **Project Structure**
```bash
game-day-notifications_terraform/
├── nba_notifications.py         # Main Lambda function code
├── nba_notifications.zip        # Main Lambda function zipped file
├── game_day_notifications.tf    # Terraform configuration file
├── LICENSE                     
├── .gitignore
└── README.md                    # Project documentation
``` 

## **Setup Instructions**

### **Clone the Repository**
```bash
git clone https://github.com/ohjeffkuston/30-DAY-DEVOPS-CHALLENGE.git
cd Day9
```

### **Store API Key as secret in Parameter store**
1. Run this aws cli command with your api key to store it in Paremeter store
```bash
aws ssm put-parameter --name "nba-api-key" --value "<API_KEY>" --type "SecureString"
```

### **Run Terraform commands**
1. Initialize Terraform directory, provider plugins and set up local backend
```bash
terraform init
```
2. Format Terraform config files to make it clean, readable, and follow best practices.
```bash
terraform fmt
```
3. Check Terraform configuration for syntax errors and correctness
```bash
terraform validate
```
4. Show preview of changes Terraform will make to your infrastructure before applying them
```bash
terraform plan
```
5. Create or update the infrastructure based on the Terraform configuration.
```bash
terraform apply
```
6. Remove all resources defined in your Terraform configuration.
```bash
terraform destory
```

### **Add Subscriptions to the SNS Topic**
1. After creating the topic, head on the SNS topic name.
2. Navigate to the Subscriptions tab and click Create subscription.
3. Select a Protocol:
- For Email:
  - Choose Email.
  - Enter a valid email address.
- For SMS (phone number):
  - Choose SMS.
  - Enter a valid phone number in international format (e.g., +1234567890).

4. Click Create Subscription.
5. If you added an Email subscription:
- Check the inbox of the provided email address.
- Confirm the subscription by clicking the confirmation link in the email.

### **Test the System**
1. Open the Lambda function in the AWS Management Console.
2. Create a test event to simulate execution.
3. Run the function and check CloudWatch Logs for errors.
4. Verify that SMS notifications are sent to the subscribed users.

### **What We Learned**
1. Designing a notification system with AWS SNS and Lambda.
2. Securing AWS services with least privilege IAM policies.
3. Automating workflows using EventBridge.
4. Integrating external APIs into cloud-based workflows.
5. Automated the entier solution with Infrastructure as Code tool Terraform
