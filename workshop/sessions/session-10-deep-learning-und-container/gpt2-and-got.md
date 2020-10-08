# Übung 2: Text Generator im Container ausführen

Die Ausführung wird durch Container noch einfacher. Man muss lediglich den Output des ersten Container Runs in folgenden geclonten git folder kopieren:

{% embed url="https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-start" %}

Und danach kann man auch schon wieder mit Docker weitermachen.

Build the docker Image with

```text
docker build -t yourgpt2starter .
```

Run the docker image 

```text
docker run -p 8080:8080 yourgpt2starter
```

AND/OR if you have GPUs

```text
docker run -p 8081:8080 --gpus all yourgpt2starter
```

Depending on your GPU the difference for inferencing is **tremendous** - for me it was 12x faster with 1 Geforce RTX2080 Super. The logs show you whether a GPU had been used an how long one request took.

Jetzt können wir mal testen wie schnell uns Text generiert wird mit:

```text
curl localhost:8080 ##cpu
curl localhost:8081 ##gpu
```

Ich habe einen Timer in die App eingebaut. Ein Blick auf die Logs mit GPU sieht ganz gut aus - man bedenke, wie groß das Modell ist:

![](../../.gitbook/assets/image%20%28166%29.png)

Und ohne GPUs ist man weit entfernt:

![](../../.gitbook/assets/image%20%28165%29.png)

