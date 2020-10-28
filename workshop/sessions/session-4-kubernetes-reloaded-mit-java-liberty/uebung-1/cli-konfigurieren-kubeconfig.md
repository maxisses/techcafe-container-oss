# CLI konfigurieren - kubeconfig

Um über eure CLI mit dem Cluster zu kommunizieren, müsst ihr eine kubeconfig erstellen. Das ist mit der ibmcloud cli automatisiert:

* [https://cloud.ibm.com/kubernetes/clusters](https://cloud.ibm.com/kubernetes/clusters) 
* euren cluster auswählen \(falls ihr den standard gelassen habt ist es: mycluster\)
* optional: rechts oben Kubernetes Dashboard anwählen in neuem Tab öffnen und dann links auf "Deployments" klicken \(für später\)
* auf dem Dashboard rechts oben "Actions" und connect via cli; im Schritt 1 recht "ibmcloud login" und dann eure nutzerdaten eingeben aus; schritt 2 & 3 exakt in den Terminal kopieren

{% hint style="info" %}
Wichtig: Wählt nach Eingabe eures Logins nicht euren Account aus, sondern den des Gastgebers aus.
{% endhint %}

```text
ibmcloud login -a cloud.ibm.com -r eu-de -g labinaboxdrvresgroup
ibmcloud ks cluster config --cluster <eure ClusterID>
kubectl config current-context
```

![](../../../.gitbook/assets/image%20%2833%29.png)

Dann könnt ihr leicht prüfen ob alles läuft:

```text
kubectl get nodes
kubectl get pods
```

