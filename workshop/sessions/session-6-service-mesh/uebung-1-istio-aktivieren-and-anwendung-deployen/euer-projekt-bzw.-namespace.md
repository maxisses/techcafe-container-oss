# Euer Projekt bzw. Namespace

Normalerweise müsstet ihr im ersten Schritt müsstet ihr ein neues Projekt bzw. Namespace erstellen. Der Einfachheit halber haben wir das schon gemacht und zwar mit euren Initialien gefolgt von -bookinfo.

{% hint style="warning" %}
Ansonsten wäre das der Befehl folgender. Der Hintergrund dafür, dass wir es schon erstellt haben ist, dass jeder neue Namespace für Istio Service Mesh aktiviert werden muss. Das dauert manchmal einen kleinen Moment, deshalb haben wir dem vorgegriffen.

```text
oc new-project <initialien>-bookinfo-servicemesh
```
{% endhint %}

Um in eurer Konsole in das Projekt zu wechseln tut ihr folgendes:

```text
oc project <initialien>-bookinfo-servicemesh
```

Jetzt deployed ihr eure Anwendung wie in der letzten Session mit 4 Services.

```text
oc apply -f https://raw.githubusercontent.com/maxisses/openshiftservicemesh/master/00-deploy/bookinfo_part1.yaml
```

Jetzt haben wir fast den Zustand aus Session 6 hergestellt und es laufen wieder 4 Services der bookinfo Anwendung.

Jetzt sollten prüfen ob in jedem Pod 2/2 Containern laufen. Nämlich der Envoy Proxy und der eigentliche Container.

```text
oc get pods
```

![](../../../.gitbook/assets/image%20%2891%29.png)

![](../../../.gitbook/assets/image%20%2889%29.png)

Der Namespace ist für [Sidecar Injection](https://istio.io/latest/docs/ops/configuration/mesh/injection-concepts/) aktiviert worden und in jedem Deployment ist diese nochmals als "enabled" annotiert. Dadurch läuft jetzt aller traffic des containers über den envoy Container.

{% hint style="info" %}
Problem: Da der erste Envoy Proxy Container in unserer Kette von Microservices neben dem productpage container läuft aber _nach_ dem Service, würde das bedeuten das man kein Traffic Management am Microservice productpage durchführen kann. Deshalb schaltet man einen Gateway davor, den Istio mitbringt. Mehr dazu später.
{% endhint %}

```text
oc apply -f https://raw.githubusercontent.com/maxisses/openshiftservicemesh/master/00-deploy/bookinfo-gateway.yaml
```

Dieser Gateway läuft als pod in der istio controlplane in seinem eigenen Namespace und hat eine eigene URL. Damit wir alle sicher stellen, dass wir auch wirklich Traffic auf unsere eigene App bringen müsst ihr einmal das YAML anpassen und zwar so:

1. Geht in der OpenShift Console links oben auf Administrator
2. öffnet darunter Home und geht auf Explore
3. Sucht in der Liste nach "VirtualService", geht dann auf Instances und wählt den einzigen Eintrag aus
4. ändert im yaml File dort wo bei mir /maxdargatz steht auf euren Namen bzw am besten eure Initialien

![](../../../.gitbook/assets/image%20%2883%29.png)

{% hint style="info" %}
Der VirtualService ist eine wesentliche Istio Ressource zum Traffic Management und in diesem Falle der Link zwischen dem Istio Gateway und des in eurem Projekt laufenden "productpage" Service. Wir gehen darauf noch mehr ein.
{% endhint %}

Eure Anwendung ist dann unter folgendem link und eurer entsprechenden Endung erreichbar. Die Endung Bitte auf Eure Initialien anpassen.

```text
http://istio-ingressgateway-istio-system.ocpclusterpub-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/maxdargatz
```

