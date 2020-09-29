# invoke und test



```text
while true; do curl -s http://istio-ingressgateway-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max | grep -E "Book Details"\|"Error fetching product details!"; sleep 0.2; done
```

