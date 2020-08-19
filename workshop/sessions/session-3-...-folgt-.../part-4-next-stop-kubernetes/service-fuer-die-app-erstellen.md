# Service für die App erstellen

* geht in VSCode 
* rechte Maustaste links auf den Ordner eurer App --&gt; New File; nennt es "service.yaml"
* fügt folgenden content ein
* ersetzt die Zeichenkette "maxpubliceduapp" durch einen Namen eurer Wahl und ändert bei
* ganz wichtig ist hier das der selector \(hier maxpubliceduapp-selector\) mit dem oben unter labes und matchLabels übereinstimmt, den über diesen Namen identifiziert der Service das deployment

```text
apiVersion: v1
kind: Service
metadata:
  name: maxpubliceduapp-service
spec:
  type: NodePort
  ports:
    - name: http
      port: 3000
      nodePort: 32555
  selector:
    app: maxpubliceduapp-selector
```



