# Scaling testen

Unsere productpage lässt schon ein bisschen aus der Ruhe bringe mit einfachem curl:

```text
while true; do curl -s http://productpage-<euer-namespace-name>.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/; sleep 0.05; done
```

Bei mir hat es für 7 Pods gereicht - und da ich den screenshot etwas zu spät gemacht habe sehen wir auch gleich wie das System wieder runterskaliert, dafür gibt es default gracePeriod von 40 Sekunden.

![](../../../.gitbook/assets/image%20%28134%29.png)

Nun haben wir gerade ja noch keinen der Backendservices aufgerufen, denn diese verbergen sich hinter /productpage. Erster Versuch mit curl:

```text
while true; do curl -s http://productpage-<name-eures-namespace>.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/ | grep -E "Book Details"\|"Error fetching product details!"; sleep 0.; done
```

Bei mir hat auch das rausnehmen des sleeps nichts gebracht. Mit größeren Geschützen sieht man den Effekt aber hervorragend:

```text
hey -c 120 -z 10s http://productpage-max-bookinfo-kn.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/productpage
```

![](../../../.gitbook/assets/image%20%28142%29.png)

