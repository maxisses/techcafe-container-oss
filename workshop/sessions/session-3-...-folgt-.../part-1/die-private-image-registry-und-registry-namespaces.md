# Die private Image Registry und Registry Namespaces

In this section, you push the Docker image to the IBM Cloud private container registry.

#### Prepare the access to the private image registry.

1. To identify your  URL, run

   ```bash
   ibmcloud cr region
   ```

2. Define an environment variable named `MYREGISTRY` pointing to the URL such as:

   ```bash
   export MYREGISTRY=us.icr.io
   ```

3. Pick one of your existing registry namespaces or create a new one. To list existing namespaces, use:

   ```bash
   ibmcloud cr namespaces
   ```



   To create a new namespace:

   ```bash
   ibmcloud cr namespace-add <REGISTRY_NAMESPACE>
   ```

4. Define an environment variable named `MYNAMESPACE` pointing to the registry namespace:

   ```bash
   export MYNAMESPACE=<REGISTRY_NAMESPACE>
   ```

