# Traffic suspension mit Kiali

Für die Fault Injection nehmen wir uns noch mal den reviews Service vor. Und um es ein bisschen interessanter zu machen ärgern wir einige unserer User. Dazu gleich mehr.

{% hint style="info" %}
Chaos Engineering hat Netflix so richtig populär gemacht und während wir hier nur mal einen speziellen Service attackieren ist die Idee dahinter solche "VirtualServices", die wir schon kennengelernt haben jederzeit, überall, random für einen bestimmten Zeitraum zu deployen um die resilienz des System zu steigern.
{% endhint %}

Im ersten Schritt kann man einmal die Kiali mitgelieferte Traffic Suspension benutzen.

![](../../../.gitbook/assets/image%20%28110%29.png)

Was dann auch schnell in Kiali sichtbar wird wenn man Last auf die Anwendung bringt:

![](../../../.gitbook/assets/image%20%28109%29.png)

