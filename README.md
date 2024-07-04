<div align="center">
  <h1>Automated Model Training with Azure ML Studio</h1>
</div>

### 🧐 I. Overview

This is a no-code tutorial project that involves training a machine learning model using Automated ML/AutoML in Azure Machine Learning Studio. 

For demonstration purposes, this tutorial will train a simple classification model to predict whether a client will subscribe to a fixed-term deposit with a financial institution or not.
<br><br>
##

### 📋 II. Prerequisites

- Azure account and subscription.<br>
- Familiarity with basic Azure concepts such as resource groups, subscriptions, Azure Storage, Azure Compute, and some familiarity with Azure Machine Learning Studio is recommended.<br>
- Basic understanding of machine learning concepts such as supervised learning, classification, regression, and evaluation metrics.
<br><br>
##

### 🎓 III. Tutorial<br><br>

**1. Create a workspace**<br>

**Option 1: From the *Azure Machine Learning Studio* website**<br>

> ![Workspace Creation](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/fb3aab2d-b3b5-437d-8625-15b67ec79bba)

- Go to https://ml.azure.com.<br><br>
- In the left navigation pane, go to **Workspaces**, then click ``+ New``.<br><br>
- In the **Name** section, enter a name for your workspace. (***Note:** You can choose any name.*)<br><br>
- In the **Subscription** section, select the subscription you want to use for the workspace. (***Note:** You can choose any subscription you have.*)<br><br>
- In the **Resource group** section, select an existing resource group from your Azure account or create a new one by clicking ``Create new``. This resource group will store the instance for your Azure ML Studio workspace.<br><br>
- In the **Region** section, choose the region where you want your workspace to be deployed. (***Note:** Select a region based on accessibility and availability. For this project, it will be deployed in "East US 2" due to its high availability.*)<br><br>
- Click ``Create``.

**Option 2: From the main *Azure* portal**<br>

>

- Go to https://portal.azure.com.<br><br>
- 

<br>

**2. Upload a dataset:**

- In the **Assets** section, go to **Data**.<br><br>
- In the **Data** page, click ``+ Create``.<br><br>
- In the **Name** section, enter a name for your data asset (***Note:** You can choose any name, but for this project, it will be named "bankmarketing".*). Next, in the **Type** section, select the type of data stored in your dataset. (***Note:** For this project, the type of data we'll use is "Tabular".*). After that, click ``Next``.<br><br>
- Select the source from which your dataset will be imported by choosing a source for your data asset. (***Note:** For this project, we'll select "From local files".*). After that, click ``Next``.<br><br>
- In the **Datastore type** section, select the type of storage where your dataset will be stored. (***Note:** For this project, we'll use the default option, which is "Azure Blob Storage".*)<br><br>
- Select a datastore from the list of existing datastores or create a new one by clicking ``Create new datastore``. (***Note:** For this project, we'll use the default option, which is "workspaceblobstore".*). After that, click ``Next``.<br><br> 
- Select "Upload files" from the **Upload files or folder** drop-down, then upload your dataset. (***Note:** For this project, I recommend downloading and using this [dataset](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/bankmarketing_train.csv), as this is what we'll use.*). After the dataset has been uploaded, click ``Next``.<br><br> 
- 

<br>

**3. Create an automated Machine Learning job** 


 


 







