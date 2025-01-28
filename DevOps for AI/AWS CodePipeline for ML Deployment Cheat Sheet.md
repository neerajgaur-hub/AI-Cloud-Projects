# AWS CodePipeline for ML Deployment Cheat Sheet

## Overview
AWS CodePipeline automates the build, test, and deploy phases for machine learning (ML) models. This cheat sheet covers the steps to set up an ML pipeline, integrating with other AWS services like SageMaker for training and deployment.

## Key Features
- **Automated Workflows**: Create end-to-end pipelines for ML model deployment.
- **Integration with AWS Services**: Seamlessly integrate with SageMaker, S3, and Lambda.
- **Scalability**: Automatically scale deployment stages as needed.

## Instructions

### 1. Set Up an S3 Bucket for Artifacts
1. Open the [AWS Management Console](https://aws.amazon.com/console/).
2. Create an S3 bucket to store CodePipeline artifacts.

### 2. Define Your CodePipeline
1. Go to **CodePipeline** in the AWS Console.
2. Create a new pipeline and specify the S3 bucket as the artifact store.
3. Add a **Source Stage**:
   - Use CodeCommit, GitHub, or S3 as the source.
4. Add a **Build Stage**:
   - Use AWS CodeBuild to execute training scripts.

#### Example: Buildspec for Training
```yaml
version: 0.2
phases:
  install:
    commands:
      - pip install -r requirements.txt
  build:
    commands:
      - python train_model.py
artifacts:
  files:
    - outputs/model.tar.gz
```

### 3. Add a Deployment Stage
1. Use SageMaker for model deployment:
   - Select **SageMaker Model** as the deployment provider.
   - Specify the model artifacts path from S3.

#### Example: Deploy Model Using SageMaker
```python
import boto3

sagemaker = boto3.client('sagemaker')

response = sagemaker.create_model(
    ModelName='my-ml-model',
    PrimaryContainer={
        'Image': '<ecr-image-url>',
        'ModelDataUrl': 's3://<bucket-name>/outputs/model.tar.gz'
    },
    ExecutionRoleArn='<execution-role-arn>'
)

print("Model deployed successfully!")
```

### 4. Test the Pipeline
- Trigger the pipeline by pushing changes to the source repository.
- Verify that the pipeline runs through all stages successfully.

### 5. Monitor and Optimize
- Use CloudWatch to monitor pipeline execution and SageMaker endpoint metrics.
- Automate model retraining by integrating event-driven triggers like S3 uploads.

## Additional Resources
- [AWS CodePipeline Documentation](https://docs.aws.amazon.com/codepipeline/)
- [AWS SageMaker Documentation](https://docs.aws.amazon.com/sagemaker/)
- [AWS CodeBuild Documentation](https://docs.aws.amazon.com/codebuild/)

**Pro Tip**: Use AWS Secrets Manager to securely manage sensitive data like API keys and IAM credentials for pipeline stages.
