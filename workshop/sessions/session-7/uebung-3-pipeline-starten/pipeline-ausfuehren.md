# Pipeline ausführen

In der Pipeline Übersicht wählen wir unter "Actions" "Start" aus.

![](../../../.gitbook/assets/image%20%28175%29.png)

Wir fügen die folgenden Parameter ein

{% hint style="danger" %}
Macht einen Fork von [https://github.com/maxisses/golang-presentation.git](https://github.com/maxisses/golang-presentation.git) in euren Account und nehmt eure git URL.
{% endhint %}

* git-url: &lt; eure git url &gt;
* package: api
* context: ./exercises/helloWorldAPI

{% hint style="danger" %}
In das Image unten euren Namespace einsetzen
{% endhint %}

* image: image-registry.openshift-image-registry.svc:5000/**&lt;namespace bzw. project&gt;**/**&lt;name des images&gt;:&lt;tags&gt;**

und wählen den Workspace aus \(PVC - tekton-pvc\).

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.36.08.png)

Außerdem fügen wir bei "Show Credential Options" die Basic-Auth für Github mit einem Verweis auf unser vorhin angelegtes Secret ein.

Dann klicken wir auf "Start".



