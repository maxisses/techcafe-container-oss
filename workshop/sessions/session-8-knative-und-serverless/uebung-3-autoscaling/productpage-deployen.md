# Productpage deployen

```text
apiVersion: v1
kind: ServiceAccount
metadata:
  name: bookinfo-productpage
  labels:
    account: productpage
---
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: productpage
  labels:
    app.kubernetes.io/part-of: bookinfo
spec:
  template:
    metadata:
      annotations:
        # ich kann zwischen knative autoscaler und k8s autoscaler wählen
        autoscaling.knative.dev/class: "kpa.autoscaling.knative.dev"
        # minimum --> knative heißt nicht zwangsläufig 0
        autoscaling.knative.dev/minScale: "1"
        # maximum an erlaubten pods
        autoscaling.knative.dev/maxScale: "15"
        # handle 10 requests auf einmal pro pod
        autoscaling.knative.dev/target: "10"
    spec:
      containers:
      - image: maxisses/productpage-kn:latest
        livenessProbe:
          httpGet:
            path: /health
          initialDelaySeconds: 60
          periodSeconds: 60
        ports:
        - containerPort: 9080
        env:
          - name: SERVICES_DOMAIN
            value: knative-tut.svc.cluster.local
      serviceAccountName: bookinfo-productpage

```

