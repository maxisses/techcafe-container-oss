# Deployment, Service & Namespace YAML parametrisieren mit HELM

Wenn man viele Kubernetes-YAML Dateien erstellt wiederholen sich einige Werte häufig. Außerdem möchte man häufig alle Updates auf die Konfigurationsdateien auf einmal in einem Release verpacken. Dazu kann man HELM verwenden.

Am deutlichsten wird das am Beispiel. Hier ist ein Helm Chart für die Beispielanwendung von eben:

```text
git clone https://github.com/maxisses/techcafe-easy-helmchart.git
cd techcafe-easy-helmchart
```

Nun passt man in der "values.yaml"-Datei einige Werte an. In unserem Falle den Applikationsnamen, den Namespace sowie ggf. das Image repository. Im "Templates" Ordner liegen die bereits bekannten YAML-Dateien von eben, allerdings diesmal parametrisiert auf Basis der "values.yaml"-Datei.

Auch den nodePort sollte man anpassen. Allerdings nicht auf den gleichen Wert wie zuvor, denn der ist ja bereits belegt, falls man den Service nicht schon gelöscht hat.

Mit einem einfach Befehl kann man dann ausrollen

```text
helm install <zB name der Applikation> .
##anzeige & Status mit:
helm list
```

Danach laufen die Ressourcen wie gewohnt im Cluster und sind mit den bekannten Befehlen abrufbar.

```text
kubectl get deployments -n <im helm chart eingetragener namespace>
kubectl get pods -n <im helm chart eingetragener namespace>
kubectl get services -n <im helm chart eingetragener namespace>
```

Nach einem Update von Werten kann man ein neues Helm Release mit:

```text
helm upgrade <zB name der Applikation> .
```

