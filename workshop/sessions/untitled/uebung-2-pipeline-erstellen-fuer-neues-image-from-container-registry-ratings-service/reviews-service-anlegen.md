# Reviews Service anlegen

Den Reviews Service deployen wir erstmal traditionell. Hier wird bereits ein Image-Stream angelegt, sodass ein Update auf exakt dieses Image auch ein neues Deployment nach sich zieht. Hier ist aber noch keine Tekton Pipeline im Spiel.

{% hint style="info" %}
Hintergrund: Reviews ist inklusive Dockerfile mit einem sogenannten "MultiStage" Build Dockerfile im heutigen Repo \(kommt später - [https://github.com/Javatar81/pipeline-examples/tree/main/reviews](https://github.com/Javatar81/pipeline-examples/tree/main/reviews)\). Das ist etwas komplexer beim anlegen der Pipeline, deshalb haben wir es heute ausgeklammert.
{% endhint %}

Image Name: **docker.io/istio/examples-bookinfo-reviews-v1:1.16.2**  
Application Name: **bookinfo**  
Name: **reviews**

![](../../../.gitbook/assets/image%20%28149%29.png)

