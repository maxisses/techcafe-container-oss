# Multi-stage Builds

Ein Multi-stage Build ermöglicht die größe von Images zu reduzieren. Man kopiert nur die notwendigen erzeugten Artefakte in ein möglichst kleines Base Image.

Kopiere den folgenden Inhalt in ein Dockerfile in einem leeren Ordner.

```text
FROM alpine as builder

RUN mkdir /app && \
    cd /app && \
    echo "Hello from the container Website" >> index.html

FROM nginx
COPY --from=builder /app/index.html /usr/share/nginx/html
```

Um das Docker Image zu erzeugen führe folgenden Befehl aus

```bash
docker build -t multi-stage:latest .
```

Und starte den Container

```bash
docker run --rm -p 8080:80 multi-stage:latest
```

Rufe jetzt im Browser [http://localhost:8080](http://localhost:8080) auf.

