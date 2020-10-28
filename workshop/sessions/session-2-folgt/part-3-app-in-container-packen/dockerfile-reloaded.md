# Dockerfile reloaded

* benennt das aktuelle "Dockerfile" diesmal in zB Dockerfilelinuxonly um:
* erstellt eine neue Datei mit Namen Dockerfile und packt folgendes rein:

Jetzt das File folgendermaßen befüllen

```text
###das linux ist schon dabei mit der entsprechenden node version, hier ist keine angegeben also wird "latest" genommen
FROM node


## jetzt wird ein ordner angelegt und in diesen gewechsel
RUN mkdir /app
WORKDIR /app


## jetzt werden von euren lokalen dateisystem dateien in das containerlinux kopiert und dann im container "npm install" ausgefügt
COPY package.json /app
RUN npm install --only=prod
COPY . /app


## container sind ISOLIERT, deshalb muss man sie so wie ihr zB euer lokales netzwerk für bestimmte anwendungen (zb 80 & 8080 sind immer freigegeben) freigebt irgendwo öffnen
EXPOSE 3000


## führe npm start aus
CMD ["npm", "start"]
```

Und jetzt seid ihr bereit eure Anwendung im Container auszuführen:

```text
docker build . -t meineappimcontainer
```

wenn fertig, seht ihr euer Image und die Größe:

```text
docker images
```

und jetzt startet euren Container:

```text
docker run -p 3000:3000 meineappimcontainer
```

... ihr kommt drauf wie immer: localhost:3000

Nur zum besseren Verständnis macht mal docker ps um die aktiven Container bzw. Linuxprozesse anzusehen:

```text
docker ps
```

Kopiert euch die Container ID und geht damit in den Container:

```text
docker exec -it <container id> /bin/bash
```

oder wenn ihr von alpine kommt \(da gibts kein /bin/bash\):

```text
docker exec -it <container id> sh
```

Auf der Kommandozeile des Containers:

```text
ls -al
```

{% hint style="info" %}
Ihr seid jetzt im container, auf dem Linuxbetriebssystem und könntet jetzt auch Dinge im container tun zB weitere Programme installieren, diese wären natürlich nicht persistent
{% endhint %}

