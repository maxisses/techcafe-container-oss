# Kiali Dynamic Traffic Routing

Mit Istio geht das natürlich charmanter. Lasst den Curl weiter laufen und wechselt zurück ins Kiali Dashboard. Geht dort in die Details des reviews Service.

![](../../../.gitbook/assets/image%20%28101%29.png)

Wählt dort rechts oben "Actions" aus und "Trafffic Shifting".

![](../../../.gitbook/assets/image%20%28153%29.png)

Hier können wir die gleiche Funktionalität problemlos konfigurieren, ohne dafür extra Pods oder unnötigen Workload zu generieren. Ihr werdet bei einem Blick auf den curl output feststellen, dass das auch schneller und zuverlässiger funktioniert.

![](../../../.gitbook/assets/image%20%28170%29.png)

Wenn man in Kiali runterscrolled und auf den "Istio Config" Tab geht, sieht man, dass wieder sowohl ein VirtualService und eine DestinationRule erstellt wurden. In den YAML Files erkennt man die Einstellungen wieder und kann sie entsprechend anpassen. Die DestinationRule selektiert in diesem Fall, welche Pods herangezogen werden mittels des labels "version". Man kann also so granular selektieren wie man will und nicht auf Deployment Ebene wie in diesem Fall geschehen.

{% hint style="info" %}
Kiali Actions ist ein super Startpunkt um schnell Templates für Gateways\(siehe "Advanced Options" oben\), VirtualServices und DestinationRules zu erstellen. Danach sollte man die YAMLs aber exportieren und in Version Control packen.
{% endhint %}

Zu guter Letzt löschen wir das Routing erstmal.

![](../../../.gitbook/assets/image%20%28105%29.png)

