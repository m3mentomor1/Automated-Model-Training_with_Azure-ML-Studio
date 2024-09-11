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

### 🎓 III. Tutorial<br>

#### Contents:
[1. Create a workspace](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/README.md#1-create-a-workspace)<br>
[2. Upload a dataset as a data asset](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/README.md#2-upload-a-dataset-as-a-data-asset)<br>
[3. Create an automated machine learning job](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/README.md#3-create-an-automated-machine-learning-job)<br>
[4. Explore trained model/s]()<br>
[5. Deploy & test trained model/s]()<br><br>


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
- Select "Upload files" from the **Upload files or folder** drop-down, then upload your . (***Note:** For this project, I recommend downloading & using this [dataset](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/dataset/bankmarketing_train.csv), as this is what we'll use.*). After the dataset has been uploaded, click ``Next``.<br><br> 

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
- Click ``Next``.<br><br>
- Select "Classification" from the **Select task type** drop-down. Then, in the **Select data** section, select the "bankmarketing" dataset we uploaded. After that, click **Next**.<br><br>
- In the **Target column** section, select "y (string)" as this column indicates whether the client subscribed to a term deposit or not, which corresponds to what we want our model to predict.<br><br>
- Select **View additional configuration settings** & ensure the following configurations to better control the training job: set **Primary metric** to "AUCWeighted", enable **Explain best model** & **Use all supported models**, ensure no models are checked in the **Blocked models** section, & leave the **Positive class label** section blank. After configuring these settings, click **Save**.<br><br>
- In the **Limits** dropdown, ensure the following configuration: set **Max nodes** to "6", set **Metric score threshold** to "0.8" (equivalent to 80%) since the model we're training is only a baseline model.<br><br>
- In the **Validation type** dropdown, select "k-fold cross-validation", then enter "2" as your **Number of cross validations**. (***Note:** This section is optional & may be left as is, but for this project, a k-fold cross-validation will be implemented.*)<br><br>
- Click ``Next``.<br><br>
- In the **Select compute type** dropdown, select "Compute cluster".<br><br>
- In the **Select Azure ML compute cluster** section, either create a new compute cluster or select an existing one. If no compute cluster is available, you can create a new one by clicking ``+ New``
- If you decide to create one, select "East US 2" in  the **Location** dropdown. (***Note:** Select a region based on accessibility & availability. For this project, it will be deployed in "East US 2" due to its high availability.*)<br><br>
- In the **Virtual machine tier** section, select "Dedicated", then choose "CPU" as your **Virtual machine type**. (***Note:** You can opt for a "GPU" for faster training, but this may result in higher costs & quicker consumption of your Azure credits.*)<br><br>
- In the **Virtual machine size** section, select "Select from all options", then find & choose "Standard_DS12_v2" from the options. (***Note:** You may choose other virtual machine sizes based on your requirements, but for this tutorial, we will use "Standard_DS12_v2" as it offers a balanced combination of CPU, memory, & storage for most workloads.*)<br><br>
- Click ``Next``.<br><br>
- In the **Compute name** section, enter a name for your compute & leave the other configurations as they are. (***Note:** You can choose any name, but for this project, you can simply name it "automl-compute".*)<br><br>
- Click ``Create``.<br><br>
- Once you have successfully created a new compute cluster, select the newly created cluster in the **Select Azure ML compute cluster** dropdown & click **Next**.<br><br>
- Click **Submit training job**.<br><br>
- To monitor the training progress, navigate to the **Jobs** tab under **Assets** in the left navigation pane, then click on "Deposit-Subscription-Prediction." You can check the training status under the **Status** section. If it says "Completed," your model/s have finished training. (***Note:** With our current training job setup & dataset, the training process could take anywhere from 15 minutes to 1 hour under typical conditions. However, these are general estimates, & the actual time may vary.*)

<br>

### 4. Explore trained model/s
- To explore the models you've trained, go to the **Jobs** tab in the **Assets** section of the left navigation pane, then select the "Deposit-Subscription-Prediction" job.<br><br>
- First, we can check the evaluation metrics of the model/s in the **Models & Child Jobs** tab. Then, click on the name of the model's algorithm, which is "MaxAbsScaler, LightGBM".<br><br>
- Under **Model Summary** > **AUC Weighted**, you can see the score that represents the model's overall performance in distinguishing between positive & negative classes. Since "AUC Weighted" is the primary metric used in this job, a higher AUC value indicates better model performance.<br><br>
- Aside from **AUC Weighted**, you can also view other metrics by clicking **View all other metrics** or go to the **Metrics** tab. (***Note:** If you don't see any metric in the **Metrics** tab just click ``🗘 Refresh``.*)<br><br>
- In the **Metrics** tab, you can filter & view only the metrics you want by using the **Select Metrics** panel on the left side. (***Note:** Click the double-arrow button pointing to the right next to the "Select Metrics" text to access the filtering options.*)<br><br>
- Back to the **Model** tab, you can also view the hyperparameters used to improve the performance of the model/s under **Model Summary** > **AUC Weighted** > **View hyperparameters**.<br><br>
- You can also view an explanation of the model/s & see which data features (raw or engineered) influenced a particular model's predictions in the **Explanations (preview)** tab.<br><br>
- Test predictions can also be performed in the **Test results (preview)** tab. In this tab, click **Test model (preview)** & configure the following settings: set **Select compute type** to "Compute cluster," set **Select Azure ML compute cluster** to "automl-compute," & choose the dataset you want to use under **Select a dataset**, then click ``Test``. (***Note:** Ensure you have a test dataset available for making predictions. It is recommended to use a different dataset than the one used to train the model.*)<br><br>
- You can monitor the progress of the testing in the table within the **Test results (preview)** tab. If the table is empty, simply click ``🗘 Refresh`` to update the view. Once the testing is complete, you will see the testing job's AUC score result in the "AUC Weighted" column, & the status will indicate "Completed".
 
<br>

### 5. Deploy & test trained model/s
- Using the Automated ML/AutoML interface, you can also deploy the models you trained by clicking ``▷ Deploy``. (***Note:** Ensure you are still in **Assets** > **Jobs** > "Deposit-Subscription-Prediction" > **Models and Child Jobs** > "MaxAbsScaler, LightGBM" to see the ``▷ Deploy`` dropdown button.*)<br><br>
-  In the ``▷ Deploy`` dropdown button, select "Real-time endpoint". (***Note:** For this tutorial, we will select the "Real-time endpoint" option to enable individual real-time predictions.*)<br><br>
- If you don't have an existing endpoint, select the "New" option & leave the configured settings as they are, then click ``Deploy``. If you have an existing endpoint, select the "Existing" option & choose the desired endpoint from the **Endpoint name** dropdown.<br><br>
- To check the endpoint's deployment status, navigate to **Assets** > **Endpoints** & click the name of the endpoint you just created. If it is successfully deployed the **Provisioning state** under **Endpoint attributes** section will indicate "Succeeded".<br><br>
- After the deployment of the endpoint, you can also check check model's deployment status by navigating to **Assets** > **Endpoints** & click the name of the endpoint you just created. If it is successfully deployed, the **Provisioning state** under the **Deployment <deployment_name>** section will indicate "Succeeded".<br><br>
- To test the deployed model & predict whether a client will subscribe to a fixed-term deposit with a financial institution or not, navigate to the **Test** tab & input data in JSON format in the **Sample inference** > **Input** editor. (***Note:** For your convenience, you can use this example [input data](https://github.com/m3mentomor1/Automated-Model-Training_with_Azure-ML-Studio/blob/main/example-input-data.txt). This also includes an explanation of each column to give you an idea on why each input data is used.*)<br><br>
- To view the prediction results, scroll-down to the bottom & see the results in the **jsonOutput** section. 







 







