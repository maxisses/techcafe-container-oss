# Troubleshooting

Ein kleinen Fehler habe ich drin gelassen ... weil er mir selbst unterlaufen ist. Wenn ihr jetzt auf die productpage geht, lädt sie - ABER die Services sind nicht erreichbar.

Der einfachste Weg zu debuggen sind die Logs. 

Und jetzt muss man aufmerksam schauen um den Fehler zu finden - In den FQDNs hat sich ein Fehler eingeschlichen und es fehlt das **.svc**.cluster.local. Das habe ich in dem yaml  in Zeile 31 unten angepasst den gesamten Service gelöscht und neu deployed.

![](../../../.gitbook/assets/image%20%28131%29.png)

Hier der zB der korrekte Wert mit einem Klick aus der Topologiesicht ausgelesen für "reviews".

![](../../../.gitbook/assets/image%20%28126%29.png)

```text
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
            value: <euer namespace bzw. Projektname>.svc.cluster.local
      serviceAccountName: bookinfo-productpage

```

