# Azure Cognitive Services Cheat Sheet

Azure Cognitive Services provides pre-built AI models for tasks like language understanding, vision recognition, and decision-making.

---

## Step 1: Set Up Azure Cognitive Services
1. Go to the [Azure Portal](https://portal.azure.com).
2. Click **Create a Resource** > Search for "Cognitive Services."
3. Select **Cognitive Services** from the results and click **Create**.
4. Fill in the following details:
   - **Name**: Choose a unique name for your service.
   - **Subscription**: Select your Azure subscription.
   - **Resource Group**: Use an existing group or create a new one.
   - **Region**: Pick a region close to your users.
   - **Pricing Tier**: Choose based on your requirements.

---

## Step 2: Retrieve Keys and Endpoint
1. Once the service is created, navigate to the **Overview** page of the resource.
2. Copy the **Key 1** and **Key 2** values.
3. Copy the **Endpoint** URL for making API calls.

---

## Step 3: Test the Service
1. Use tools like [Postman](https://www.postman.com/) or the built-in **Test Console** in Azure to test API requests.
2. Example API Call:
   ```bash
   curl -X POST "{Endpoint}/text/analytics/v3.0/sentiment" \
   -H "Ocp-Apim-Subscription-Key: {Your-Key}" \
   -H "Content-Type: application/json" \
   -d '{"documents":[{"id":"1","language":"en","text":"Azure is amazing!"}]}'
