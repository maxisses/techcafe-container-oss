# Reviews deployen

Jetzt widmen wir uns den beiden Services, die einer Anpassung bedurften und zumindest was das .yaml angeht immer noch bedürfen.

Ihr könnt das yaml deployen wie ihr mögt. Ich schlage die drei Möglichkeiten vor.

1. repo clonen und files dort anpassen und mit `oc apply -f <filename>` deployen 

   Am einfachsten \(und für euch potentiell nachhaltigsten :\) \) ist es wenn ihr euch das github-repo cloned:

   1. ```text
      git clone https://github.com/maxisses/knative-on-openshift.git
      ```

2. Ihr kopiert euch die hier angegebenen YAMLs und speichert sie als \*.yaml auf eurem rechner und deployed mit `oc apply -f <filename>` 
3. Ihr nutzt die GUI von OpenShift für das deployment \("Create resources from their YAML"\). Nicht vergessen erst den ServiceAccount und dann den KNative Service, da die GUI nur eine Ressource auf einmal zulässt.

![](../../../.gitbook/assets/image%20%28137%29.png)

**2 Dinge sind in dem folgenden YAML für das Deployment von reviews wieder neu.** 

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
          value: black
        - name: ENABLE_RATINGS
          value: "true"
```

