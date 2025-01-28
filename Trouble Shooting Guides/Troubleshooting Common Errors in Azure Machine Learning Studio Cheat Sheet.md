# Troubleshooting Common Errors in Azure Machine Learning Studio Cheat Sheet

## Overview
This cheat sheet covers common issues encountered in Azure Machine Learning Studio, their possible causes, and actionable solutions to help you resolve them quickly.

## Common Errors and Fixes

### 1. **Error: Insufficient Quota**
- **Cause**: Exceeded resource quota for your subscription.
- **Solution**:
  1. Go to the **Azure Portal** > **Subscriptions** > **Usage + quotas**.
  2. Request a quota increase for the specific resource (e.g., GPUs, vCPUs).
  3. Optimize your resources by selecting smaller VM types or Spot VMs.

#### Example: Check Quota with Azure CLI
```bash
az vm list-usage --location eastus --output table
```

---

### 2. **Error: Compute Instance Fails to Start**
- **Cause**: Networking issues, insufficient permissions, or unavailability of resources in the selected region.
- **Solution**:
  1. Verify that the selected region has the required resources available.
  2. Check the **IAM roles** to ensure you have sufficient permissions.
  3. Ensure the subnet associated with the compute instance allows outbound internet access.

#### Example: Restart a Compute Instance
```bash
az ml compute restart --name my-compute --resource-group my-group --workspace-name my-workspace
```

---

### 3. **Error: Model Deployment Fails**
- **Cause**: Incorrect model dependencies, missing container image, or configuration issues.
- **Solution**:
  1. Ensure all required Python libraries are listed in the `conda.yaml` or `requirements.txt` file.
  2. Validate that the scoring script (`score.py`) is correctly implemented and matches the input/output schema.
  3. Use Azure Container Registry (ACR) to store the model image and ensure it is accessible.

#### Example: Validate Environment Configuration
```bash
az ml environment list --workspace-name my-workspace --resource-group my-group
```

---

### 4. **Error: Experiment Fails to Run**
- **Cause**: Missing data, incorrect compute target, or syntax errors in the training script.
- **Solution**:
  1. Verify that the dataset is correctly uploaded to the datastore and accessible.
  2. Ensure the compute target specified in the experiment exists and is running.
  3. Debug the training script locally before running it on Azure.

#### Example: Check Datastores
```bash
az ml datastore list --workspace-name my-workspace --resource-group my-group
```

---

### 5. **Error: Endpoint Response Times Are High**
- **Cause**: Insufficient compute resources or inefficient model inference.
- **Solution**:
  1. Scale up or scale out the deployed endpoint to handle more requests.
  2. Optimize the model for inference using tools like ONNX or TensorRT.
  3. Enable autoscaling for the endpoint to dynamically adjust compute resources.

#### Example: Update Endpoint Autoscaling
```bash
az ml endpoint update --name my-endpoint --autoscale-enabled true
```

---

## Best Practices

### General Troubleshooting Tips
1. **Use Logs**: Check logs in Azure Monitor or Application Insights for detailed error messages.
2. **Validate Configurations**: Ensure that YAML files and environment configurations are correctly defined.
3. **Monitor Resource Usage**: Use Azure Monitor to identify bottlenecks or resource constraints.
4. **Stay Updated**: Ensure SDKs and dependencies are up-to-date to avoid compatibility issues.

---

## Additional Resources
- [Azure Machine Learning Documentation](https://learn.microsoft.com/en-us/azure/machine-learning/)
- [Azure CLI Reference](https://learn.microsoft.com/en-us/cli/azure/)
- [Azure Monitor Documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/)

**Pro Tip**: Enable email alerts for critical resource failures to stay proactive in resolving issues.
