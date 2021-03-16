# YAML des Kiali-generierten VirtualService inspizieren

Wenn ihr nach Erstellung in Kiali in den Details vom reviews Service runterscrollt findet ihr einen VirtualService. Schaut euch das YAML dazu an. Kiali hat uns schonmal ein Template für Fault Injection erstellt. Wir können an den Keys im YAML schon erahnen, dass man da einiges tunen kann. U.a. kann man eine bestimmte Prozentzahl an Request scheitern lassen und den entsprechenden http-Status zurückgeben. In diesem Falle [503 - Service Unavailable](https://developer.mozilla.org/de/docs/Web/HTTP/Status/503).

![](../../../.gitbook/assets/image%20%2897%29.png)

![](../../../.gitbook/assets/image%20%28102%29.png)

