# Erstellen des Circuit Breakers

```text
kind: VirtualService
apiVersion: networking.istio.io/v1alpha3
metadata:
  name: details
spec:
  hosts:
    - details
  http:
    - route:
        - destination:
            host: details
---
kind: DestinationRule
apiVersion: networking.istio.io/v1alpha3
metadata:
  name: details
spec:
  host: details
  trafficPolicy:
    outlierDetection:
      consecutiveErrors: 2
      interval: 2s
      baseEjectionTime: 5s
      maxEjectionPercent: 100

```

