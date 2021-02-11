# Anzahl der Layer

Die Befehle `RUN`, `COPY` und `ADD` erzeugen neue Layer im Container Image.

{% hint style="info" %}
Um sich die Layer eines Dockerfiles zu visualisieren kann [dive](https://github.com/wagoodman/dive) verwendet werden.
{% endhint %}

Als erste erzeugen wir ein Docker Images mit schlechter Nutzung der Layers. Kopiere den Inhalt in eine neue Datei `Dockerfile.bad`

```text
FROM ubuntu

RUN apt-get update
RUN apt-get install htop -y
RUN apt-get install jq -y
```

Erstelle das Image:

```bash
docker build -t layers:bad -f Dockerfile.bad .
```

Als zweites erzeugen wir ein Docker Image mit besserer Nutzung der Layers. Kopiere den Inhalt in eine neue Datei `Dockerfile.good`

```bash
FROM ubuntu

RUN apt-get update && \
    apt-get install htop -y && \
    apt-get install jq -y
```

Erstelle das Image:

```bash
docker build -t layers:good -f Dockerfile.good .
```

Jetzt vergleichen wir die Größen der beiden Images. Dafür führe den folgenden Befehl aus

```bash
docker images
```

Als Ergebnis sollten die beiden Images unterschiedlich groß sein:

```bash
REPOSITORY  TAG       IMAGE ID       CREATED              SIZE
layers      good      bd7780f81cb3   3 seconds ago        102MB
layers      bad       e51c8e977ba2   About a minute ago   103MB
```

Das Image `layers:good` ist um 1 MB kleiner als das Image `layers:bad`.

