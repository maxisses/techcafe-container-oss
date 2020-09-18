# Testen des Dark Release

Obwohl immernoch beide Services da sind, können Nutzer aktuell nur die schwarzen Sternchen aufrufen.

```text
while true; do curl -s 
http://istio-ingressgateway-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max
 | grep "font color" | head -n 1; sleep 0.5; done
```

![](../../../.gitbook/assets/image%20%2894%29.png)

Wenn wir allerdings mit curl den http-Header mit "-H" spezifizieren können wir unser darkrelease ansteuern.

```text
while true; do curl -H "user-agent: darkrelease" -s 
http://istio-ingressgateway-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max
 | grep "font color" | head -n 1; sleep 0.5; done
```

![](../../../.gitbook/assets/image%20%2895%29.png)



