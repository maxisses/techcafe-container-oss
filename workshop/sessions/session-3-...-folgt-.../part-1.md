# Part 1:



## -- Überarbeitung folgt  --

### Create a Kubernetes cluster

{: \#create\_kube\_cluster} {: step}

 delivers powerful tools by combining Docker and Kubernetes technologies, an intuitive user experience, and built-in security and isolation to automate the deployment, operation, scaling, and monitoring of containerized apps in a cluster of compute hosts.

The major portion of this tutorial can be accomplished with a **Free** cluster. Two optional sections relating to Kubernetes Ingress and custom domain require a **Standard** cluster.

A minimal cluster with one \(1\) zone, one \(1\) worker node and the smallest available size \(**Flavor**\) is sufficient for this tutorial.

* Create the Kubernetes cluster:
  * For Kubernetes on VPC infrastructure, you are required to create a VPC and subnet\(s\) prior to creating the Kubernetes cluster. You may follow the instructions provided under the [Creating a standard VPC Gen 1 compute cluster in the console](https://{DomainName}/docs/containers?topic=containers-clusters#clusters_vpc_ui).
  * For Kubernetes on Classic infrastructure follow the [Creating a standard classic cluster](https://{DomainName}/docs/containers?topic=containers-clusters#clusters_standard) instructions.

    {: \#create\_cluster}

### Create a starter application

{: \#create\_application} {: step}

The `ibmcloud dev` tooling greatly cuts down on development time by generating application starters with all the necessary boilerplate, build and configuration code so that you can start coding business logic faster.

1. Start the `ibmcloud dev` wizard to create a new directory in the current working directory.

   ```text
   ibmcloud dev create
   ```

   {: pre}

   You may be asked to target an organization and a space, follow the instructions on the CLI {:tip}

2. Select `Backend Service / Web App` &gt; `Java - MicroProfile / JavaEE` &gt; `Java Liberty App` to create a Java starter. \(To create a Node.js starter instead, use `Backend Service / Web App` &gt; `Node`&gt; `Node.js Web App with Express.js (Web App)` \)
3. Enter a **unique name** for your application such as `<your-initials>kubeapp`.
4. Select the **resource group** where your cluster has been created.
5. Do not add additional services.
6. Do not add a DevOps toolchain, select **manual deployment**.
7. Select **Helm-based** deployment target.

This generates a starter application complete with the code and all the necessary configuration files for local development and deployment to cloud on Cloud Foundry or Kubernetes.

![](https://github.com/maxisses/firstgitbook/tree/5b5370a9d28ef3477285a814c57784ecc17465be/workshop/sessions/images/solution2/Contents.png)

### Deploy application to cluster using helm chart

{: \#deploy} {: step}

In this section, you first push the Docker image to the IBM Cloud private container registry, and then create a Kubernetes deployment pointing to that image.

#### Prepare the access to 

1. To identify your  URL, run

   ```bash
   ibmcloud cr region
   ```

   {:pre}

2. Define an environment variable named `MYREGISTRY` pointing to the URL such as:

   ```bash
   export MYREGISTRY=us.icr.io
   ```

   {:pre}

3. Pick one of your existing registry namespaces or create a new one. To list existing namespaces, use:

   ```bash
   ibmcloud cr namespaces
   ```

   {:pre}

   To create a new namespace:

   ```bash
   ibmcloud cr namespace-add <REGISTRY_NAMESPACE>
   ```

   {:pre}

4. Define an environment variable named `MYNAMESPACE` pointing to the registry namespace:

   ```bash
   export MYNAMESPACE=<REGISTRY_NAMESPACE>
   ```

   {:pre}

#### Build the container image

1. Define an environment variable named `MYPROJECT` set with the name of the application you generated in the previous section:

   ```bash
   export MYPROJECT=<your-initials>kubeapp
   ```

   {:pre}

2. Change to the directory of the generated project.

   ```text
   cd $MYPROJECT
   ```

   {: pre}

3. Ensure your local Docker engine is started.

   ```text
   docker ps
   ```

   {: pre}

4. Build, tag \(`-t`\) and push the docker image to your container registry on IBM Cloud

   ```bash
   ibmcloud cr build -t $MYREGISTRY/$MYNAMESPACE/$MYPROJECT:v1.0.0 .
   ```

   {: pre}

#### Deploy the application

1. Gain access to your cluster as described on the Access tab of your cluster.

   For more information on gaining access to your cluster and to configure the CLI to run kubectl commands, check the [CLI configure](https://github.com/maxisses/firstgitbook/tree/5b5370a9d28ef3477285a814c57784ecc17465be/docs/containers?topic=containers-cs_cli_install/README.md#cs_cli_configure) section {:tip}

2. Initialize the environment variable with the cluster name

   ```bash
   export MYCLUSTER=<CLUSTER_NAME>
   ```

[Helm](https://helm.sh/) helps you manage Kubernetes applications through Helm Charts, which helps define, install, and upgrade even the most complex Kubernetes application.

**With Helm 2**

1. Install Helm into your cluster [by following steps 2\) and 3\) on how to configure tiller and initialize Helm](https://{DomainName}/docs/containers?topic=containers-helm#public_helm_install).
2. Change to the chart directory:

   ```bash
   cd chart/$MYPROJECT
   ```

   {:pre}

3. Install the chart:

   ```bash
   helm install . --name ${MYPROJECT} --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
   ```

   {:pre}

**With Helm 3**

1. Change to the chart directory:

   ```bash
   cd chart/$MYPROJECT
   ```

   {:pre}

2. Install the chart:

   ```bash
   helm install ${MYPROJECT} . --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
   ```

   {:pre}

#### View the application

1. List the Kubernetes services in the namespace:

   ```bash
   kubectl get services
   ```

   {:pre}

2. Locate the service linked to your application. It is named after your project.

   If your project name contains hyphens, they may have been removed by the chart, e.g `my-project` would become `myproject`.

3. Make note of the the public port the service is listening on. The port is a 5-digit number\(e.g., 31569\) under `PORT(S)`.
4. Identify a public IP of a worker node with the command below:

   ```bash
   ibmcloud ks workers --cluster ${MYCLUSTER}
   ```

   {: pre}

5. Access the application at `http://worker-ip-address:portnumber/`. For VPC the IP addresses of the clusters are private to the VPC. These can be accessed by opening the **Web Terminal** from the Kubernetes cluster console UI.  See [Using the Kubernetes web terminal in your web browser](https://{DomainName}/docs/containers?topic=containers-cs_cli_install#cli_web)

### Use the IBM-provided domain for your cluster

{: \#ibm\_domain} {: step}

In the previous step, the application was accessed with a not standard port. The service was exposed by way of Kubernetes NodePort feature.

Paid clusters come with an IBM-provided domain. This gives you a better option to expose applications with a proper URL and on standard HTTP/S ports.

Use Ingress to set up the cluster inbound connection to the service.

![Ingress](https://github.com/maxisses/firstgitbook/tree/5b5370a9d28ef3477285a814c57784ecc17465be/workshop/sessions/images/solution2/Ingress.png)

1. Identify your IBM-provided **Ingress domain**

   ```bash
   ibmcloud ks cluster get --cluster ${MYCLUSTER}
   ```

   {: pre}

   to find

   ```yaml
   Ingress subdomain: mycluster.us-south.containers.appdomain.cloud
   Ingress secret:    mycluster
   ```

   {: screen}

2. Create an Ingress file `ingress-ibmdomain.yml` pointing to your domain with support for HTTP and HTTPS. Use the following file as a template, replacing all the values wrapped in &lt;&gt; with the appropriate values from the above output. **service-name** is the name under `==> v1/Service` in the above step. You can also use `kubectl get svc` to find the service name of type **NodePort**.

   ```yaml
   apiVersion: extensions/v1beta1
   kind: Ingress
   metadata:
     name: ingress-for-ibmdomain-http-and-https
   spec:
     tls:
     - hosts:
       -  <nameofproject>.<ingress-sub-domain>
       secretName: <ingress-secret>
     rules:
     - host: <nameofproject>.<ingress-sub-domain>
       http:
         paths:
         - path: /
           backend:
             serviceName: <service-name>
             servicePort: 9080
   ```

   {: codeblock}

3. Deploy the Ingress

   ```bash
   kubectl apply -f ingress-ibmdomain.yml
   ```

   {: pre}

4. Access your application at `https://<nameofproject>.<ingress-sub-domain>/`

### Use your own custom domain

{: \#custom\_domain} {: step}

This section requires you to own a custom domain and to be able to modify the DNS records of the domain. You will need to create a `CNAME` record pointing to the IBM-provided domain.

See [Using the Ingress controller with a custom domain](https://{DomainName}/docs/containers?topic=containers-ingress#ingress) for more information.

#### with HTTP

1. Create an Ingress file `ingress-customdomain-http.yml` pointing to your domain:

   ```yaml
   apiVersion: extensions/v1beta1
   kind: Ingress
   metadata:
     name: ingress-for-customdomain-http
   spec:
     rules:
     - host: <my-custom-domain.com>
       http:
         paths:
         - path: /
           backend:
             serviceName: <service-name>
             servicePort: 9080
   ```

   {: codeblock}

2. Deploy the Ingress

   ```bash
   kubectl apply -f ingress-customdomain-http.yml
   ```

   {: pre}

3. Access your application at `http://<my-custom-domain.com>/`

#### with HTTPS

If you were to try to access your application with HTTPS at this time `https://<my-custom-domain.com>/`, you will likely get a security warning from your web browser telling you the connection is not private. You would also get a 404 as the Ingress just configured would not know how to direct HTTPS traffic.

1. Obtain a trusted SSL certificate for your domain. You'll need the certificate and the key as described [here](https://{DomainName}/docs/containers?topic=containers-ingress#public_inside_3). To generate a trusted certificate, you can either use [Let's Encrypt](https://letsencrypt.org/) or .
2. Save the cert and the key in base64 ascii format files.
3. Create a TLS secret to store the cert and the key:

   ```bash
   kubectl create secret tls my-custom-domain-secret-name --cert=<custom-domain.cert> --key=<custom-domain.key>
   ```

   {: pre}

4. Create an Ingress file `ingress-customdomain-https.yml` pointing to your domain:

   ```yaml
   apiVersion: extensions/v1beta1
   kind: Ingress
   metadata:
     name: ingress-customdomain-https
   spec:
     tls:
     - hosts:
       - <my-custom-domain.com>
       secretName: <my-custom-domain-secret-name>
     rules:
     - host: <my-custom-domain.com>
       http:
         paths:
         - path: /
           backend:
             serviceName: <service-name>
             servicePort: 9080
   ```

   {: codeblock}

5. Deploy the Ingress:

   ```bash
   kubectl apply -f ingress-customdomain-https.yml
   ```

   {: pre}

6. Access your application at `https://<my-custom-domain.com>/`.

### Monitor application health

{: \#monitor\_application} {: step}

1. To check the health of your application, navigate to [clusters](https://{DomainName}/kubernetes/clusters) to see a list of clusters and click on your cluster.
2. Click **Kubernetes Dashboard** to launch the dashboard in a new tab.
3. Select **Nodes** on the left pane, click the **Name** of the nodes and see the **Allocation Resources** to see the health of your nodes.
4. To review the application logs from the container, select **Pods**, **pod-name** and **Logs**.
5. To **ssh** into the container, identify your pod name from the previous step and run

   ```bash
   kubectl exec -it <pod-name> -- bash
   ```

   {: pre}

### Scale Kubernetes pods

{: \#scale\_cluster} {: step}

As load increases on your application, you can manually increase the number of pod replicas in your deployment. Replicas are managed by a [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/). To scale the application to two replicas, run the following command:

```bash
kubectl scale deployment <deployment-name> --replicas=2
```

{: pre}

After a shortwhile, you will see two pods for your application in the Kubernetes dashboard \(or with `kubectl get pods`\). The Ingress controller in the cluster will handles the load balancing between the two replicas.

With Kubernetes, you can enable [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to automatically increase or decrease the number of instances of your apps based on CPU.

To create an autoscaler and to define your policy, run the below command

```bash
kubectl autoscale deployment <deployment-name> --cpu-percent=<percentage> --min=<min_value> --max=<max_value>
```

{: pre}

Once the autoscaler is successfully created, you should see `horizontalpodautoscaler.autoscaling/<deployment-name> autoscaled`

Refer to [scaling apps](https://{DomainName}/docs/containers?topic=containers-app#app_scaling) for prerequisites and additional info.

### Remove resources

{: step}

* Delete the Kubernetes artifacts created for this application:

  ```bash
   helm delete ${MYPROJECT}
  ```

   {:pre}

* Delete the cluster.

### Related content

* [IBM Cloud Kubernetes Service](https://{DomainName}/docs/containers?topic=containers-container_index#container_index)
* [Continuous Deployment to Kubernetes](https://{DomainName}/docs/solution-tutorials?topic=solution-tutorials-continuous-deployment-to-kubernetes#continuous-deployment-to-kubernetes)
* [Scaling a deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment)
* [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/)

