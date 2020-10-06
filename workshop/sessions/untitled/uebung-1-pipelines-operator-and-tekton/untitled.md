# Projekt anlegen

Die Ressource Project ist eine OpenShift spezifische Erweiterung von Kubernetes. Jedes Projekt erhält auch seinen gleichnamigen Kuberntes Namespace. Projekte können u. a. für folgende Use Cases genutzt werden:

* Separate Namespaces für Applikationen und andere Ressourcen.
* Berechtigungen können auf Projektebene vergeben werden, um z. B. nur bestimmten Teams Zugriff zu gewähren.
* Trennung der Projekte auf Netzwerkebene durch _NetworkPolicies_.
* Definition von Resource Quotas auf Projektebene.
* nicht zuletzt kann durch die Kombination der oberen Punkte eine komplette Mandantentrennung vollzogen werden.

Damit wir unsere neue Applikation Bookinfo bauen und deployen können müssen wir uns zunächst ein neues Projekt anlegen.

### OC CLI

```text
oc new-project <initialien>-bookinfo-tekton
```

### **OpenShift Console / GUI**

![](../../../.gitbook/assets/image%20%28151%29.png)

