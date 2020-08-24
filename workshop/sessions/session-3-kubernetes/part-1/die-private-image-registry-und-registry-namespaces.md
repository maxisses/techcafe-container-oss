# Die private Image Registry und Registry Namespaces

In this section, you push the Docker image to the IBM Cloud private container registry.

#### Prepare the access to the private image registry.

1. To identify your  URL, run

   ```bash
   ibmcloud cr region
   ```

2. Define an environment variable named `MYREGISTRY` pointing to the URL such as:

   ```bash
   export MYREGISTRY=de.icr.io
   ```

3. Pick one of your existing registry namespaces or create a new one. To list existing namespaces, use:

   ```bash
   ibmcloud cr namespaces
   ```

{% hint style="info" %}


To create a new namespace \(on your own account\):

```bash
ibmcloud cr namespace-add <REGISTRY_NAMESPACE>
```
{% endhint %}

1. Define an environment variable named `MYNAMESPACE` pointing to the registry namespace. Use the provided namespace: drvtechcaferegistry

   ```bash
   export MYNAMESPACE=drvtechcaferegistry
   ```

