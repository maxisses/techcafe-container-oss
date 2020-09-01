---
description: Mit git clone oder ibmcloud dev
---

# Java Starter Anwendung erstellen

The `ibmcloud dev` tooling greatly cuts down on development time by generating application starters with all the necessary boilerplate, build and configuration code so that you can start coding business logic faster.

1. Start the `ibmcloud dev` wizard to create a new directory in the current working directory.

   ```text
   ibmcloud dev create
   ```

   You may be asked to target an organization and a space, follow the instructions on the CLI {:tip}

2. Select `Backend Service / Web App` &gt; `Java - MicroProfile / JavaEE` &gt; `Java Liberty App` to create a Java starter. \(To create a Node.js starter instead, use `Backend Service / Web App` &gt; `Node`&gt; `Node.js Web App with Express.js (Web App)` \)
3. Enter a **unique name** for your application such as `<your-initials>kubeapp`.
4. Select the **resource group** where your cluster has been created.
5. Do not add additional services.
6. Do not add a DevOps toolchain, select **manual deployment**.
7. Select **Helm-based** deployment target.

This generates a starter application complete with the code and all the necessary configuration files for local development and deployment to cloud on Cloud Foundry or Kubernetes.



\_\_\_\_\_\_\_\_\_\_\_ **NOT REQUIRED** but if you want to check where the code comes from\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

We dont use automation features \(integration with ci/cd; direct deployment to kubernetes / openshift\) "ibmcloud dev" provides, alternatively we could just do a git clone , which gets the repo that is behind the scaffold application we would build with the ibmcloud dev command. But it 

```text
git clone https://github.com/IBM/java-liberty-app
```



