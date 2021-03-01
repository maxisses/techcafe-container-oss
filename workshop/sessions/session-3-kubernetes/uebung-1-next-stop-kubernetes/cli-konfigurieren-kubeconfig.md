# CLI konfigurieren - kubeconfig

Loggt euch auf [www.cloud.ibm.com](https://cloud.ibm.com) ein.

* Wählt rechts oben bei eurem Account den neuen, für euch bereitgestellten Account aus über das Dropdown.

![](../../../.gitbook/assets/image%20%2865%29%20%281%29.png)

Entweder über Ressource List oder diesen Direktlink seht ihr einen Kubernetes Cluster: [https://cloud.ibm.com/kubernetes/clusters](https://cloud.ibm.com/kubernetes/clusters) 

* euren Cluster auswählen \([BAMFTechcafeK8sCluster](https://cloud.ibm.com/kubernetes/clusters/c0pqastf0q1128ov9na0/overview?region=eu-de&resourceGroup=ce468ccfdbfc47e2ae0e9c91324ee462&ace_config=%7B%22region%22%3A%22eu-de%22%2C%22crn%22%3A%22crn%3Av1%3Abluemix%3Apublic%3Acontainers-kubernetes%3Aeu-de%3Aa%2F4b5f219cdaee498f9dac672a896250ef%3Ac0pqastf0q1128ov9na0%3A%3A%22%2C%22resource_id%22%3A%22%22%2C%22orgGuid%22%3A%22%22%2C%22redirect%22%3A%22https%3A%2F%2Fcloud.ibm.com%2Fresources%22%2C%22bluemixUIVersion%22%3A%22v6%22%7D)\)

Um über eure CLI mit dem Cluster zu kommunizieren, müsst ihr eine kubeconfig erstellen. Das macht ihr so:

* auf dem Dashboard rechts oben "Actions" und **Connect via CLI**; im Schritt 1 recht "ibmcloud login" und dann eure nutzerdaten eingeben aus; schritt 2 & 3 exakt in den Terminal kopieren

![](../../../.gitbook/assets/image%20%2861%29.png)

![](../../../.gitbook/assets/image%20%2873%29%20%281%29.png)

```text
ibmcloud login -a cloud.ibm.com -r eu-de -g BAMFTechcafeSessions
##nicht den eigenen Account auswählen, sondern den neuen und "eu-de" als Region angeben
ibmcloud plugin install container-service
ibmcloud ks cluster config --cluster <eure ClusterID>
kubectl config current-context
```

![](../../../.gitbook/assets/image%20%2863%29%20%281%29.png)

Dann könnt ihr leicht prüfen ob alles läuft:

```text
kubectl get nodes
kubectl get pods
```

