# GitHook & Code Änderung

In this task, you modify the application and redeploy it. You can see how your Tekton-based delivery pipeline automatically picks up the changes in the application on commit and redeploys the app.

1. On the toolchain's Overview page, click the Git tile for your application.

   **Tip:** You can also use the built-in Eclipse Orion-based Web IDE, a local IDE, or your favorite editor to change the files in your repo.

2. In the repository directory tree, open the `app.js` file.

   ![File browser](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Files.png)

3. Edit the text message code to change the welcome message.

   ![Edit file](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Commit.png)

4. Commit the updated file by typing a commit message and clicking **Commit changes** to push the change to the project's remote repository.
5. Return to the toolchain's Overview page by clicking the back arrow.
6. Click **Delivery Pipeline**. The pipeline is running because the commit automatically started a build. Over the next few minutes, watch your change as it is built, tested, and deployed.

   ![Dashboard redeployment](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Redeploy.png)

7. After the deploy-to-kubernetes step is completed, refresh your application URL. The updated message is shown.

