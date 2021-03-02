# Horizontal Pod Autoscaling

Passt euer deployment.yaml wieder auf 1 Replica an. Dann, diesmal ausnahmsweise imperativ, deployed ihr direkt in Kubernetes einen horizontal autoscaler \(vertical wäre nodes hinzufügen\). In diesem Falle ist die Cpu percentage bezogen auf den resource request bewusst gering gewählt da wir ja eine Miniwebanwendung haben. min/max bezieht sich auf die Pods.

```text
kubectl autoscale deployment <name eures deployments> --cpu-percent=5 --min=1 --max=3 -n <eure-initialien>-projekt
```

Um den in Aktion zu sehen muss man ihn ein bisschen pushen und das schafft ihr wahrscheinlich nicht mit einem einfach curl...

```text
while true; do curl http://<ip eures nodes>:<nodeport>/; done
```

... sondern es braucht einen http load generator wie zB hey \([https://github.com/rakyll/hey](https://github.com/rakyll/hey)\). Nodeport und IP zu finden ist hier beschrieben:

{% page-ref page="../uebung-1-next-stop-kubernetes/service-fuer-die-app-erstellen.md" %}

Danach könnt ihr dann starten:

```text
hey -c 1000 -z 10s "http://<ip eures nodes>:<nodeport>/"
```

und sehen, dass immer mehr pods gestartet werden:

```text
watch -n 0.1 kubectl get pods
```

