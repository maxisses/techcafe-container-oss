# Manueller PipelineRun um die Pipeline zu untersuchen

With a Tekton-based delivery pipeline, you can automate the continuous building, testing, and deployment of your apps.

The Tekton Delivery Pipeline dashboard displays an empty table until at least one Tekton pipeline runs. After a Tekton pipeline runs, either manually or as the result of external Git events, the table lists the run, its status, and the last updated time of the run definition.

To run the manual trigger that you set up in the previous task, click **Run pipeline** and select the name of the manual trigger that you created. The pipeline starts to run and you can see the progress on the dashboard. Pipeline runs can be in any of the following states:

* Pending: The PipelineRun definition is queued and waiting to run.
* Running: The PipelineRun definition is running in the cluster.
* Succeeded: The PipelineRun definition was successfully completed in the cluster.
* Failed: The PipelineRun definition run failed. Review the log file for the run to determine the cause.

  ![Pipeline dashboard](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Pipeline_Dashboard.png)

For more information about a selected run, click any row in the table. You view the Task definition and the steps in each PipelineRun definition. You can also view the status, logs, and details of each Task definition and step, and the overall status of the PipelineRun definition.

![Pipeline Log](https://www.ibm.com/cloud/architecture/images/tutorials/toolchains/develop-kubernetes-app-using-tekton-delivery-pipelines/Pipeline_Details.png)

The pipeline definition is stored in the `pipeline.yaml` file in the `.tekton` folder of your Git repository. Each task has a separate section of this file. The steps for each task are defined in the `tasks.yaml` file.

