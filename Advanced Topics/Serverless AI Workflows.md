# Serverless AI Workflows Cheat Sheet

## Overview
Serverless AI workflows enable running AI inference without managing infrastructure. This cheat sheet explains how to use **Azure Functions** and **AWS Lambda** for deploying serverless AI workflows, along with best practices and examples.

---

## Key Features

### Azure Functions
- **Event-Driven**: Triggered by HTTP requests, queues, blob storage, and more.
- **AI Integration**: Seamlessly integrates with Azure Cognitive Services and Azure Machine Learning.
- **Scaling**: Automatically scales to handle varying workloads.

### AWS Lambda
- **Event Sources**: Triggered by API Gateway, S3 events, DynamoDB streams, and more.
- **AI Integration**: Connects with SageMaker, Rekognition, and Translate.
- **Cost Efficiency**: Pay only for execution time.

---

## Step-by-Step Instructions

### 1. Set Up Serverless Functions

#### Azure Functions
1. Create a new Function App in the Azure Portal.
2. Choose a trigger type (e.g., HTTP, Timer).
3. Write the function code in Python, C#, or JavaScript.

#### AWS Lambda
1. Open the AWS Lambda Console and create a new function.
2. Select a trigger (e.g., S3, API Gateway).
3. Write the function code in Python, Node.js, or Java.

---

### 2. Add AI Inference Logic

#### Example: Azure Functions for Text Sentiment Analysis
```python
import requests
import logging

endpoint = "https://<your-resource-name>.cognitiveservices.azure.com/text/analytics/v3.0/sentiment"
api_key = "<your-api-key>"

def main(req: func.HttpRequest) -> func.HttpResponse:
    data = req.get_json()
    headers = {"Ocp-Apim-Subscription-Key": api_key}
    response = requests.post(endpoint, headers=headers, json=data)
    return func.HttpResponse(response.text)
```

#### Example: AWS Lambda for Image Classification with SageMaker
```python
import boto3

def lambda_handler(event, context):
    sagemaker = boto3.client('sagemaker-runtime')
    response = sagemaker.invoke_endpoint(
        EndpointName='my-endpoint',
        ContentType='application/json',
        Body=event['body']
    )
    return {
        'statusCode': 200,
        'body': response['Body'].read().decode()
    }
```

---

### 3. Deploy and Test

#### Azure Functions
- Deploy via **Azure Portal**, **VS Code**, or **Azure CLI**.
- Test locally using the Azure Functions Core Tools.

#### AWS Lambda
- Deploy via **AWS Console**, **SAM CLI**, or **CloudFormation**.
- Test using the AWS Lambda Console or API Gateway.

---

## Best Practices

### General Recommendations
1. **Optimize Function Runtime**: Use lightweight models and minimize cold start latency.
2. **Set Memory Limits**: Allocate sufficient memory to handle AI inference workloads.
3. **Secure API Access**: Use API keys, IAM roles, or Azure AD for securing endpoints.

### Azure Functions
- Use **Azure Blob Storage** for storing intermediate results.
- Enable **Application Insights** for monitoring function performance.

### AWS Lambda
- Use **S3** for input/output data storage.
- Leverage **CloudWatch Logs** for debugging and monitoring.

---

## Additional Resources
- [Azure Functions Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/)
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Azure AI Services](https://learn.microsoft.com/en-us/azure/cognitive-services/)
- [AWS AI Services](https://aws.amazon.com/machine-learning/)

**Pro Tip**: Combine serverless functions with event-driven architectures for real-time, scalable AI workflows.
