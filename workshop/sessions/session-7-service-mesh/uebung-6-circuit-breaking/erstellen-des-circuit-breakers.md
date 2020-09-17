# Erstellen des Circuit Breakers

```text
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: circuit-breaker-for-the-entire-default-namespace
spec:
  host: "<servicename>.<namespacename>.svc.cluster.local"          # This is the name of the k8s service that we're configuring
  trafficPolicy:
    outlierDetection: # Circuit Breakers HAVE TO BE SWITCHED ON
      maxEjectionPercent: 100
      consecutiveErrors: 2
      baseEjectionTime: 20s
      interval: 12s
```

