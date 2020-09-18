# Fault Injection mit httpStatus Codes

Das YAML aus Kiali

```text
oc apply -f fault-injection.yaml
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
          httpStatus: 503
          percentage:
            value: 100
      route:
        - destination:
            host: reviews.max-bookinfo.svc.cluster.local
            subset: risky
    - route:
        - destination:
            host: reviews
            subset: safe
```

```text
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

