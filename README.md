<div align="center">
  <h1>Automated Model Training with Azure ML Studio</h1>
</div>

### 🧐 I. Overview

This is a no-code tutorial project that involves training a machine learning model using Automated ML/AutoML in Azure Machine Learning Studio. 

For demonstration purposes, this tutorial will train a simple classification model to predict whether a client will subscribe to a fixed-term deposit with a financial institution or not.
<br><br>
##

### 📋 II. Prerequisites

- Azure account & subscription.<br>
- Familiarity with basic Azure concepts such as resource groups, subscriptions, Azure Storage, Azure Compute, & some familiarity with Azure Machine Learning Studio is recommended.<br>
- Basic understanding of machine learning concepts such as supervised learning, classification, regression, & evaluation metrics.
<br><br>
##

### 🎓 III. Tutorial<br><br>

### 1. Create a workspace<br>

**Option 1: From the *Azure Machine Learning Studio***<br>

> ![Workspace Creation](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/fb3aab2d-b3b5-437d-8625-15b67ec79bba)

- Go to https://ml.azure.com.<br><br>
- In the left navigation pane, go to **Workspaces**, then click ``+ New``.<br><br>
- In the **Name** section, enter a name for your workspace. (***Note:** You can choose any name.*)<br><br>
- In the **Subscription** section, select the subscription you want to use for the workspace. (***Note:** You can choose any subscription you have.*)<br><br>
- In the **Resource group** section, select an existing resource group from your Azure account or create a new one by clicking ``Create new``. This resource group will store the instance for your Azure ML Studio workspace.<br><br>
- In the **Region** section, choose the region where you want your workspace to be deployed. (***Note:** Select a region based on accessibility & availability. For this project, it will be deployed in "East US 2" due to its high availability.*)<br><br>
- Click ``Create``.

<br>

**Option 2: From the *Azure Portal***<br>

> ![Option 2 - Workspace Creation](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/62327be5-aa8a-47ff-a582-b2d3a98061a6)

- Go to https://portal.azure.com.<br><br>
- Under **Azure services**, click ``Create a resource``.<br><br>
- Search for "Azure Machine Learning" & click on the **Azure Machine Learning** service, then click ``Create``.<br><br>
- In the **Subscription** section, select the subscription you want to use for the workspace. (***Note:** You can choose any subscription you have.*)<br><br>
- In the **Resource group** section, select an existing resource group from your Azure account or create a new one by clicking ``Create new``. This resource group will store the instance for your Azure ML Studio workspace.<br><br>
- In the **Name** section, enter a name for your workspace. (***Note:** You can choose any name.*)<br><br>
- In the **Region** section, choose the region where you want your workspace to be deployed. (***Note:** Select a region based on accessibility & availability. For this project, it will be deployed in "East US 2" due to its high availability.*)<br><br>
- Click ``Review + create``.<br><br>
- After passing the validation, click ``Create``.<br><br>
- After successful deployment, go to https://ml.azure.com.<br><br>
- In the left navigation pane, go to **Workspaces**.

<br>

### 2. Upload a dataset as a data asset

> ![Upload dataset](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/623cdba1-98f4-4573-9d5e-bdce024d6ef8)

- Go to the workspace you created.<br><br>
- In the left navigation pane, go to **Data**.<br><br>
- In the **Data** page, click ``+ Create``.<br><br>

> ![Data type to data source](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/916d5af2-ca40-460f-88d3-3cecf6847354)

- In the **Name** section, enter a name for your data asset (***Note:** You can choose any name, but for this project, it will be named "bankmarketing".*). Next, in the **Type** section, select the type of data stored in your dataset. (***Note:** For this project, the type of data we'll use is "Tabular".*). After that, click ``Next``.<br><br>
- Select the source from which your dataset will be imported by choosing a source for your data asset. (***Note:** For this project, we'll select "From local files".*). After that, click ``Next``.<br><br>

> ![demo](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/02132896-94f2-4e02-96f0-564606df2c65)

- In the **Datastore type** section, select the type of storage where your dataset will be stored. (***Note:** For this project, we'll use the default option, which is "Azure Blob Storage".*)<br><br>
- Select a datastore from the list of existing datastores or create a new one by clicking ``Create new datastore``. (***Note:** For this project, we'll use the default option, which is "workspaceblobstore".*). After that, click ``Next``.<br><br> 
- Select "Upload files" from the **Upload files or folder** drop-down, then upload your dataset. (***Note:** For this project, I recommend downloading & using this [dataset](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/dataset/bankmarketing_train.csv), as this is what we'll use.*). After the dataset has been uploaded, click ``Next``.<br><br> 

> ![demo22](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/c8427979-ef5b-448b-9d17-0d74dad9febc)

- In the **Data preview** section, verify that the data in the dataset is populated as follows.<br><br>
- Verify that the data is properly formatted. After you verify that the data is populated & properly formatted, click ``Next``. (***Note:** For this project, keep the data format as it is: **File format** set to "Delimited", **Delimiter** set to "Comma", **Column headers** set to "All files have same headers", **Encoding** set to "UTF-8", **Skip rows** set to "None", leave the **Dataset contains multi-line data** un-ticked*)<br><br>
- On **Schema**, ensure that the data **Type** of each column in the dataset is correct & modify the columns you want to include. After everything is verified, click ``Next``.<br><br>

> ![last part](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/assets/95956735/48749489-3b6c-402c-8508-c9b65e2ae614)
 
- On **Review**, ensure that all information matches what was previously configured for your data asset. Once everything is verified, click ``Create``.

<br>

### 3. Create an automated machine learning job

- In the left navigation pane, go to **Automated ML**, then click ``+ New Automated ML job``.<br><br> 
- In the **Job name** section, enter a name for your training job. (***Note:** You can choose any name, but for this project, you can simply name it "Deposit-Subscription-Prediction".*)<br><br>
- In the **Experiment name** section, select "Create new". (***Note:**  If this is your first time creating an experiment/job or you don't have any existing experiments, this section might be grayed out & defaulted to "Create new". If this is the case, leave it as is.*)<br><br> 
- In the **New experiment name** section, enter a name for your experiment. (***Note:** You can choose any name, but for this project, you can name it "Binary-Classification" since the model we will train is a binary classification model.*)<br><br>
- In the **Description** section, you can also put a description about your experiment. (**Optional**)<br><br>
- Click **Next**.<br><br>
- Select "Classification" from the **Select task type** drop-down. Then, in the **Select data** section, select the "bankmarketing" dataset we uploaded. After that, click **Next**.<br><br>
- In the **Target column** section, select "y (string)" as this column indicates whether the client subscribed to a term deposit or not, which corresponds to what we want our model to predict.<br><br>
- Select **View additional configuration settings** & ensure the following configurations to better control the training job: set **Primary metric** to "AUCWeighted", enable **Explain best model** & **Use all supported models**, ensure no models are checked in the **Blocked models** section, & leave the **Positive class label** section blank. After configuring these settings, click **Save**.<br><br>
- In the **Limits** dropdown, ensure the following configuration: set **Max nodes** to "6", set **Metric score threshold** to "0.8" (equivalent to 80%) since the model we're training is only a baseline model.<br><br>
- In the **Validation type** dropdown, select "k-fold cross-validation", then enter "2" as your **Number of cross validations**. (***Note:** This section is optional & may be left as is, but for this project, a k-fold cross-validation will be implemented.*)<br><br>
- Click **Next**.<br><br>
- In the **Select compute type** dropdown, select "Compute cluster".<br><br>
- In the **Select Azure ML compute cluster** section, either create a new compute cluster or select an existing one. If no compute cluster is available, you can create a new one by clicking ``+ New``
- If you decide to create one, select "East US 2" in  the **Location** dropdown. (***Note:** Select a region based on accessibility & availability. For this project, it will be deployed in "East US 2" due to its high availability.*)<br><br>
- In the **Virtual machine tier** section, select "Dedicated", then choose "CPU" as your **Virtual machine type**. (***Note:** You can opt for a "GPU" for faster training, but this may result in higher costs & quicker consumption of your Azure credits.*)<br><br>
- In the **Virtual machine size** section, select "Select from all options", then find & choose "Standard_DS12_v2" from the options. (***Note:** You may choose other virtual machine sizes based on your requirements, but for this tutorial, we will use "Standard_DS12_v2" as it offers a balanced combination of CPU, memory, & storage for most workloads.*)<br><br>
- Click **Next**.<br><br>
- In the **Compute name** section, enter a name for your compute & leave the other configurations as they are. (***Note:** You can choose any name, but for this project, you can simply name it "automl-compute".*)<br><br>
- Click **Create**.<br><br>
- Once you have successfully created a new compute cluster, select the newly created cluster in the **Select Azure ML compute cluster** dropdown & click **Next**.<br><br>
- Click **Submit training job**.<br><br>





 







