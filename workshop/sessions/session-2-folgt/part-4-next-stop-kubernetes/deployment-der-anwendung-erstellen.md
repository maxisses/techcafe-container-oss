# Deployment der Anwendung erstellen

* öffnet VSCode
* öffnet zB in VSCode einen Terminal \(rechte Maustaste links auf den Ordner eurer -&gt; Open Terminal\) 
* rechte Maustaste links auf den Ordner eurer App --&gt; New File; nennt es "deployment.yaml"
* fügt folgenden content ein
* ersetzt die Zeichenkette "maxpubliceduapp" durch einen Namen eurer Wahl
* ersetzt, wenn ihr es habt, nach dem image tag "maxisses/maxapp:latest" in dieser form dockernutzername/nameeuresimage:latest

```text
apiVersion: apps/v1
kind: Deployment
metadata:
  name: maxpubliceduapp-deployment
spec:
  # anpassen auf mehrere instanzen wenn gewünscht
  replicas: 1
  selector: 
    matchLabels:
      app: maxpubliceduapp-selector
  template:
    metadata:
      labels:
        app: maxpubliceduapp-selector
    spec:
      containers:
      - name: maxpubliceduapp
        image: maxisses/maxpubliceduapp:latest
        ports:
            - containerPort: 3000
```

führt im Terminal den Befehl aus:

```text
kubectl apply -f deployment.yaml
```

--&gt; Output ungefähr so: deployment.apps/maxpubliceduapp-deployment created

* geht in den browser und wenn ihr das kubernetes dashboard offen habt seht ihr unter deployments jetzt eure app \(alternativ Terminal: kubectl get deployments\)
* wenn ihr links auf Pods geht, seht ihr außerdem einen pod mit dem namen eurer app und einer zeichenkette hinten dran \(alternativ Terminal: kubectl get pods\)

