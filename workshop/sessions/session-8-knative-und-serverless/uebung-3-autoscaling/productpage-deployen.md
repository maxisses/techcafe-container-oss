# Productpage deployen

Die productpage zu deployen funktioniert praktisch genauso wie die reviews Page. Es gibt aber einen Unterschied. Die productpage soll natürlich auch extern Adressierbar sein. Wer die bisherigen YAMLs aufmerksam gelesen hat, hat ggf. diese Zeile gesehen:

```text
serving.knative.dev/visibility: cluster-local
```

Sobald wir darauf verzichten, generiert KNative per default anhand des KNative Ingress eine externe Domain.

Außerdem sind hier folgende Dinge neu:

1. Ich habe in Zeile 19 explizit den KNative Pod Autoscaler eingestellt - das ist die default Einstellung. Man könnte aber hier auch auf den Standard Kubernetes Scaler wechseln, wenn man nach CPU Last skalieren will
2. 
{% hint style="danger" %}
Die Umgebungsvariable SERVICE\_DOMAIN muss für euren Namespace angepasst werden in Zeile 37:

```text
value: <euer namespace bzw. Projektname>.svc.cluster.local
```
{% endhint %}

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
        autoscaling.knative.dev/target: "2"
        # Alternative zum default "concurrency" ist requests per second
        autoscaling.knative.dev/metric: "rps"
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
            value: <euer namespace bzw. Projektname>.cluster.local
      serviceAccountName: bookinfo-productpage

```

