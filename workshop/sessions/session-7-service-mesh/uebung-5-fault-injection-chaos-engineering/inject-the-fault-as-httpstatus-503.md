# Fault Injection mit httpStatus Codes

Das YAML aus Kiali liegt hier für euch erweitert schon vor. Es gibt im wesentlichen zwei Möglichkeiten für Fault Injection: abort und delay. Beide könnt ihr nacheinander anwenden. Wenn ihr genau reinschaut erkennt ihr was ich mit "User Ärgern" meinte. Wenn man sich einloggt, hier zB als "max", dann werden die faults erst aktiviert.   
Das könnt ihr sowohl im Browser, als auch mit curl testen.

Als erstes ohne einen User zu spezifizieren.

```text
while true; do curl -s http://istio-ingressgateway-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max | grep "font color" | head -n 1; sleep 0.5; done    
```

Und danach mit entsprechendem User:

### 1. Abort

```text
oc apply -f https://raw.githubusercontent.com/maxisses/openshiftservicemesh/master/02-fault-injection/fault-injection_abort.yaml
```

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

