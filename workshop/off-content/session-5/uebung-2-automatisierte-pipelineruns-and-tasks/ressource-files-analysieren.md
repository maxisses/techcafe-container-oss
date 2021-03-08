# Ressource Files analysieren

In your app folder there is a .tekton subdirectory. That's where all Pipeline related Ressource Definitions exist. Note how they specify an "apiVersion". This points to a Kubernetes CRD, tekton implements. If the pipeline would run in our cluster we could actually get all those ressources with, for instance:

```text
kubectl get pipelinerun
```

