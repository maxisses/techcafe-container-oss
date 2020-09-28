# Untitled

```text
tkn pipeline start build-and-deploy \
    --workspace name=shared-workspace,claimName=tekton-workspace-pvc,subPath=dir \
    -p deployment-name=vote-api \
    -p git-url=http://github.com/openshift-pipelines/vote-api.git \
    -p IMAGE=image-registry.openshift-image-registry.svc:5000/pipelines-tutorial/vote-api
```

