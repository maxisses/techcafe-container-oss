# Deployment nach Kubernetes mit HELM

## Deploy the application

1. Gain access to your cluster as described on the Access tab of your cluster \("connect via CLI" at the right top in the screenshot\).

![](../../../.gitbook/assets/image%20%2858%29.png)

{% hint style="info" %}
For more information on gaining access to your cluster and to configure the CLI to run kubectl commands, check the [CLI configure](https://github.com/maxisses/firstgitbook/tree/5b5370a9d28ef3477285a814c57784ecc17465be/docs/containers?topic=containers-cs_cli_install/README.md#cs_cli_configure) section
{% endhint %}

1. Initialize the environment variable with the cluster name \(DRVTECHCAFE-X\) - X is your number-

   ```bash
   export MYCLUSTER=<CLUSTER_NAME>
   ```

[Helm](https://helm.sh/) helps you manage Kubernetes applications through Helm Charts, which helps define, install, and upgrade even the most complex Kubernetes application.

**Mit Helm 3**

1. Change to the chart directory:

   ```bash
   cd chart/$MYPROJECT
   ```

2. Install the chart:

   ```bash
   helm install ${MYPROJECT} . --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
   ```

