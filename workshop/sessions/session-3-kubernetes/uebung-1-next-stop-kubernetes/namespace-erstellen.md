# Namespace erstellen

Legt eine Datei z.B. im Ordner der Applikation an und nennt sie namespace.yaml

```text
apiVersion: v1
kind: Namespace
metadata:
  name: <eure-initialien>-projekt ## nur klein Buchstaben
```

Erstellt den Namespace mit

```text
kubectl apply -f namespace.yaml
```

