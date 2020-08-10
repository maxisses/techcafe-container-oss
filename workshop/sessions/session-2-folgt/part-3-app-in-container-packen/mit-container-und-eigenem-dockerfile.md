# Mit Container und eigenem Dockerfile

* öffne VSCode, dort findest du bereits deine Anwendung
* da ist ein Dockerfile; das benutzen wir erstmal nicht deshalb benenne es um in "Dockerfileoriginal"
* clicke rechte maustaste im VsCode links auf deinen Ordner und wähle "New File", nenne es "Dockerfile"

![](../../../.gitbook/assets/image%20%2825%29.png)

Jetzt das File folgendermaßen befüllen

```text
###alpine ist eine super abgespeckte LinuxVersion optimiert für container, hier wird also ein linux "installiert"
FROM alpine 


## jetzt wird auf dem linux node.js und npm installiert
RUN apk add --update nodejs npm


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

