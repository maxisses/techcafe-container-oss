# SetUp checken

Check whether your provided cluster is available.

```text
ibmcloud cs clusters
```

Create the API key by using the string that is provided for your key name.

```text
ibmcloud iam api-key-create <my api key name>
```

Save the API key value that is provided by the command.

We stick to namespace from the last Session:

`ibmcloud cr namespaces`

Alternatively, you can create a namespace on the [Container Registry page](https://cloud.ibm.com/kubernetes/registry/main/namespaces?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-namespaces).

