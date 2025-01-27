# Terraform Integration

## Using Terraform to automate RapidAPI to obtain NCAA game highlights using a Docker container and uses AWS Media Convert to convert the media file.

### **Configuring terraform.tfvars**
1. Access the resources folder in the repository and duplicate its contents
2. Create vpc_setup.sh in either AWS Cloudshell or VS Code terminal
3. Execute the setup script
```bash
bash vpc_setup.sh
```
4. Copy the generated variables to lines 8-13
5. Securely store your API credentials using AWS Secrets Manager
```bash
aws ssm put-parameter \
    --name "/myproject/rapidapi_key" \
    --value "YOUR_SECRET_KEY" \
    --type SecureString
```
6. Retrieve your MediaConvert endpoint:
```bash
aws mediaconvert describe-endpoints
```
7. Keep mediaconvert_role_arn blank for now

### **Project Deployment Steps**
1. Switch to the terraform directory
```bash
cd terraform
```
2. Set up terraform environment
```bash
terraform init
```
3. Verify configuration integrity
```bash
terraform validate
```
4. Preview infrastructure changes
```bash
terraform plan
```
5. Deploy infrastructure
```bash
terraform apply -var-file="terraform.tfvars"
```
6. Prepare Docker image for AWS
```bash
docker build -t highlight-pipeline:latest .
```
```bash
docker tag highlight-pipeline:latest <AWS_ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/highlight-pipeline:latest
```
7. ECR Authentication and Upload
```bash
aws ecr get-login-password --region us-east-1 | \
    docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
```   
```bash
docker push <AWS_ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/highlight-pipeline:latest
```

### **Resource Cleanup**
1. Create and execute ncaaprojectcleanup.sh from the resources folder
```bash
bash ncaaprojectcleanup.sh
```

### **Output Verification**
1. Check your S3 Bucket for:
   - JSON video file in highlights folder
   - Video file in videos folder

### **Key Takeaways**
1. ECR Docker image deployment
2. Terraform configuration fundamentals
3. AWS networking components (VPC, IGW, Subnets)
4. AWS Systems Manager Parameter Store integration
