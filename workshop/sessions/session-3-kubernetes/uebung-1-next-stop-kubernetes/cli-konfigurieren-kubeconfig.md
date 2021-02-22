# CLI konfigurieren - kubeconfig

Um über eure CLI mit dem Cluster zu kommunizieren, müsst ihr eine kubeconfig erstellen. Das ist mit der ibmcloud cli automatisiert:

* [https://cloud.ibm.com/kubernetes/clusters](https://cloud.ibm.com/kubernetes/clusters) 
* Wählt oben bei eurem Account den für euch bereitgestellten 
* euren cluster auswählen \(falls ihr den standard gelassen habt ist es: mycluster\)
* optional: rechts oben Kubernetes Dashboard anwählen in neuem Tab öffnen und dann links auf "Deployments" klicken \(für später\)
* auf dem Dashboard rechts oben "Actions" und connect via cli; im Schritt 1 recht "ibmcloud login" und dann eure nutzerdaten eingeben aus; schritt 2 & 3 exakt in den Terminal kopieren

```text
ibmcloud login -a cloud.ibm.com -r eu-de -g labinaboxdrvresgroup
ibmcloud plugin install container-service
ibmcloud ks cluster config --cluster <eure ClusterID>
kubectl config current-context
```

![](../../../.gitbook/assets/image%20%2833%29.png)

Dann könnt ihr leicht prüfen ob alles läuft:

```text
kubectl get nodes
kubectl get pods
```

