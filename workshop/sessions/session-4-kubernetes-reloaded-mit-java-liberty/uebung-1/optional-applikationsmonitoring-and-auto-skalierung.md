# optional: Applikationsmonitoring & Auto-Skalierung

### Monitor application health

1. To check the health of your application, navigate to [clusters](https://{DomainName}/kubernetes/clusters) to see a list of clusters and click on your cluster.
2. Click **Kubernetes Dashboard** to launch the dashboard in a new tab.
3. Select **Nodes** on the left pane, click the **Name** of the nodes and see the **Allocation Resources** to see the health of your nodes.
4. To review the application logs from the container, select **Pods**, **pod-name** and **Logs**.
5. To **ssh** into the container, identify your pod name from the previous step and run

   ```bash
   kubectl exec -it <pod-name> -- bash
   ```

### Scale Kubernetes pods

As load increases on your application, you can manually increase the number of pod replicas in your deployment. Replicas are managed by a [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/). To scale the application to two replicas, run the following command:

```bash
kubectl scale deployment <deployment-name> --replicas=2
```

After a shortwhile, you will see two pods for your application in the Kubernetes dashboard \(or with `kubectl get pods`\). The Ingress controller in the cluster will handles the load balancing between the two replicas.

With Kubernetes, you can enable [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to automatically increase or decrease the number of instances of your apps based on CPU.

To create an autoscaler and to define your policy, run the below command

```bash
kubectl autoscale deployment <deployment-name> --cpu-percent=<percentage> --min=<min_value> --max=<max_value>
```

Once the autoscaler is successfully created, you should see `horizontalpodautoscaler.autoscaling/<deployment-name> autoscaled`

Refer to [scaling apps](https://{DomainName}/docs/containers?topic=containers-app#app_scaling) for prerequisites and additional info.

### Remove resources

* Delete the Kubernetes artifacts created for this application:

  ```bash
   helm delete ${MYPROJECT}
  ```

