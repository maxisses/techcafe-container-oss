# Yaml exportieren

Wenn ihr nach Erstellung in Kiali runterscrollt findet ihr einen VirtualService. Schaut euch das YAML dazu an. Kiali hat uns schonmal ein Template für Fault Injection erstellt. Wir wollen es so anpassen, dass nur unser v3 Service fehlerhaft ist, weil er zB schlecht implementiert wurde und v2 weiterhin super läuft.  
Dazu können wir uns am YAML aus dem DarkRelease Teil orientieren. 

![](../../../.gitbook/assets/image%20%2897%29.png)

![](../../../.gitbook/assets/image%20%28101%29.png)

