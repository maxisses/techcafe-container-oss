# Details Service deployen

Der Details Service wird nur gecalled und ruft nichts auf. Hier können wir ein ganz komplikationsloses KNative Service yaml verwenden.

```text
oc apply -f https://raw.githubusercontent.com/maxisses/knative-on-openshift/master/details-kn.yaml
```

Bei der Gelegenheit ein neues Konzept im yaml-File. Nämlich das minScale. Dieser Service wird nie auf 0 skalieren. KNative kann also auch völlig ohne scale-to-zero auskommen.

```text
apiVersion: v1
kind: ServiceAccount
metadata:
  name: bookinfo-details
  labels:
    account: details
---
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: details
  labels:
    app: details
    version: v1
    app.kubernetes.io/part-of: bookinfo
    serving.knative.dev/visibility: cluster-local
spec:
  template:
    metadata:
      annotations:
        # minimum --> knative heißt nicht zwangsläufig 0
        autoscaling.knative.dev/minScale: "1"
    spec:
      serviceAccountName: bookinfo-details
      containers:
      - name: details
        image: docker.io/istio/examples-bookinfo-details-v1:1.16.2
        imagePullPolicy: Always
        env:
        - name: LOG_DIR
          value: "/tmp/logs"
        ports:
        - containerPort: 9080
          name: http1
```

