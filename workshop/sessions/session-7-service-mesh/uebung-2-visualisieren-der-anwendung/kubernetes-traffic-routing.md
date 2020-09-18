# Kubernetes Traffic Routing \(Canary\)

Der Standard Mechanismus eines Service in Kubernetes ist seine Requests gleichmäßig gemäß Round Robin an seine Pods zu verteilen. Im folgenden Beispiel wird das durch ein simples curlen und auslesen der Farbe der Sterne deutlich. 

```text
while true;
do curl -s http://istio-ingressgateway-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/max |
grep "font color" | head -n 1; sleep 0.5; done
```

![](../../../.gitbook/assets/image%20%2896%29.png)

Man sieht deutlich, dass hier 50:50 aufgeteilt wird. Das mit Kubernetes-Basis Mittel anzupassen ist nur möglich indem man die Zahl der Pods ändert. Geht dazu in die OpenShift Console und fahrt zB den reviews-v3 Service auf 10 Pods hoch. Das neue Ergebnis des curl spiegelt das sofort entsprechend wider. Skaliert danach wieder runter auf 1.

Der curl darf ruhig weiterlaufen, damit wir gleich ein bisschen Traffic analysieren können. Er sollte sich zurück auf das alte 50:50 entwickeln.

![](../../../.gitbook/assets/image%20%28113%29.png)

![](../../../.gitbook/assets/image%20%28111%29.png)

{% hint style="info" %}
Defakto war das gerade eine Form von Canary Release, denn die "black"-Version von reviews hat nur gut 9% des Traffics bekommen \(11 Pods in Summe, 10 rot, 1 schwarz\).  
Canary ist hier super erklärt: [https://martinfowler.com/bliki/CanaryRelease.html](https://martinfowler.com/bliki/CanaryRelease.html)
{% endhint %}

