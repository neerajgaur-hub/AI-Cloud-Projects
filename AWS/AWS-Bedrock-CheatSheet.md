# Amazon Bedrock Cheat Sheet

## Overview
Amazon Bedrock is a managed service by AWS that allows developers to build and scale generative AI applications using foundation models (FMs) without managing infrastructure. It simplifies the integration of AI into applications by providing API access to various FMs from multiple providers.

---

## Key Features
- **Foundation Models Access:** Seamlessly use multiple foundation models, including those from AI21 Labs, Anthropic, and Stability AI.
- **No Infrastructure Management:** Focus on building applications without worrying about model hosting or scaling.
- **Customizations:** Use in-context learning and embeddings to tailor models to specific use cases.
- **Integration with AWS Services:** Easily connect with other AWS tools like S3, Lambda, and SageMaker.
- **Pay-As-You-Go Pricing:** Only pay for the resources used.

---

## Step-by-Step Instructions
1. **Set Up Amazon Bedrock in AWS:**
   - Log in to the AWS Management Console.
   - Search for "Bedrock" and enable access (if required).
   - Ensure your IAM role has necessary permissions to interact with Bedrock APIs.

2. **Choose a Foundation Model:**
   - Explore available models (e.g., Claude, Jurassic-2, Stable Diffusion).
   - Select a model based on your use case (text generation, image generation, etc.).

3. **Create a Request:**
   - Use Bedrock APIs to send prompts and get model outputs.

4. **Integrate Bedrock in Your Application:**
   - Combine Bedrock with AWS Lambda for serverless deployments.
   - Use SageMaker for further model fine-tuning and training if needed.

5. **Monitor and Optimize:**
   - Track usage and performance through AWS CloudWatch.
   - Optimize API calls for cost-efficiency.

---

## Code Snippets
### Example: Text Generation with Amazon Bedrock
```python
import boto3

# Initialize the Bedrock client
client = boto3.client('bedrock')

# Define the model and prompt
response = client.invoke_model(
    modelId='ai21-jurassic-2',
    body={
        'prompt': 'Write a product description for a smart home device.',
        'maxTokens': 100
    }
)

print(response['body'])
```

<button onclick="navigator.clipboard.writeText(`import boto3

client = boto3.client('bedrock')

response = client.invoke_model(
    modelId='ai21-jurassic-2',
    body={
        'prompt': 'Write a product description for a smart home device.',
        'maxTokens': 100
    }
)

print(response['body'])
`)">Copy Code</button>

### Example: Image Generation with Stable Diffusion
```python
response = client.invoke_model(
    modelId='stability-stable-diffusion',
    body={
        'prompt': 'A serene mountain landscape at sunset.',
        'width': 512,
        'height': 512
    }
)

# Save the generated image
with open('output_image.png', 'wb') as f:
    f.write(response['body']['generatedImage'])
```

<button onclick="navigator.clipboard.writeText(`response = client.invoke_model(
    modelId='stability-stable-diffusion',
    body={
        'prompt': 'A serene mountain landscape at sunset.',
        'width': 512,
        'height': 512
    }
)

with open('output_image.png', 'wb') as f:
    f.write(response['body']['generatedImage'])
`)">Copy Code</button>

---

## Additional Resources
- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/): Official guide and API documentation.
- [AWS Pricing for Bedrock](https://aws.amazon.com/bedrock/pricing/): Details on usage costs.
- [Bedrock API Reference](https://docs.aws.amazon.com/bedrock/latest/APIReference/): Comprehensive API details.

---

**Pro Tip:** Combine Bedrock with AWS Step Functions to create robust AI-driven workflows for your applications.
