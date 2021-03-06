# Deployment nach Kubernetes mit HELM

## Deployment der Application



1. Um auf das Kubernetes Cluster zu zugreifen, klickt auf das erstellte Cluster \("connect via CLI"\).

{% hint style="danger" %}
Habt ihr eine langsame Leitung und der docker push aus der letzten Session läuft noch dann nehmt ein einfach ein anderes Image. Ihr findet alle bereits hochgeladenen hier: [https://cloud.ibm.com/registry/namespaces](https://cloud.ibm.com/registry/repos)
{% endhint %}

![](../../../.gitbook/assets/image%20%2893%29.png)

{% hint style="info" %}
Beim Security Status sehen wir, dass in unserem Container Image 37 Security-Issues existieren. Viele Container Registries bringen Out-of-the-Box einen Security Scan nach "Commom Vulnerabilites and Exposures" \(CVE\). CVE ist ein Industriestandard und ein Katalog bekannter Cybersicherheitslücken. Die 37 Lücken zeigen deutlich, dass man Updates für Basis-Images und Abhängigkeit immer aus einem durch Anbieter aktualisierte Kataloge abrufen sollte wie z.B. dem [https://catalog.redhat.com/](https://catalog.redhat.com/) Katalog.
{% endhint %}

1. Setzt eine Environment Variable mit dem Cluster Namen

   ```bash
   export MYCLUSTER=<CLUSTER_NAME>
   ```

[Helm](https://helm.sh/) ist eine Technologie um Applikationen in Kubernetes durch Helm Charts zu managen. Helm ermöglicht komplexe Applikationen zu definieren, installieren und zu upgraden.

Jetzt packt noch euren Kubernetes Namespace in eine Umgebungsvariable:

```bash
export K8SNAMESPACE=<euer Namespace>
```

Wir deployen jetzt mal trotzdem .... :\) Installiert die Anwendung mit Helm in eurem Kubernetes Cluster. Mit dem --set Tag passt man in der Datei values.yaml die Variable Repository an, um aus der korrekten Registry zu pullen.

1. Öffne den Chart Ordner:

   ```bash
   cd chart/$MYPROJECT
   ```

2. Installiere Den Chart:

   ```bash
   helm install ${MYPROJECT} . --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
   ```

```bash
helm install ${MYPROJECT} . --namespace ${K8SNAMESPACE} --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
```

Der Output sieht dann ungefähr so aus:

![](../../../.gitbook/assets/image%20%28106%29.png)

