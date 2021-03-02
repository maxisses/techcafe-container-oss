# optional: Applikationsmonitoring & Auto-Skalierung

## Monitor Application Health

1. Um den Health Status euerer Applikation zu überprüfen, wählt euer Cluster in der IBM Cloud Oberfläche aus.
2. Klicke auf **Kubernetes Dashboard** um das Dashboard aufzurufen.
3. Wählt auf der linken Seite **Nodes** aus und klickt einen der Nodes an. Über **Allocation Resources** könnt ihr den Health Status der Nodes sehen.
4. Um die Logs euerer Applikationen zu sehen wählt **Pods**, &lt;**pod-name**&gt; \(dort klickt ihr auf die drei Punkte rechts\) und **Logs**. Oben in der
5. Um eine **ssh** Verbindung mit einem Container herzustellen, könnt ihr folgenden Befehl nutzen

   ```bash
   kubectl exec -it <pod-name> -- bash
   ```

![](../../../.gitbook/assets/image%20%2885%29.png)

## Scale Kubernetes Pods

Mit zunehmender Last kann es nötig werden die Anzahl der Pod zu erhöhen. Es möglich die Anzahl der Pods von Hand zu erhöhen. Die Anzahl der Pods wird als Replicas bezeichnet und diese werden durch ein  [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) gesteuert. Um die Anzahl der Pods zu erhöhen kann man folgenden Befehl nutzen:

```bash
kubectl scale deployment <deployment-name> --replicas=2 -n ${K8SNAMESPACE}
```

Nach kurzer Zeit, sind werden zwei Pods im Kubernetes Dashboard erscheinen \(oder mit `kubectl get pods`\). Das Load Balancing zwischen den beiden Pods über den Ingress Controller geregelt.

In Kubernetes gibt es die Möglichkeit den [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) zu aktivieren um automatisiert die Anzahl der Pods zu erhöhen oder zu verringern. Mittels verschiedener Regeln kann dies z.B. basierend auf der CPU Auslastung erfolgen.

Um einen Autoscaler zu erzuegen und eine dazugehörige Regel anzulegen kann folgender Befehl genutzt werden

```bash
kubectl autoscale deployment <deployment-name> --cpu-percent=<percentage> --min=<min_value> --max=<max_value>
```

Wenn der Befehl erfolgreich war, sieht man folgendes Ergebnis`horizontalpodautoscaler.autoscaling/<deployment-name> autoscaled`

### **Testen**

```text
while true; do curl https://<name eurer app>.bamftechcafek8scluster-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/; done
```

## Löschen der Resourcen

* Um alle erzeugten Resourcen zu löschen nutzt folgenden Befehl:

  ```bash
   helm uninstall ${MYPROJECT}
  ```

