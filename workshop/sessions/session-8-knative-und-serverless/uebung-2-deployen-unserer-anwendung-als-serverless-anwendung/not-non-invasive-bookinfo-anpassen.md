# "not non-invasive" - Bookinfo anpassen

Bei der Implementierung von Anwendungen gilt es etwas aufzupassen. ServiceMesh hatte die Herausforderungen der Header-Propagation um Tracing zu ermöglichen. Das Problem ist hier etwas einfacher - im Kern ist es wichtig HTTP-Calls unserer Microservices bzw. die Adressen dieser vollständig als Umgebungsvariablen konfigurieren zu können.

Beispiel:

Wir erinnern uns, dass die reviews den ratings Service rufen müssen um die Anzahl Sternchen anzuzeigen. Das tut sie mit normalen Kubernetes Services mit Namen und Port, im Code sieht das so aus: [http://ratings:9080](http://ratings:9080)

![](../../../.gitbook/assets/image%20%28129%29.png)

Während Kubernetes Services Ports brauchen nutzt KNative FQDNs der generierten Routen. Wir sehen sie auch in OpenShift: [http://ratings.max-bookinfo-kn.svc.cluster.local](http://ratings.max-bookinfo-kn.svc.cluster.local).

Das Problem ist hier der Port - welcher hart gecoded ist und für KNative Services standard 80 \(http - deshalb oben nicht nötig ihn zu vermerken\) ist. Die beiden Services welche andere aufrufen \(productpage und reviews\) müssen also angepasst werden und brauchen als Umgebungsvariable den hostnamen \(wie bisher auch\) und zusätzlich die services\_domain - das ist der FQDN eures Projects bzw. Namespace - in meinem Falle [max-bookinfo-kn.svc.cluster.local](http://ratings.max-bookinfo-kn.svc.cluster.local/).  
Das heißt bei productpage und reviews müsst ihr im yaml-File euren Projektnamen eintragen - wo zeige ich gleich.

{% hint style="info" %}
Wer sich jetzt denkt - ein Projekt oder Namespace wird man doch als Umgebungsvariable automatisch auslesen können: Der hat Recht. In Kubernetes Deployments funktioniert das super. Leider ist es für KNative noch nicht da. Es gibt einen Pull Request:\)

[https://github.com/knative/serving/pull/8126](https://github.com/knative/serving/pull/8126)

[https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/](https://kubernetes.io/docs/tasks/inject-data-application/environment-variable-expose-pod-information/)

Und es gäbe noch eine zweite charmante Methode - da wir den Wert an 4 Stellen ändern müssen bietet sich ein Helm Chart ebenfalls an.
{% endhint %}

![](../../../.gitbook/assets/image%20%28127%29.png)

