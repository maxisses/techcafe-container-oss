# Neue Revisionen vom reviews Service anlegen

Der Reviews Service ruft den ratings Service mit einer ENABLE\_RATINGS und STAR\_COLOR Umgebungsvariable auf. Deshalb bietet es sich an, diesen zu nutzen, damit wir einen Effekt sehen.

Die naheliegendste Option sind zwei Updates. 

1. [x] STAR\_COLOR: red
2. [x] ENABLE\_RATINGS: false

Diese liegen auch fertig im github-Repo. Ihr müsst dort aber selbstverständlich wieder:

{% hint style="danger" %}
Die Umgebungsvariable SERVICE\_DOMAIN muss für euren Namespace angepasst werden:

```text
value: <euer namespace bzw. Projektname>.svc.cluster.local
```
{% endhint %}

Sobald ihr die rote Version deployed `oc apply -f reviews-kn-red.yaml` habt und auf den gestrichelten Kasten in der Topologie-Sicht klickt seht ihr jetzt 2 Revisionen und sobald ihr `oc apply -f reviews-kn-nostars.yaml` deployed taucht auch die dritte auf. 

![](../../../.gitbook/assets/image%20%28137%29.png)



```text
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
        autoscaling.knative.dev/target: "5"
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
          value: red
        - name: ENABLE_RATINGS
          value: "true"
```

```text
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
        autoscaling.knative.dev/target: "5"
    spec:
      serviceAccountName: bookinfo-reviews
      containers:
      - name: reviews
        image: docker.io/maxisses/reviews-kn
        imagePullPolicy: Always
        ports:
        - containerPort: 9080
        env:
        - name: LOG_DIR
          value: "/tmp/logs"
        - name: SERVICES_DOMAIN
          value: <euer namespace bzw. Projektname>.svc.cluster.local
        - name: STAR_COLOR
          value: black
        - name: ENABLE_RATINGS
          value: "false"
```

