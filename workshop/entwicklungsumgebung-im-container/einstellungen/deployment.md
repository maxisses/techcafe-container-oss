# Deployment

Um das Image im Cluster zu deployen kann folgendes YAML genutzt werden

```text
---
apiVersion: v1
kind: Namespace
metadata:
  name: <your-namespace>
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: terminal-deployment
  namespace: <your-namespace>
spec:
  replicas: 1
  selector:
    matchLabels:
      app: terminal-selector
  template:
    metadata:
      labels:
        app: terminal-selector
    spec:
      containers:
        - name: terminal
          image: wumaxd/terminal:latest
          resources:
            requests:
              memory: "128Mi"
              cpu: "250m"
            limits:
              memory: "256Mi"
              cpu: "500m"
          ports:
            - containerPort: 22
          securityContext:
            privileged: true
          env:
            - name: SSH_USER
              value: <your-user>
            - name: SSH_PASSWORD
              value: <your-password>
---
apiVersion: v1
kind: Service
metadata:
  name: terminal-service
  namespace: <your-namespace>
spec:
  type: LoadBalancer
  ports:
    - name: ssh
      port: 22
  selector:
    app: terminal-selector

```

Mittels des Service kann die URL für die SSH Verbindung abgerufen werden

```text
kubectl get services -n terminal-app
NAME               TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)        AGE
terminal-service   LoadBalancer   172.21.181.128   169.50.39.220   22:30088/TCP   7h26m
```

