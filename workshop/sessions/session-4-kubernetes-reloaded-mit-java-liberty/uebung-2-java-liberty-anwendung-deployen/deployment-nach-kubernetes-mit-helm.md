# Deployment nach Kubernetes mit HELM



1. Wechselt auf der Kommandozeile in den Ordner Chart, dies ist der Ordner eures Helm Charts.

   ```bash
   cd chart/$MYPROJECT
   ```

2. Installiert die Anwendung mit Helm in eurem Kubernetes Cluster. Mit dem --set Tag passt man in der Datei values.yaml die Variable Repository an, um aus der korrekten Registry zu pullen.

{% hint style="danger" %}
Habt ihr eine langsame Leitung und der docker push aus der letzten Session läuft noch dann nehmt ein einfach ein anderes Image. Ihr findet alle bereits hochgeladenen hier: [https://cloud.ibm.com/registry/namespaces](https://cloud.ibm.com/registry/repos)
{% endhint %}

![](../../../.gitbook/assets/image%20%2862%29.png)

```bash
helm install ${MYPROJECT} . --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
```

