# Fault injection durch Service Delay



### 2. Delay

```text
oc apply -f https://github.com/maxisses/openshiftservicemesh/blob/master/02-fault-injection/fault-injection_delay.yaml
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
        delay:
          fixedDelay: 3s
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

