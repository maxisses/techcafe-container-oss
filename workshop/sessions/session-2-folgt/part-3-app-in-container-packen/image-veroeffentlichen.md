# Image veröffentlichen

Um eure images allen verfügbar zu machen, macht euch einen Account auf Docker Hub: [https://hub.docker.com/](https://hub.docker.com/)

euren image namen findet ihr mit

```text
docker images
```

damit ihr euer image pushen könnt müsst ihr es mit eurem nutzernamen von dockerhub taggen

```text
docker tag <name eures images> <euer username>/<name eures images>
docker login
docker push <euer username>/<name eures images>
```

Jetzt kann jeder euer Image mit dem immer gleichen Workflow einsetzen:

```text
docker pull <euer username>/<name eures images>
docker run -p 3000:3000 <euer username>/<name eures images>
```

{% hint style="info" %}
Mit dem gleichen Workflow könntet ihr euch jetzt eine unendliche Anzahl an Open Source und kommerzieller software installieren zB von IBM \(ok bei IBM bzw. kommerziellen Produkten muss man meist noch was über sich preisgeben und paar AGBs akzeptieren\):  
[https://hub.docker.com/\_/db2-developer-c-edition](https://hub.docker.com/_/db2-developer-c-edition)[https://hub.docker.com/\_/ibm-websphere-liberty](https://hub.docker.com/_/ibm-websphere-liberty)  
und der Flow ist immer gleich:

docker pull  
docker run \(mit parametern natürlich\)
{% endhint %}

