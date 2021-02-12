# UID, unprivileged und OpenShift

Aus Security Gründen erlaubt es OpenShift nicht Container mit einer vorgegebenen UID auszuführen. \(falls doch nötig muss der SSC anyuid vergeben werden\)

Jedoch wählt OpenShift einen zufällig UID aus der Root Group aus.

```bash
docker run --rm -u 1234 -p 8080:80 nginx:latest

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: can not modify /etc/nginx/conf.d/default.conf (read-only file system?)
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2021/02/12 09:04:36 [warn] 1#1: the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:2
nginx: [warn] the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:2
2021/02/12 09:04:36 [emerg] 1#1: mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
nginx: [emerg] mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
```

Es ergeben sich hier zwei Probleme  
- Der `unprivileged` Nutzer mit der UID `1234` hat nicht die nötigen Rechte. In OpenShift wäre das Container Image mit den Standard Security Einstellungen somit nicht lauffähig.  
- Der verwendete Standard Port `80` darf aus Sicherheitsgründen auch nicht genutzt werden.

Um sicherzustellen, dass das Image innerhalb OpenShift lauffähig ist, muss ein `unprivileged` Port verwendet werden und ein zufällig ausgewählter Nutzer der Root Group Zugriff haben.

Dafür erzeuge ein Dockerfile mit den notwendigen Anpassungen

```bash
FROM nginx

EXPOSE 8080

RUN sed -i "s/listen       80/listen       8080/g" /etc/nginx/conf.d/default.conf && \
    chgrp -R 0 /var/cache/nginx /var/run /var/log/nginx && \
    chmod -R g=u /var/cache/nginx /var/run /var/log/nginx
```

Baue das Container Image und starte den Container mit einem "zufälligen" Nutzer

```bash
docker build -t nginx-unprivileged:latest .
docker run --rm -p 8080:8080 -u 1234 nginx-unprivileged:latest
```

Rufe jetzt im Browser [http://localhost:8080](http://localhost:8080) auf.

