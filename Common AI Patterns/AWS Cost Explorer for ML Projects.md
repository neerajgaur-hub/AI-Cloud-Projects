# AWS Cost Explorer for ML Projects Cheat Sheet

## Overview
AWS Cost Explorer helps you analyze and optimize spending on machine learning (ML) projects. This cheat sheet provides tips, best practices, and tools for managing costs across AWS services like SageMaker, EC2, and S3.

## Key Features
- **Cost and Usage Reports**: View detailed breakdowns of AWS costs by service, resource, and tags.
- **Forecasting**: Predict future spending based on historical usage trends.
- **Cost Allocation Tags**: Organize and track ML project expenses using custom tags.
- **Savings Plans**: Commit to consistent usage levels for discounts on compute resources.

---

## Step-by-Step Instructions

### 1. Set Up Cost Explorer
1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Open **Cost Management** and enable Cost Explorer.
3. Configure **Cost Allocation Tags**:
   - Go to **Billing Console** > **Cost Allocation Tags**.
   - Enable relevant tags (e.g., `Project`, `Environment`, `Owner`).

### 2. Analyze ML Costs
- Use the **Service Filter** to isolate SageMaker, EC2, S3, and other ML-related services.
- Group costs by **Usage Type** (e.g., `ml.m5.large`, `ml.p3.2xlarge`) to identify expensive instance types.
- Set a **Time Range** to analyze cost trends over weeks or months.

#### Example Query
- **Group by**: Service
- **Filter**: SageMaker, EC2, and S3
- **Time Period**: Last 30 days

### 3. Forecast Future Costs
1. In Cost Explorer, go to the **Forecasts** tab.
2. View spending predictions for the next 3 or 12 months.
3. Adjust project budgets or commit to Savings Plans based on the forecast.

---

## Best Practices

### General Recommendations
1. **Enable Reserved Instances or Savings Plans**:
   - Use Reserved Instances for persistent training jobs.
   - Commit to Savings Plans for discounts on on-demand compute usage.

2. **Optimize Instance Usage**:
   - Use Spot Instances for non-critical training jobs to save up to 90%.
   - Right-size instance types for training and inference workloads.

3. **Tag Resources**:
   - Apply consistent tags (e.g., `Project:MLModel1`, `Environment:Dev`) to track specific project costs.

4. **Use Auto-Termination Policies**:
   - Automatically stop idle SageMaker notebooks or EC2 instances.

#### Example: Auto-Shutdown for SageMaker Notebooks
```python
import boto3

sagemaker = boto3.client('sagemaker')
response = sagemaker.stop_notebook_instance(
    NotebookInstanceName='my-notebook-instance'
)
print("Notebook instance stopped!")
```

---

## Monitoring Tools
- **AWS Budgets**: Set spending limits and receive alerts when costs approach thresholds.
- **AWS Trusted Advisor**: Receive recommendations for cost optimization and resource usage.
- **Cost Anomaly Detection**: Detect unusual spending patterns for ML services.

---

## Additional Resources
- [AWS Cost Explorer Documentation](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-explorer.html)
- [AWS SageMaker Pricing](https://aws.amazon.com/sagemaker/pricing/)
- [AWS Budgets Documentation](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets.html)

**Pro Tip**: Regularly review Cost Explorer to identify underutilized ML resources and switch to cost-effective alternatives like Spot Instances or serverless options.
