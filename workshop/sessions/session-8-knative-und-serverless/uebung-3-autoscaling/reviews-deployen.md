# Reviews deployen

Jetzt widmen wir uns den beiden Services, die einer Anpassung bedurften und zumindest was das .yaml angeht immer noch bedürfen.

Ihr könnt das yaml deployen wie ihr mögt. Als File abspeichern und mit "oc apply -f &lt;filename&gt;" oder ihr nutzt die GUI von OpenShift für das deployment.

2 Dinge sind hie

{% hint style="danger" %}
Bitte nicht
{% endhint %}



```text
apiVersion: v1
kind: ServiceAccount
metadata:
  name: bookinfo-reviews
  labels:
    account: reviews
---
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: reviews
  labels:
    app: reviews
    version: v2
    app.kubernetes.io/part-of: bookinfo
    serving.knative.dev/visibility: cluster-local
spec:
  template:
    metadata:
      annotations:
        # minimum --> knative heißt nicht zwangsläufig 0
        autoscaling.knative.dev/minScale: "1"
        # maximum an erlaubten pods
        autoscaling.knative.dev/maxScale: "15"
    spec:
      serviceAccountName: bookinfo-reviews
      containers:
      - name: reviews
        image: docker.io/maxisses/reviews-kn
        imagePullPolicy: Always
        ports:
        - containerPort: 9080
        env:
        - name: SERVICES_DOMAIN
          value: knative-tut.svc.cluster.local
        - name: LOG_DIR
          value: "/tmp/logs"
        - name: STAR_COLOR
          value: black
        - name: ENABLE_RATINGS
          value: "true"
```

