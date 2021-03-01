# Die Applikation über NodePort anschauen



1. List the Kubernetes services in the namespace:

   ```bash
   kubectl get services
   ```

2. Locate the service linked to your application. It is named after your project.

   If your project name contains hyphens, they may have been removed by the chart, e.g `my-project` would become `myproject`.

3. Make note of the the public port the service is listening on. The port is a 5-digit number\(e.g., 31569\) under `PORT(S)`.
4. Identify a public/external IP of a worker node with the command below:

   ```bash
   kubectl get nodes -o wide
   ```

5. Access the application at `http://worker-ip-address:portnumber/`.

