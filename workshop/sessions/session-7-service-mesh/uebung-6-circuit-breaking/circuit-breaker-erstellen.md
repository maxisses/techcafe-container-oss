# Circuit Breaker erstellen

Jetzt macht es Sinn einen Circuit Breaker einzubauen. Istio benutzt hier den Begriff OutlierDetection

```text
oc apply -f circuit-breaking.yaml
```

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

