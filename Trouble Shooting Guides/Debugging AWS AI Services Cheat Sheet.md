# Debugging AWS AI Services Cheat Sheet

## Overview
This cheat sheet provides solutions to common issues encountered while working with AWS AI services such as SageMaker, Rekognition, and Translate. Learn to identify causes and apply best practices for debugging.

---

## Common Errors and Fixes

### 1. **Error: SageMaker Training Job Fails**
- **Cause**: Incorrect input data format, insufficient permissions, or incompatible hyperparameters.
- **Solution**:
  1. Verify that the input data is correctly uploaded to the S3 bucket and matches the expected format.
  2. Check IAM permissions for accessing S3 and SageMaker resources.
  3. Review and adjust hyperparameters for compatibility with the algorithm.

#### Example: Check Training Job Logs
```bash
aws sagemaker describe-training-job --training-job-name my-training-job
```

---

### 2. **Error: Rekognition Cannot Detect Objects**
- **Cause**: Image resolution is too low, unsupported file format, or insufficient permissions for S3 objects.
- **Solution**:
  1. Ensure that images are in a supported format (JPEG, PNG) and have sufficient resolution.
  2. Check that the S3 bucket permissions allow Rekognition to access the images.
  3. Use the `MinConfidence` parameter to fine-tune detection results.

#### Example: Rekognition API Call with Confidence Setting
```python
response = client.detect_labels(
    Image={
        'S3Object': {
            'Bucket': 'my-bucket',
            'Name': 'image.jpg'
        }
    },
    MinConfidence=75
)
```

---

### 3. **Error: Translate Returns Incorrect Results**
- **Cause**: Input text length exceeds limits or language pairs are not supported.
- **Solution**:
  1. Break input text into smaller segments if exceeding the 5,000-character limit.
  2. Verify that the specified language pair is supported by Translate.
  3. Use the `Terminology` feature to customize translations for domain-specific accuracy.

#### Example: Using Translate Terminology
```python
response = client.translate_text(
    Text="Hello World",
    TerminologyNames=['custom-terminology'],
    SourceLanguageCode='en',
    TargetLanguageCode='es'
)
```

---

### 4. **Error: SageMaker Endpoint Times Out**
- **Cause**: Insufficient compute resources, network connectivity issues, or large payload size.
- **Solution**:
  1. Scale up the endpoint instance type or increase the number of instances.
  2. Ensure the endpoint is deployed in the correct VPC and has proper network configurations.
  3. Use compression for large payloads to reduce data transfer time.

#### Example: Update SageMaker Endpoint Config
```bash
aws sagemaker update-endpoint --endpoint-name my-endpoint \
  --endpoint-config-name my-new-config
```

---

### 5. **Error: Permissions Denied for AWS AI Service**
- **Cause**: Missing IAM policies or insufficient permissions for required actions.
- **Solution**:
  1. Attach the correct IAM policies to the role or user accessing the service.
  2. Use AWS Identity and Access Management (IAM) Policy Simulator to debug permission issues.

#### Example: Add IAM Policy for Rekognition
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "rekognition:*",
            "Resource": "*"
        }
    ]
}
```

---

## Best Practices

### General Debugging Tips
1. **Enable Logging**: Use AWS CloudWatch to track logs for SageMaker, Rekognition, and other AI services.
2. **Test Locally**: Validate algorithms and scripts locally with smaller datasets before deploying to AWS.
3. **Monitor Resource Usage**: Use CloudWatch metrics to identify resource bottlenecks and optimize configurations.
4. **Stay Updated**: Ensure that SDKs and dependencies are up-to-date to avoid compatibility issues.

---

## Monitoring Tools
- **AWS CloudWatch**: Monitor logs and metrics for all AWS services.
- **AWS Trusted Advisor**: Get recommendations to optimize resources and permissions.
- **IAM Policy Simulator**: Test and debug IAM permission policies.

---

## Additional Resources
- [AWS SageMaker Documentation](https://docs.aws.amazon.com/sagemaker/)
- [AWS Rekognition Documentation](https://docs.aws.amazon.com/rekognition/)
- [AWS Translate Documentation](https://docs.aws.amazon.com/translate/)

**Pro Tip**: Set up CloudWatch Alarms for critical metrics like endpoint latency, error rates, and service quotas to stay proactive in resolving issues.
