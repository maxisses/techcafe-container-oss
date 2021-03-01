# Zugriff auf eine private Container Registry einrichten - "Convenient"

Der DockerHub ist natürlich nicht der ideale Ort für die eigenen Applikationen. Cloud Provider stellen üblicherweise eine Registry zur Verfügung. Bei IBM ist es die IBM Container Registry. Wir sehen sie gleich neben dem Kubernetes Cluster hier: [https://cloud.ibm.com/registry/namespaces](https://cloud.ibm.com/registry/namespaces)

{% hint style="info" %}
Nicht vergessen auf die richtige Region zu filtern \(Frankfurt\)
{% endhint %}

Die "universelle" Methode um mit Container Registries zu arbeiten ist das Container Werkzeug der Wahl, also vermutlich docker oder podman, zu nutzen. Jeder Cloud Provider bringt natürlich für die Arbeit mit **seiner** Registry Convenience Funktionen mit. Dies tun im übrigen auch die Anbieter von Container Registries. 

1. Um mit der Registry arbeiten zu können müssen wir sie über die CLI erreichbar machen. Dafür wird die cr-Erweiterung des ibmcloud CLI Tools genutzt.

   ```bash
   ibmcloud plugin install container-registry
   ibmcloud cr region
   ```

2. Weil es später beim pushen einiges erleichtert, definiert eine Umgebungsvariable für die URL der IBM Container Registry: `MYREGISTRY`

   ```bash
   export MYREGISTRY=de.icr.io
   ```

3. Mit folgendem Befehl seht ihr die Verfügbaren "Bereiche" bzw. Namespaces in denen ihr Images ablegen könnt. Beim DockerHub entsprach der Namespace eurem Benutzernamen. 

{% hint style="warning" %}
Diese Registry Namespaces sind nicht zu verwechseln mit Kubernetes Namespaces!
{% endhint %}

```bash
ibmcloud cr namespaces
```

{% hint style="info" %}
Ihr habt in dem Workshop-Account keine Rechte dazu, aber mit folgendem Befehl könntet ihr z.B. auf eurem eigenen Account weitere Bereiche anlegen:

```bash
ibmcloud cr namespace-add <REGISTRY_NAMESPACE>
```
{% endhint %}

Zuletzt könnt ihr noch eine Umgebungsvariable `MYNAMESPACE` für den eben angegebenen Namespace definieren, damit ihr diese in späteren Befehlen verwenden könnt.

```bash
export MYNAMESPACE=techcaferegistry
```

