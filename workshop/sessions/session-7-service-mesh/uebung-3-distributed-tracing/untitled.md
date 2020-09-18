# Jaeger Trace Analyse

Jaeger lässt sich direkt aus Kiali heraus starten \(links unten\) oder alternativ aus dem istio-system Projekt in der Topology.

Jaeger bietet alle Möglichkeiten um einzelne Requests auszuwerten.

{% hint style="info" %}
Header Propagation

Das alles funktioniert nur wenn es in jedem einzelnen Service implementiert ist, denn die http-Header werden leider nicht automatisch weitergeleitet.

[https://istio.io/latest/faq/distributed-tracing/](https://istio.io/latest/faq/distributed-tracing/)
{% endhint %}

![](../../../.gitbook/assets/image%20%28107%29.png)

![](../../../.gitbook/assets/image%20%28111%29.png)

