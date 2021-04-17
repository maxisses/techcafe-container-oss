# ArgoCD GUI

Logged euch in der ArgoCD Oberfläche ein.

Username: admin

Password:

```text
oc get secret argocd-cluster-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d
```

{% embed url="https://argocd-cluster-server-openshift-gitops.ocpclusterpub-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud/applications" %}

Damit sehen wir die ArgoCD Übersicht. Wir nutzen für die restlichen Sessions alle den Admin Nutzer.

![](../../../.gitbook/assets/screenshot-2021-04-17-at-15.10.06.png)

{% hint style="info" %}
Alle Informationen zu ArgoCD findet ihr [hier](https://argoproj.github.io/argo-cd/).
{% endhint %}

{% hint style="info" %}
Um in der aktuellen Variante ArgoCD vollen Zugriff auf das Cluster zu geben muss folgender Befehl ausgeführt werden. In unserem Fall wurde die Policy schon angepasst.
{% endhint %}

```text
oc adm policy add-cluster-role-to-user cluster-admin -z argocd-cluster-argocd-application-controller -n openshift-gitops
```

