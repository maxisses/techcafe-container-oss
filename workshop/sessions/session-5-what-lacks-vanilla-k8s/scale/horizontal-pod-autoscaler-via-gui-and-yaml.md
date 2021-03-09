# Horizontal Pod Autoscaler via GUI & YAML

Um den Pod zu skalieren müssen die Resourcen Limits gesetzt sein. Dafür öffnen wir das Deployment und klicken auf YAML. Dort suchen wir nach "resources:"

![](../../../.gitbook/assets/screenshot-2021-03-08-at-21.56.45.png)

Anstelle von "{}" tragen wir folgende Limits ein und klicken auf "Save":

```text
            limits: 
              cpu: 50m
              memory: 128Mi
            requests:
              cpu: 50m
              memory: 128Mi
```

Um ein automatisches Skalieren zu erwirken, müssen wir einen HorizontalPodAutoscaler erstellen. Hierzu klicken wir auf "Add Horizontal Pod Autoscaler"

![](../../../.gitbook/assets/screenshot-2021-03-08-at-21.51.24.png)

Es öffnet sich der OpenShift Editor. Dort tragen wir die CPU Utilization von 1% ein und klicken auf "Save".

![](../../../.gitbook/assets/screenshot-2021-03-08-at-22.06.26.png)

Alternativ kann auch per OC automatisch skaliert werden:

```text
oc autoscale deployment productpage --min=1 --max=3 --cpu-percent=5   

horizontalpodautoscaler.autoscaling/productpage autoscaled
```

Der Status des Autoscalers kann abgefragt werden, um zu checken, ob dieser ordnungsgemäß funktioniert:

```text
oc get horizontalpodautoscaler

NAME      REFERENCE                   TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
example   Deployment/productpage-v1   32%/50%   1         3         1          2m29s
```

