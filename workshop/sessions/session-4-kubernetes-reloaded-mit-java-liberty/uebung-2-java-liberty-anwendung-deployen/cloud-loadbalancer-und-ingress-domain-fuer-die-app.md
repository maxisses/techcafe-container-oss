# optional: Cloud Loadbalancer und Ingress \(Domain\) für die App

Im letzten Schritt haben wir die Applikation wie in der vorigen Session über "NodePort" angesprochen.

IBM Kubernetes Cluster werden per Default mit einer Domain ausgestattet, welche wir nutzen können um unsere Applikation mit einer URL und auf dem Standard HTTP/HTTPS \(80/443\) freizugeben.

Dafür nutzen wir das Kubernetes Feature **Ingress:**

\*\*\*\*

Den Ingress kann man sich über die CLI anzeigen lassen:

```bash
ibmcloud ks cluster get --cluster ${MYCLUSTER}
```

oder über die GUI:

![](../../../.gitbook/assets/image%20%28130%29.png)



Erstellt eine Datei`ingress.yml` im Ordner **chart/&lt;name eurer app&gt;/templates**  
Ersetzt alle Werte &lt;&gt; mit den Werten für die Subdomain.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: <name-eurer-app>
spec:
  tls:
  - hosts:
    -  <app name>.bamftechcafek8scluster-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud
    secretName: bamftechcafek8scluster-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000
  rules:
  - host: <app name>.bamftechcafek8scluster-39df0ed7a3c2ec1b2ad7d1247807cc2f-0000.eu-de.containers.appdomain.cloud
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: <name eures Svc "kubectl get svc -n ...">
            port:
              number: 9080
```

Wechselt wieder in den Ordner /chart/&lt;name eurer App&gt;

```bash
cd /chart/<name eurer App>
helm upgrade ${MYPROJECT} . --namespace ${K8SNAMESPACE} --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
```

Eure Applikation erreicht ihr dann unter:`https://<nameofproject>.<ingress-sub-domain>/`

