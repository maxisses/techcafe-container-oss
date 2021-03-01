# optional: Cloud Loadbalancer und Ingress \(Domain\) für die App

Im letzten Schritt haben wir die Applikation wie in der vorigen Session über "NodePort" angesprochen.

IBM Kubernetes Cluster werden per Default mit einer Domain ausgestattet, welche wir nutzen können um unsere Applikation mit einer URL und auf dem Standard HTTP/HTTPS \(80/443\) freizugeben.

Diese Möglichkeit wird mittels des Ingresses konfiguriert. Darüber kann man wird dann eine Verbindung zum Service herstellen.

1. Ruft die **Ingress domain** eures Clusters ab:

   ```bash
   ibmcloud ks cluster get --cluster ${MYCLUSTER}
   ```

   oder über den Browser über die IBM Cloud:

\*\*\*\*

Den Ingress kann man sich über die CLI anzeigen lassen:

```bash
ibmcloud ks cluster get --cluster ${MYCLUSTER}
```

oder über die GUI:

![](../../../.gitbook/assets/image%20%28130%29.png)

die Ergebnisse sehen ähnlich aus

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

1. Erzeuge eine Ingress Konfiguration `ingress-ibmdomain.yml` die auf euere Domain zeigt \(HTTP oder HTTPS\). Im Folgenden findet ihr ein Template. Passt die Werte in den Klammern &lt;&gt; an den Ergebnisse aus dem ersten Schritt an. **service-name** findet ihr unter `==> v1/Service`. Man kann auch über `kubectl get svc` Namen des services herausfinden.

   ```yaml
   apiVersion: extensions/v1beta1
   kind: Ingress
   metadata:
     name: ingress-for-ibmdomain-http-and-https
   spec:
     tls:
     - hosts:
       -  <nameofproject>.<ingress-sub-domain>
       secretName: <ingress-secret>
     rules:
     - host: <nameofproject>.<ingress-sub-domain>
       http:
         paths:
         - path: /
           backend:
             serviceName: <service-name>
             servicePort: 9080
   ```

2. Deploy den Ingress

   ```bash
   kubectl apply -f ingress-ibmdomain.yml
   ```

   Eure Applikation erreicht ihr unter `https://<nameofproject>.<ingress-sub-domain>/`

Wechselt wieder in den Ordner /chart/&lt;name eurer App&gt;

```bash
cd /chart/<name eurer App>
helm upgrade ${MYPROJECT} . --namespace ${K8SNAMESPACE} --set image.repository=${MYREGISTRY}/${MYNAMESPACE}/${MYPROJECT}
```

Eure Applikation erreicht ihr dann unter:`https://<nameofproject>.<ingress-sub-domain>/`

