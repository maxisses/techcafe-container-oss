# Circuit Breaker erstellen

Jetzt macht es Sinn einen Circuit Breaker einzubauen. Istio benutzt hier den Begriff OutlierDetection.

```text
oc apply -f https://raw.githubusercontent.com/maxisses/openshiftservicemesh/master/03-circuit_breaking/circuit-breaking.yaml
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
      interval: 1s
      baseEjectionTime: 2s
      maxEjectionPercent: 100
```

{% hint style="info" %}
Dieser CircuitBreaker triggered nach 2 Errors in Folge die innerhalb von 2 Sekunden aufgetreten sein müssen und nimmt den Service für 3 Sekunden raus mit 100% seiner pods.
{% endhint %}

