# Azure Machine Learning Studio Cheat Sheet

Azure Machine Learning Studio is a collaborative platform for building, training, and deploying machine learning models. It offers tools for both code-first and low-code users.

---

## Step 1: Set Up Azure Machine Learning Studio
1. Go to the [Azure Portal](https://portal.azure.com).
2. Click **Create a Resource** > Search for "Machine Learning."
3. Select **Machine Learning** and click **Create**.
4. Fill in the following details:
   - **Workspace Name**: Choose a unique name for your workspace.
   - **Subscription**: Select your Azure subscription.
   - **Resource Group**: Use an existing group or create a new one.
   - **Region**: Select the region closest to your users.
   - **Storage Account, Key Vault, Application Insights**: Either create new ones or link existing resources.
5. Click **Review + Create** and wait for the deployment to finish.

---

## Step 2: Explore the Workspace
1. Navigate to the Machine Learning Workspace in the Azure Portal.
2. Click **Launch Studio** to open the Machine Learning Studio interface.
3. Explore key sections:
   - **Designer**: Drag-and-drop tool for building pipelines.
   - **Notebooks**: Write and run Python code for advanced workflows.
   - **Datasets**: Manage and explore your datasets.

---

## Step 3: Build and Deploy a Simple Model
### Build a Model with the Designer
1. Open the **Designer** tab.
2. Drag and drop the following modules:
   - **Dataset**: Upload a dataset or use a sample dataset.
   - **Split Data**: Split the dataset into training and testing sets.
   - **Train Model**: Choose an algorithm (e.g., Linear Regression).
   - **Score Model**: Evaluate the performance of your model.
3. Connect the modules by dragging lines between them.

### Deploy the Model
1. Click **Run** to execute the pipeline.
2. Once complete, click **Deploy** and create an **Endpoint**.
3. Test the endpoint using the built-in test console or tools like Postman.

---

## Helpful Links
- [Azure Machine Learning Studio Documentation](https://learn.microsoft.com/en-us/azure/machine-learning/)
- [Getting Started Guide](https://learn.microsoft.com/en-us/azure/machine-learning/tutorial-1st-experiment-sdk-setup)
- [API Reference](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-use-azureml-cli)

---

## Example Use Cases
- Predict customer churn using historical data.
- Automate image classification with deep learning.
- Build recommendation engines for personalized user experiences.

---

*Pro Tip: Add screenshots of the Machine Learning Studio interface for better guidance!*
