# AWS SageMaker Cheat Sheet

AWS SageMaker is a cloud service that enables developers and data scientists to build, train, and deploy machine learning models at scale.

---

## Step 1: Set Up AWS SageMaker
1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Search for **SageMaker** in the services menu.
3. Click **Create Notebook Instance** and configure:
   - **Name**: Choose a unique name for your notebook.
   - **Instance Type**: Select an instance size (e.g., `ml.t2.medium` for small-scale use).
   - **IAM Role**: Create or select an IAM role with permissions to access SageMaker and S3.
4. Click **Create Instance** and wait for it to start.

---

## Step 2: Prepare Your Dataset
1. Upload your data to an S3 bucket in your AWS account.
2. Ensure your IAM role has permissions to read from the S3 bucket.

---

## Step 3: Build and Train a Model
1. Open your SageMaker notebook instance.
2. Choose a sample notebook or upload your own script (Python recommended).
3. Use SageMaker's built-in algorithms or bring your own model.
4. Example Training Code:
   ```python
   import sagemaker
   from sagemaker import get_execution_role

   role = get_execution_role()

   # Set up session and S3 bucket
   session = sagemaker.Session()
   bucket = 'your-bucket-name'

   # Define training job
   estimator = sagemaker.LinearLearner(
       role=role,
       instance_count=1,
       instance_type='ml.m5.large',
       output_path=f's3://{bucket}/output'
   )

   # Start training
   estimator.fit({'train': 's3://your-bucket-name/train.csv'})
   
