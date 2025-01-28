# Azure Cognitive Services + AWS Lambda Integration Cheat Sheet

## Overview
This guide demonstrates how to integrate Azure Cognitive Services with AWS Lambda to create serverless AI solutions. Azure Cognitive Services provides a wide range of AI capabilities (e.g., language, vision, and speech processing), while AWS Lambda enables event-driven, serverless computing to run code without managing servers.

---

## Key Features of the Integration
- **Azure Cognitive Services:** Offers pre-built AI models for tasks like natural language processing, computer vision, and speech recognition.
- **AWS Lambda:** Provides serverless execution, allowing you to trigger AI processes based on events like S3 uploads or API calls.
- **Cross-Cloud Interoperability:** Combines the flexibility of AWS Lambda with the advanced AI models of Azure.
- **Scalability:** Automatically scales based on demand.

---

## Step-by-Step Instructions

### 1. Set Up Azure Cognitive Services
- Create an Azure Cognitive Services resource in the Azure portal.
- Select the service type (e.g., Text Analytics, Computer Vision, Speech).
- Note down the **API Key** and **Endpoint URL** from the Azure portal.

#### Example: Cognitive Services API Call
```python
import requests

# Define the API endpoint and key
endpoint = "https://<your-resource-name>.cognitiveservices.azure.com/text/analytics/v3.0/sentiment"
key = "<your-api-key>"

headers = {
    "Ocp-Apim-Subscription-Key": key,
    "Content-Type": "application/json"
}

# Example payload
data = {
    "documents": [
        {"id": "1", "language": "en", "text": "Azure is amazing!"}
    ]
}

response = requests.post(endpoint, headers=headers, json=data)
print(response.json())
```

---

### 2. Set Up AWS Lambda
- Open the AWS Management Console and create a new Lambda function.
- Choose a runtime (e.g., Python 3.x).
- Add an S3 bucket or an API Gateway trigger to invoke the function.

#### Example: AWS Lambda Function Code
```python
import boto3
import requests

def lambda_handler(event, context):
    # Azure Cognitive Services API details
    endpoint = "https://<your-resource-name>.cognitiveservices.azure.com/text/analytics/v3.0/sentiment"
    key = "<your-api-key>"

    headers = {
        "Ocp-Apim-Subscription-Key": key,
        "Content-Type": "application/json"
    }

    # Example payload
    data = {
        "documents": [
            {"id": "1", "language": "en", "text": "AWS and Azure integration is powerful!"}
        ]
    }

    response = requests.post(endpoint, headers=headers, json=data)
    result = response.json()

    return {
        'statusCode': 200,
        'body': result
    }
```

---

### 3. Test the Integration
- Trigger the Lambda function via the configured event (e.g., uploading a file to S3 or calling an API Gateway endpoint).
- Verify the response from Azure Cognitive Services in the Lambda logs.

---

## Additional Resources
- [Azure Cognitive Services Documentation](https://learn.microsoft.com/en-us/azure/cognitive-services/): Comprehensive guide to Azure AI services.
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/): Details on creating and managing Lambda functions.
- [Cross-Cloud Data Transfer Guide](https://docs.aws.amazon.com/solutions/latest/cross-cloud-data-transfer/): Best practices for data sharing between AWS and Azure.

---

**Pro Tip:** Use AWS Secrets Manager to securely store the Azure API key and retrieve it in your Lambda function to enhance security.
