# Pipeline ausführen

In der Pipeline Übersicht wählen wir unter "Actions" "Start" aus.

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.34.07.png)

Wir fügen die folgenden Parameter ein

* git-url: [https://github.com/wumaxd/golang-presentation](https://github.com/wumaxd/golang-presentation)
* package: api
* context: ./exercises/helloWorldAPI

{% hint style="danger" %}
Ins Image unten euren Namespace einsetzen
{% endhint %}

* image: image-registry.openshift-image-registry.svc:5000/**&lt;namespace bzw. project&gt;**/go-test-image:latest

und wählen den Workspace aus \(PVC - tekton-pvc\).

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.36.08.png)

Dann klicken wir auf "Start".



