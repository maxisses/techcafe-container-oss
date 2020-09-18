# Kiali Integration

Kiali kommt mit Istio und ist ein hervorragendes Werkzeug für die Analyse von Microservices, Traffic und Release Management.

Es läuft bereits mit Pod, Service und Route in unserem Cluster und lässt sich leicht im Istio-system namespace finden und mittels des Pfeils direkt öffnen \(das blaue Symbol mit schwarzem Kreis\).

{% hint style="info" %}
Daneben laufen in diesem Namespace eine Reihe weiterer Istio Komponenten zB der Sidecar Injector und der Gateway, den wir schon benutzen.
{% endhint %}

[https://kiali-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/](https://kiali-istio-system.openshift-for-techcafe-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/)

![](../../../.gitbook/assets/image%20%2898%29.png)

Dort können wir uns unsere Anwendung anschauen. 

{% hint style="info" %}
Damit Kiali sinnvollen Output liefert ist Traffic notwendig!
{% endhint %}

![](../../../.gitbook/assets/image%20%2893%29.png)

