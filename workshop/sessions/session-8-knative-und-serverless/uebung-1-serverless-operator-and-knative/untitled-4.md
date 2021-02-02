# KNative Komponenten

Wechselt nun in die OpenShift Console/GUI. Hier seht ihr nun euer neues Projekt, aber bevor es losgeht schauen wir uns nochmal das Projekt "knative-serving" und das Projekt "knative-serving-ingress".

In dem erstgenannten seht ihr die Komponenten, welche auch schon auf die Funktionalität von KNative hinweisen. Z.b der activator - welcher gewährleistet, dass man Applikationen komplett abschaltet - scale to zero. Außerdem der Autoscaler, welcher das skalieren entlang von **concurrency** und **requests-per-seconds** \(rps\) unterstützt. Ihr seht den autoscaler zweimal - das liegt daran, dass man sowohl den Kubernetes-nativen HPA nutzen kann, welchen wir schon kennengelernt haben, als auch einen von KNative optimierten \(KPA\). Beide unterstützen unterschiedliche Metriken - der HPA unterstützt CPU Usage. Weitere Details zu controller \("desired state"\) und webhook für allen eingehenden Traffic in der Doku: [https://knative.dev/v0.15-docs/serving/knative-kubernetes-services/](https://knative.dev/v0.15-docs/serving/knative-kubernetes-services/)

![](../../../.gitbook/assets/image%20%28139%29.png)

Darüber hinaus gibt es wieder einen speziellen Ingress, welcher den eingehenden Traffic empfangen muss und das Networking der KNative Services steuert. Diesen findet ihr im "knative-serving-ingress" Projekt und seht dort den 3scale Kourier indem alle "Routen", also public URLs unserer KNative Anwendungen zu sehen sind. Kourier ist tatsächlich ein leichtgewichtiger Ersatz für den Istio Ingress den wir in der letzten Session gesehen haben.

![](../../../.gitbook/assets/image%20%28133%29.png)

