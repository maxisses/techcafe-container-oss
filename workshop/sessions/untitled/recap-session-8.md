# \[Archive\] ReCap Session 8

Im Ergebniss haben wir in Session 8 die Bookinfo Anwendung vollständig als KNative bzw. Serverless Anwendung deployed. Damit könnten wir Traffic Management/Roll Backs / Roll Forwards zwischen Updates in Deployments machen und könnten außerdem die Autoscaling Features nach Requests-per-Second und Concurrent Requests sowie die Scale to Zero Features \(haben wir nur für ratings konfiguriert\) nutzen.

![](../../.gitbook/assets/image%20%28145%29.png)

Wichtig ist, dass die Anwendung auch dazu passen muss. Ein Blick in die Logs eines der Pods des reviews Deployments zeigt, dass dies beim initialen Aufruf bzw. einem Aufruf nach einer gewissen Pause für bookinfo und den ratings-Service nicht gegeben ist. Er startet nicht schnell genug und der http-Request schlägt fehl. Je nach Typ der Anwendung müsste man mindestens eines der beiden Probleme lösen.

![](../../.gitbook/assets/image%20%28155%29.png)

Sobald der ratings-Service gestartet ist lässt sich dann auch der Traffic Split entsprechend beobachten.

![](../../.gitbook/assets/image%20%28156%29.png)

![](../../.gitbook/assets/image%20%28157%29.png)

Und wir sehen auch wie der Autoscaler, welchen wir für die productpage konfiguriert haben in Aktion tritt.

![](../../.gitbook/assets/image%20%28158%29.png)

