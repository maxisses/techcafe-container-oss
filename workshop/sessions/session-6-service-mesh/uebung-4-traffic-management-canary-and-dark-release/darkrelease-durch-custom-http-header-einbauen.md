# DarkRelease durch custom http-Header einbauen

Wir tun für unser dark Release so als wären unsere roten Sternchen ein neues Feature in v3 der reviews Anwendung und wir möchten diese v3 versteckt testen.

Anbei der Befehl den nötigen VirtualService und die DestinationRule welche via Label Selector Pods segmentiert. Hier in die Subsets risky und safe. Wir nutzen um das DarkRelease durchzuführen http-Header Modifikation. Mehr auf der nächsten Seite.

```text
oc apply -f https://raw.githubusercontent.com/maxisses/openshiftservicemesh/master/01-dark-release/dark-release.yaml
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
    - match:
        - headers:
            user-agent:
              exact: darkrelease
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

