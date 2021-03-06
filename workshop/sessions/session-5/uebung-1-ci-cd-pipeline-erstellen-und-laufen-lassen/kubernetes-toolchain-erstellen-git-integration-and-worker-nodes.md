# Kubernetes Toolchain erstellen - Git Integration

In this task, you create a toolchain and add the tools that you need for this Session. Before you begin, you need your API key and Kubernetes cluster name.

1. Create your toolchain by following one of these options:
   * Open the toolchain creation page by clicking **Create toolchain**.

     ```text
       [![Create Toolchain](https://cloud.ibm.com/devops/graphics/create_toolchain_button.png)](https://cloud.ibm.com/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain&env_id=ibm:yp:us-east)
     ```

   * Go to [cloud.ibm.com](https://cloud.ibm.com/?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-ibm-bluemix-website). Open the menu in the upper-left corner and click **DevOps**. Click **Create a Toolchain**. Click **Build Your Own Toolchain**.

     ![Build your own toolchain](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Blank_Template.png)

We have a cluster there for you, so if you go to [cloud.ibm.com](https://cloud.ibm.com/?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-ibm-bluemix-website) you could alternatively Open the menu in the upper-left corner and click **Kubernetes**. Click **Clusters** and click your cluster. On the cluster dashboard, click the **DevOps** tab and click **Create a Toolchain**. Click **Build Your Own Toolchain**.

\*\*\*\*

1. On the "Build your own toolchain" page, review the default information for the toolchain settings. The toolchain's name identifies it in IBM Cloud. Make sure that the toolchain's name is unique within IBM Cloud. Each toolchain is associated with a specific region and resource group. From the menus on the page, select the region and resource group where you want to create the toolchain. You can have up to 200 toolchains per resource group.

   ![Select\_Region](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Region_Select.png)

2. Click **Create**. The blank toolchain is created.

   ![Blank\_Toolchain](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Blank_Toolchain.png)

3. Click **Add a Tool** and click **Git Repos and Issue Tracking**.

   ![Git Repos tile](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Add_Tool_Git.png)

   a. From the **Repository type** list, select **Clone**.

   b. In the **Source repository URL** field, type [`https://github.com/maxisses/hello-tekton`](https://github.com/maxisses/hello-tekton.git).

   c. Make sure that the **Make this repository private** checkbox is cleared and that the **Track deployment of code changes** checkbox is selected.

   ![Git window](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Git_Setup.png)

   d. Click **Create Integration**. Tiles for Git Issues and Git Code are added to your toolchain.

4. Return to your toolchain's overview page.

