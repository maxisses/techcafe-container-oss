# App erreichen aus dem Web

Für nutzen wir noch nicht den vorinstallierten Loadbalancer, welchen man üblicherweise nutzen würde um die App mit einer Domain im Netz verfügbar zu machen. Das würde man einen Ingress nennen und das kommt später. Jetzt nutzen wir die Funktion den Service ebenfalls per NodePort verfügbar zu machen.

* führt den Befehl aus:

```text
kubectl get services -n <eure-initialien>-projekt
```

* notiert euch das port mapping; wichtig ist nicht die 3000, sondern die zweite Zahl, der nodePort, also der geöffnete Port eures Kubernetes Worker Knotens: 32555
* den Port habt ihr, jetzt braucht ihr noch die öffentliche IP des Workers, die erfahrt ihr mit:

```text
kubectl get nodes -o wide
```

* kopiert die "EXTERNAL IP" und fügt den port an, bei mir so 173.193.85.173:&lt;3-Tag eures Geburtstags-Monat&gt;
* jetzt läuft eure WebApp in Kubernetes und ist erreichbar

{% hint style="info" %}
NodePort Lösung; normalerweise dient der "Service" nicht dazu die App über das Internet erreichbar zu machen; sondern um mit anderen Services bzw. dann Apps\(Deployments\) im Cluster zu kommunizieren --&gt; Verfügbarkeit im Netz stellt eine weitere Kubernetes Ressource, nämlich der "Ingress" zur Verfügung

internet  
       \|  
\[ Ingress \]  
   --\|-----\|--  
\[ Services \]  
 --\|---\|---\|---\|---  
    \[Pods\]
{% endhint %}

