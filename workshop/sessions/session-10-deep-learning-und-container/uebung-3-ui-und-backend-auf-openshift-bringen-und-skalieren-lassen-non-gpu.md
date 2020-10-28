# Übung 3: \(optional\) UI und Backend auf OpenShift bringen und skalieren lassen \(non-GPU :\( \)

Als ersten deployen wir den Backend-Service. Damit wir den Service "from Dockerfile", also neu bauen könnten, müssten wir das DeepLearning Modell neu gebaut haben, dort entsprechend im Build Ordner ablegen und dann das Dockerimage inklusive des DeepLearning Modells.

{% hint style="info" %}
Es bietet sich extrem an beide Images als 2 Steps in einen Tekton Task zu packen.
{% endhint %}

Da wir das nicht gemacht haben wählen wir einfach die Container Image Strategie um zu deployen \(OpenShift Console -&gt; Developer Ansicht -&gt; Add +\). Deployed **inklusive** einer Route. Es bietet sich außerdem an eine Resource Request einzurichten - das ist aber optional und dient dazu das wir hier einen Memory und Compute intensiven Pod haben werden, dem es hilft wenn er mehr Ressourcen zur Verfügung hat. Allerdings gilt es natürlich darauf zu achten, dass er überhaupt starten kann :\)

![](../../.gitbook/assets/image%20%28164%29.png)

Falls ihr mein Docker Image verwenden möchtet:

```text
docker.io/maxisses/maxgpt2starter
```

Die UI können wir hingegen auch über den eingebauten build Service von OpenShift deployen mit der "from Dockerfile" Strategie unter diesem git Repo: [https://github.com/maxisses/GoT-Mining-UI.git](https://github.com/maxisses/GoT-Mining-UI.git)

Schneller geht direkt from Image und das liegt hier:

```text
docker.io/maxisses/gotminingui
```

![](../../.gitbook/assets/image%20%28173%29.png)

{% hint style="success" %}
Wichtig: Ihr müsst die Umgebungsvariable GPT2SERVICEURL auf die Route-URL des Backend-Services setzen, die euch OpenShift anzeigt wenn ihr in der Developer-Topologie Ansicht auf den Service klickt und dort ist sie rechts unten zu sehen. Hintergrund - die UI Anwendung ruft den backend-Service aktuell Client-seitig \(also im HTML\) auf.
{% endhint %}

Wenn wir dann loslegen, stellt sich aber schnell Ernüchterung ein - DeepLearning mit einem Neuronalen Netz wie GPT2 braucht eben selbst beim Inferencing ein bisschen mehr Power.

236 Sekunden .... für einen Request \( vs. 8 Sekunden auf meiner Maschine mit GPU\). :\(

![](../../.gitbook/assets/image%20%28169%29.png)

Im nächsten Schritt schauen wir mal ob wir das besser hinbekommen.

