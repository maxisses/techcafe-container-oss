# Build Context

Dateien welche sich im Build Context befinden, jedoch nicht für das Image relevant sind, vergrößern den Build Context und somit auch die Größe des Images. Des Weiteren wird dadurch auch die Build-Zeit, die Pull- und Push-Zeit und die Container Runtime Größe verlängert bzw. vergrößert.

Die Größe des Build Context wird beim Erzeugen des Images angezeigt.

```bash
docker build --no-cache -t helloapp:v2 .
Sending build context to Docker daemon  187.8MB
```

