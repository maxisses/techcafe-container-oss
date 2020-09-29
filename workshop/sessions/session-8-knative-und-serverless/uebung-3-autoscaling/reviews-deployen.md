# Reviews deployen

Jetzt widmen wir uns den beiden Services, die einer Anpassung bedurften und zumindest was das .yaml angeht immer noch bedürfen.

Ihr könnt das yaml deployen wie ihr mögt. Als File abspeichern und mit "oc apply -f &lt;filename&gt;" oder ihr nutzt die GUI von OpenShift für das deployment. Nicht vergessen erst den ServiceAccount und dann den KNative Service.

2 Dinge sind hier wieder neu. 

1. Umgebungsvariablen in der Anwendung bzw. dem Container definieren in Zeile 33
2. In Zeile 24 und 26 steht die maxScale Annotation und das Target. Mit dem ersten definiert man die maximale Anzahl an Pods und mit dem Target definiert man wann skaliert wird.

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
        # handle 10 requests auf einmal pro pod
        autoscaling.knative.dev/target: "10"
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
          value: <euer namespace bzw. Projektname>.svc.cluster.local
        - name: LOG_DIR
          value: "/tmp/logs"
        - name: STAR_COLOR
          value: black
        - name: ENABLE_RATINGS
          value: "true"
```

