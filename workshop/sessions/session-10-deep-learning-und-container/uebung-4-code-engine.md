# Übung 4: Die Cloud zur \(halben\) Rettung - Code Engine

Da es ein unglaublich einfach zu bedienendes Tool ist nehmen wir das brandneue Tool CodeEngine von IBM, welches es uns ermöglicht Container zu starten. Unter der Haube läuft kubernetes mit KNative. Davon merken wir aber nichts. 

Deshalb können wir Autoscaling nach Concurrent Request \(wer erinnert sich?\) erstellen und Memory und CPU requests \(wer erinnert sich?\) anlegen. Außerdem - wichtig - Umgebungsvariablen definieren. Das funktioniert so als würden sie im deployment.yaml eintragen \(wer erinnert sich? ;\) \).

Es wird wie wir das von OpenShift kennen ein Build "from Dockerfile" und "from Dockerimage" unterstützt.  
Der Gamechanger: CodeEngine eliminiert alle Limits die alle anderen functions-as-a-Service oder Container-Run Services am Markt bieten. Wir können unseren Container deshalb mit 32GB RAM und 8 vCPUs laufen lassen.

{% hint style="warning" %}
Leider bringt uns das für unser Neuronales Netz auch noch nicht so richtig auf Lichtgeschwindigkeit - denn CodeEngine unterstützt heute noch kein Deployment auf GPU Knoten. Man kann natürlich einen OpenShift oder Kubernetes  Cluster mit GPU-Nodes provisionieren - der Aufwand und die Kosten sind nur nicht ganz gerechtfertigt ;\)
{% endhint %}

Hier könnt ihr euch dann unseren Backend-Service anlegen: [https://cloud.ibm.com/codeengine/overview](https://cloud.ibm.com/codeengine/overview)  
  
Falls ihr mein Docker Image verwenden möchtet: 

```text
docker.io/maxisses/maxgpt2starter
```

Und für das Frontend liegt das Docker Image hier:

```text
docker.io/maxisses/gotminingui
```

Das könntet ihr auch **from Dockerfile** bzw. **from Source** bauen lassen: [https://github.com/maxisses/GoT-Mining-UI](https://github.com/maxisses/GoT-Mining-UI)

{% hint style="success" %}
Wichtig: Ihr müsst wieder die Umgebungsvariable GPT2SERVICEURL auf die URL des Backend-Services setzen, die euch die GUI von CodeEngine anzeigt.
{% endhint %}

Entweder ihr lasst beide Container direkt in CodeEngine laufen oder ihr deployed nur das backend hier und ändert die Variable 

![](../../.gitbook/assets/image%20%28167%29.png)

{% hint style="info" %}
Ergebnis: wir liegen wieder bei knapp einer Minute - das verwundert auch nicht, den auf meiner eigenen Maschine, wenn ich ohne GPU laufen lasse, kommt etwas ähnliches heraus und die hat 32GB RAM und 16 Cores.
{% endhint %}

