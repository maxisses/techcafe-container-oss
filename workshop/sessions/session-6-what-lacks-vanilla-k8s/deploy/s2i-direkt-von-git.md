# Source2Image \(S2I\) Build & Deployment via WebConsole

Die letzte Komponente, die wir deployen ist die ProductPage. Diese wollen wir ohne Dockerfile direkt aus dem Sourcecode bauen und deployen. Dazu wählen wir +Add From Git aus.



* GIT Repo URL
  * [https://github.com/istio/istio.git](https://github.com/istio/istio.git)
* Context Dir
  * /samples/bookinfo/src/productpage
* Builder Image
  * Python
* Application Name
  * bookinfo
* Name
  * productpage
* Create Route
  * Yes

Hier sollten folgende Felder angepasst werden, damit OpenShift unser Dockerfile finden kann und die dazugehörigen Ressourcen erstellen kann.

 

