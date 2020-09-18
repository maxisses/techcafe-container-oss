# Fehler einbauen

Ein Circuit Breaker wird dann aktiviert wenn der angesprochene Pod nicht antwortet bzw. fehlerhaft antwortet. 

Die aktuelle Anwendung läuft ziemlich fehlerfrei. Deshalb lasst uns einen fehlerhaften Details Service einbauen. Ich habe dazu den ruby Code ein bisschen verschwandelt und ein neues Image gebaut. Das Image liegt hier: docker.io/maxisses/bookinfo-details-v2

Mit folgendem Befehl wird nur ein Update auf das aktuelle details-Deployment gemacht und das Image durch das fehlerhafte getauscht.

```text
oc apply -f bookinfo_part3.yaml
```

Wenn wir nun fleißíg refreshen dann sehen wir das in ca. 20% der Fälle folgendes erscheint. "Error fetching products details".

![](../../../.gitbook/assets/image%20%2898%29.png)

Das können wir auch so prüfen:

```text
while true; do curl -s http://istio-ingressgateway-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max | grep -E "Book Details"\|"Error fetching product details!"; sleep 0.2; done
```

![](../../../.gitbook/assets/image%20%28108%29.png)



