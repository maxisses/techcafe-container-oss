# Canary Reloaded

Canary kennen wir schon aus Session 6. OpenShift hat KNative in seine GUI integriert und macht es uns damit noch einfacher.

{% hint style="info" %}
Der Reviews Service ist recht behäbig. Das liegt an seinem doch sehr mächtigen Application Server. Deshalb entwicklt sich gerade Quarkus extrem stark, als Kubernetes-natives Java Framework: [https://www.redhat.com/de/topics/cloud-native-apps/what-is-quarkus](https://www.redhat.com/de/topics/cloud-native-apps/what-is-quarkus)
{% endhint %}

In der Topologie-Sicht kann ich über Set Traffic Distribution das Canary steuern:

![](../../../.gitbook/assets/image%20%28144%29.png)

```text
while true; do curl -s http://productpage-<namespace bzw. project>.ocpclusterpub-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/productpage | grep "font color" | head -n 1; sleep 0.5; done
```

