# Übung 4: \(optional\) Die Cloud zur \(halben\) Rettung - Code Engine

Da es ein unglaublich einfach zu bedienendes Tool ist nehmen wir den Container-Service CodeEngine von IBM, welches es uns ermöglicht Container laufen zu lassen ohne die Komplexität von OpenShift oder K8s handlen zu müssen. Unter der Haube läuft Kubernetes mit KNative. Davon merken wir aber nichts.

Deshalb können wir Autoscaling nach Concurrent Request \(wer erinnert sich?\) erstellen und Memory und CPU requests \(wer erinnert sich?\) anlegen. Außerdem - wichtig - Umgebungsvariablen definieren. Das funktioniert so als würden wir sie im deployment.yaml eintragen \(wer erinnert sich? ;\) \).

Es wird wie wir das von OpenShift kennen ein Build "from Dockerfile" und "from Docker Image" unterstützt.  
Der Gamechanger: CodeEngine eliminiert alle Limits die alle anderen functions-as-a-Service oder Container-Run Services am Markt bieten. Wir können unseren Container deshalb mit 32GB RAM und 8 vCPUs laufen lassen und sogar noch skalieren.

{% hint style="warning" %}
Leider bringt uns das für unser Neuronales Netz auch noch nicht so richtig auf Lichtgeschwindigkeit - denn CodeEngine unterstützt heute noch kein Deployment auf GPU Knoten. Man kann natürlich einen OpenShift oder Kubernetes Cluster mit GPU-Nodes provisionieren - der Aufwand und die Kosten sind nur nicht ganz gerechtfertigt ;\)
{% endhint %}

Hier könnt ihr euch dann unseren Backend-Service anlegen: [https://cloud.ibm.com/codeengine/overview](https://cloud.ibm.com/codeengine/overview)

Falls ihr mein Docker Image verwenden möchtet:

```text
docker.io/maxisses/gpt2inferencing:small
```

Das könntet ihr ebenfalls **from Dockerfile** bzw. **from Source** bauen lassen: [https://github.com/maxisses/GoT-Mining](https://github.com/maxisses/GoT-Mining-UI)  
sub-directory: /[gpt2-got](https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got)/**gpt2-model-inferencing**/

Und für das Frontend liegt das Docker Image hier:

```text
docker.io/maxisses/gotminingui
```

Das könntet ihr ebenfalls **from Dockerfile** bzw. **from Source** bauen lassen: [https://github.com/maxisses/GoT-Mining-UI](https://github.com/maxisses/GoT-Mining-UI)

{% hint style="success" %}
Wichtig: Ihr müsst wieder die Umgebungsvariable GPT2SERVICEURL auf die URL des Backend-Services setzen, die euch die GUI von CodeEngine anzeigt. Außerdem muss der Listening Port **3000** gesetzt werden.
{% endhint %}

Entweder ihr lasst beide Container direkt in CodeEngine laufen oder ihr deployed nur das backend hier und ändert die Variable

![](../../.gitbook/assets/image%20%28167%29.png)

{% hint style="info" %}
Ergebnis: wir liegen wieder bei knapp einer Minute - das verwundert auch nicht, den auf meiner eigenen Maschine, wenn ich ohne GPU laufen lasse, kommt etwas ähnliches heraus und die hat 32GB RAM und 16 Cores.
{% endhint %}

