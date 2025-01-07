
# **30 Days DevOps Challenge - Weather Dashboard**

### **Day 1: Building a Weather Data Collection System with AWS S3 and OpenWeather API**

---

## **📌 Project Overview**
This project focuses on creating a Weather Data Collection System to demonstrate core DevOps principles, including:
- **API Integration**: Fetch real-time weather data using the OpenWeather API.
- **Cloud Storage**: Store weather data securely in AWS S3.
- **Infrastructure as Code**: Streamline deployment processes.
- **Version Control**: Use Git for efficient change management.
- **Python Development**: Write clean and modular code.
- **Error Handling**: Build a robust system to handle failures.
- **Environment Management**: Securely manage sensitive credentials.

---

## **🌟 Features**
- Fetches real-time weather data for multiple cities.
- Displays:
  - Temperature (°F)
  - Humidity
  - Weather conditions
- Stores weather data automatically in AWS S3 with timestamps.
- Supports historical data tracking for multiple cities.

---

## **⚙️ Technical Architecture**
- **Programming Language**: Python 3.x
- **Cloud Provider**: AWS (S3)
- **External API**: OpenWeather API
- **Key Dependencies**:
  - `boto3` (AWS SDK for Python)
  - `python-dotenv` (Environment variable management)
  - `requests` (HTTP requests)

---

## **📂 Project Structure**
\`\`\`plaintext
weather-dashboard/
  ├── src/
  │     ├── __init__.py
  │     └── weather_dashboard.py
  ├── tests/
  ├── data/
  ├── .env
  ├── .gitignore
  ├── requirements.txt
\`\`\`

---

## **🚀 Setup Instructions**

### 1. Clone the Repository
\`\`\`bash
git clone https://github.com/ohjeffkuston/30-DAY-DEVOPS-CHALLENGE.git
cd 30-DAY-DEVOPS-CHALLENGE
\`\`\`

### 2. Install Dependencies
\`\`\`bash
pip install -r requirements.txt
\`\`\`

### 3. Configure Environment Variables
Create a `.env` file in the project root directory and add the following:
\`\`\`plaintext
OPENWEATHER_API_KEY=your_api_key
AWS_BUCKET_NAME=your_bucket_name
\`\`\`

### 4. Configure AWS Credentials
Set up AWS credentials using the AWS CLI:
\`\`\`bash
aws configure
\`\`\`

### 5. Run the Application
Execute the program:
\`\`\`bash
python src/weather_dashboard.py
\`\`\`

---

## **🎓 What I Learned**
- **AWS S3**: Bucket creation and management.
- **Environment Variables**: Secure handling of API keys.
- **Python**: Best practices for API integration.
- **Git**: Managing workflows for collaborative development.
- **Error Handling**: Building resilience in distributed systems.
- **Cloud Management**: Resource automation and monitoring.

---

## **🚧 Future Enhancements**
- Add weather forecasting capabilities.
- Implement data visualization for enhanced insights.
- Expand support for additional cities.
- Create automated tests for improved reliability.
- Set up a CI/CD pipeline for seamless integration and deployment.

---

## **📜 License**
This project is open-source and available under the [MIT License](LICENSE).
