# Funktioniert er?

Nutzt jetzt erneut den curl Befehl um zu schauen ob er funktioniert. Sobald er triggered ist er für 2 Sekunden aktiv bevor er den Traffic wieder freigibt.

```text
while true; do curl -s http://istio-ingressgateway-istio-system.ocpclusterpub-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max | grep -E "Book Details"\|"Error fetching product details!"; sleep 0.2; done
```

Man wird deshalb immer nur einzelne Errors oder mehr als 2 in Folge sehen, denn nach Errors schaltet sich der CircuitBreaker ein.

![](../../../.gitbook/assets/image%20%28119%29.png)



