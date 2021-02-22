# manuell Skalieren

* Ändert die anzahl "replicas" in der datei "deployment.yaml" auf eine euch genehme Zahl, zB 5; speichert und
* führt den Befehl erneut aus:

```text
kubectl apply -f deployment.yaml -n <eure-initialien>-projekt
```

* prüft mit 

```text
kubectl get pods -n <eure-initialien>-projekt
```

oder in der GUI ob es funktioniert hat

