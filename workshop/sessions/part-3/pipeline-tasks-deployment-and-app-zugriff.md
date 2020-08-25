# Pipeline Tasks, Deployment & App Zugriff



1. Review the pipeline-build-task. The task consists of a git clone of the repository followed by two steps:
   * pre-build-check: This step checks for the mandatory Dockerfile and runs a lint tool. It then checks the registry current plan and quota before it creates the image registry namespace if needed.
   * build-docker-image: This step creates the Docker image by using the IBM Cloud Container Registry build service through the `ibmcloud cr build` CLI script. The script stores the output image into the private IBM Cloud Container Registry and copies other app scripts with the build results into the `ARCHIVE_DIR` folder.
2. Review the pipeline-validate-task. The task consists of a git clone of the repository, followed by the check-vulnerabilities step. This step runs the [IBM Cloud Vulnerability Advisor](https://cloud.ibm.com/docs/va?topic=va-va_index#about&cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-vulnerability-advisor-docs) on the image to check for known vulnerabilities. If it finds a vulnerability, the job fails, preventing the image from being deployed. This safety feature prevents apps with security holes from being deployed. The image has no vulnerabilities, so it passes. In this tutorial template, the default configuration of the job is to not block on failure.
3. Review the pipeline-deploy-task. The task consists of a git clone of the repository followed by two steps:
   * pre-deploy-check: This step checks whether the IBM Container Service cluster is ready and has a namespace that is configured with access to the private image registry by using an IBM Cloud API Key. This step also configures the Helm Tiller service to later run a deployment with Helm.
   * deploy-to-kubernetes: This step checks for cluster readiness and namespace existence, configures the cluster namespace, updates the `deployment.yml` manifest file, and grants access to the private image registry. It also sets environment variables and uses the deployment manifest file to deploy the app into the Kubernetes cluster.
4. After all the steps in the pipeline are completed, a green status is shown for each task. Click the **deploy-to-kubernetes** step and click the **Logs** tab to see the successful completion of this step.

   ![Pipeline success](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Success.png)

5. Scroll to the end of the log. The `DEPLOYMENT SUCCEEDED` message is shown at the end of the log.

   ![Deployment succeeded](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_Deployment_Success.png)

6. Click the URL to see the running application.

   ![Running app](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Tekton_App.png)

