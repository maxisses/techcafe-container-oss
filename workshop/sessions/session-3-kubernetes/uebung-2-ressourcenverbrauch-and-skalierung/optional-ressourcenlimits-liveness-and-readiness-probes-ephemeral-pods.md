# Ressourcenlimits Liveness & Readiness Probes // ephemeral Pods

fügt eurem deployment.yaml folgendes unten hinzu \(auf einrückung achten\) und deployed neu wie oben \(kubectl apply -f deployment.yaml\):

```text
resources:
            limits:
              memory: "256Mi"
              cpu: "1000m"
            requests:
              memory: "128Mi"
              cpu: "250m"
```

![](../../../.gitbook/assets/image%20%2862%29%20%281%29.png)

* ist die Summe aus Requests und Anzahl der Replikas größer als die verfügbaren Ressourcen verbleiben die Pods im Status "Pending" 

```text
kubectl get nodes
```

IP kopieren

```text
kubectl describe node <IP einfügen>
```

* unten bei "Allocated Ressources" seht ihr die Auslastung eures Knotens

fügt eurem deployment.yaml folgendes unten hinzu \(auf einrückung achten\) und deployed neu wie oben \(kubectl apply -f deployment.yaml\):

```text
livenessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 60
          periodSeconds: 60
```

* sobald der healthcheck nicht erfolgreich ist wird er Pod neu gestartet
* schaut euch mit kubectl get pods eure X \(zB 5\) pods an \(mit kubectl get pods -o wide seht ihr auch noch etwas mehr\) 
* killt einen mit kubectl delete pod &lt;NAME eines pods&gt; 
* mit kubectl get pods direkt danach seht ihr das ein neuer pod als ersatz gestartet wurde, weil pods durch das replicaset gemonitored werden und sobald einer crashed/stirbt/gekillt wird, wird ein neuer gestartet
* VSCode bietet auch die möglichkeit zwei terminals nebeneinander zu haben mit dem button neben dem +, dann kann man es sich parallel anschauen

```text
watch kubectl get pods -n <eure-initialien>-projekt
```

```text
kubectl delete --all pods -n <eure-initialien>-projekt
```

{% hint style="info" %}
Der letzte Befehl zeigt euch die "ephemeral nature" von pods. Pods werden durch ReplicaSet Controller und diese durch Deployments gesteuert. Das löschen von Pods, sorgt also nur dafür das der Controller den "desired state" asap wieder herstellt.
{% endhint %}

