# Nützliche Docker Befehle

Löschen aller gestoppten Containern

```bash
docker rm $(docker ps -qa)
```

Löschen aller ungenutzten Containern, Netzwerken, Images und Volumes.

```bash
docker system prune
```

