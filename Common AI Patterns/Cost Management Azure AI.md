# Cost Management Tips for Azure AI Cheat Sheet

## Overview
Optimizing costs for Azure AI services is critical to managing budgets while leveraging powerful AI capabilities. This cheat sheet provides actionable tips and best practices to reduce costs across Azure AI services like Azure Machine Learning, Cognitive Services, and Synapse Analytics.

## Key Areas to Optimize

### 1. Azure Machine Learning
- **Use Spot VMs**: Save up to 90% on compute costs by using Spot Virtual Machines for training jobs.
- **Schedule Compute Instances**: Automatically shut down idle compute resources with scheduled tasks.
- **Leverage Low-Priority VMs**: Use low-priority compute clusters for batch inference or non-time-sensitive workloads.
- **Monitor Job Utilization**: Use Azure Monitor to track and optimize job resource usage.

#### Example: Schedule Compute Shutdown
```bash
az ml compute update --name my-compute --resource-group my-group \
  --workspace-name my-workspace --auto-scale-enabled true --min-instances 0 --max-instances 5
```

### 2. Cognitive Services
- **Choose the Right Pricing Tier**: Select pricing tiers based on expected usage (e.g., S0 for development, S1+ for production).
- **Batch Requests**: Combine multiple API calls into a single batch request to minimize costs.
- **Monitor Quotas**: Track API usage and set alerts to avoid overages.

#### Example: Batch API Request
```python
import requests
url = "https://<endpoint>.cognitiveservices.azure.com/vision/v3.0/analyze"
headers = {"Ocp-Apim-Subscription-Key": "<key>"}
data = {"requests": [{"url": "<image-url-1>"}, {"url": "<image-url-2>"}]}
response = requests.post(url, headers=headers, json=data)
print(response.json())
```

### 3. Azure Synapse Analytics
- **Use Serverless Pools**: For ad-hoc queries, serverless SQL pools offer cost-effective, pay-per-query pricing.
- **Optimize Data Partitioning**: Reduce scan costs by partitioning data in Parquet or Delta Lake formats.
- **Pause Dedicated SQL Pools**: Pause dedicated pools during periods of inactivity to save costs.

#### Example: Pause Dedicated SQL Pool
```sql
ALTER DATABASE my_database SET PAUSE;
```

---

## Best Practices

### General Cost Optimization Tips
1. **Use Azure Cost Management + Billing**: Set budgets and monitor spending in real time.
2. **Apply Reserved Instances**: Commit to long-term usage for discounts on VMs and other resources.
3. **Right-Size Resources**: Analyze resource utilization and downgrade overprovisioned instances.
4. **Leverage Free Tiers**: Use free tier options during development or testing phases.
5. **Enable Autoscaling**: Dynamically scale resources to match workload demand.

---

## Monitoring Tools
- **Azure Monitor**: Provides insights into resource usage and performance.
- **Cost Management + Billing**: Tracks spending and forecasts future costs.
- **Azure Advisor**: Offers recommendations to optimize resources and reduce costs.

---

## Additional Resources
- [Azure Cost Management](https://learn.microsoft.com/en-us/azure/cost-management/)
- [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- [Azure Monitor Documentation](https://learn.microsoft.com/en-us/azure/azure-monitor/)

**Pro Tip**: Regularly review Azure Advisor recommendations to identify underutilized resources and cost-saving opportunities.
