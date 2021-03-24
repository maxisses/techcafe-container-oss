# Fault Injection mit httpStatus Codes auf Basis bestimmter User

## Abort

Das YAML aus Kiali liegt hier für euch erweitert schon vor. 

```text
oc apply -f https://raw.githubusercontent.com/maxisses/openshiftservicemesh/master/02-fault-injection/fault-injection_abort.yaml
```

Es gibt im wesentlichen zwei Möglichkeiten für Fault Injection: abort und delay. Beide könnt ihr nacheinander anwenden. Wenn ihr genau reinschaut erkennt ihr was ich mit "User Ärgern" meinte. Wenn man sich einloggt, hier zB als "max" \(ohne Passwort\), dann werden die faults erst aktiviert.  
Das könnt ihr dann im Browser testen.

```text
kind: VirtualService
apiVersion: networking.istio.io/v1alpha3
metadata:
  name: reviews
spec:
  hosts:
    - reviews
  http:
    - fault:
        abort:
          httpStatus: 500
          percentage:
            value: 50
      match:
      - headers:
          end-user:
            exact: max
      route:
        - destination:
            host: reviews
            subset: risky
    - route:
        - destination:
            host: reviews
            subset: safe
---
kind: DestinationRule
apiVersion: networking.istio.io/v1alpha3
metadata:
  name: reviews
spec:
  host: reviews
  subsets:
    - labels:
        version: v2
      name: safe
    - labels:
        version: v3
      name: risky
```

