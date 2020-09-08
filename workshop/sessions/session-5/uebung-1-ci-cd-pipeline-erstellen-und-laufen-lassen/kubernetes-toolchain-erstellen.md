# Kubernetes Toolchain erstellen - Pipeline Konfiguration



1. Click **Add a Tool** and click **Delivery Pipeline**.

   a. Type a name for your new pipeline.

   b. Click **Tekton**. 

   ![Pipeline type](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Select.png)

   c. Make sure that the **Show apps in the View app menu** checkbox is selected. All the apps that your pipeline creates are shown in the **View App** list on the toolchain's Overview page.

   d. Click **Create Integration** to add the Delivery Pipeline to your toolchain.

2. Click **Delivery Pipeline** to open the Tekton Delivery Pipeline dashboard. On the **Definitions** tab, complete these tasks:

   a. Click **Add** to add your repository.

   b. Specify the Git repo and URL that contains the Tekton pipeline definition and related artifacts. From the list, select the Git repo that you created earlier.

   c. Select the branch in your Git repo that you want to use. For this tutorial, use the default value.

   d. Specify the path to your pipeline definition within the Git repo. You can reference a specific definition within the same repo. For this tutorial, use the default value.

   e. Save your changes.

   ![Pipeline window](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Repo_Definition.png)

3. On the left, click **Worker**.

   a. Select the private worker that you want to use to run your Tekton pipeline on the associated cluster. Either select the private worker you set up in the previous steps, or select the **IBM Managed workers in Frankfurt** option.

   ![Worker tab](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Worker.png)

   b. Save your changes.

4. On the left, click **Triggers** &gt; **Add trigger** &gt; **Git Repository**. Associate the trigger with an event listener: 

   a. From the **Repository** list, select your repo.

   b. Select the **When a commit is pushed** checkbox, and in the **EventListener** field, make sure that **listener** is selected.

   ![Git Repository trigger](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Trigger.png)

   c. Click **Save**.

5. Click **Add trigger** and click **Manual**. Associate that trigger with an event listener:

   a. In the **EventListener** field, make sure that **listener** is selected.

   ![Manual trigger](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Manual_Trigger.png)

   b. Click **Save**.

   **Note:** Manual triggers run when you click **Run pipeline** and select the trigger. Git repository triggers run when the specified Git event type occurs for the specified Git repo and branch. The list of available event listeners is populated with the listeners that are defined in the pipeline code repo. 

6. On the left, click **Environment properties**, and define the environment properties for this tutorial. To add each property, click **Add property** and click **Text property**, except for apiKey, which is a secured property. Add these properties:

| Property | Value |
| :--- | :--- |
| apikey | &lt; ibmcloud iam api-key-create testtest &gt; |
| cluster | DRVTECHCAFE-X |
| clusterNamespace | default |
| clusterRegion | eu-de |
| registryNamespace | drvtechcaferegistry |
| registryRegion | eu-de |
| repository | &lt; repo link from "Definitions" tab &gt; |

![Environment properties](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Environment.png)

Click **Save**, and on the left, click **PipelineRuns**. Your toolchain is now set up.

