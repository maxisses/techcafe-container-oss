---
description: Mit git clone oder ibmcloud dev
---

# Java Starter Anwendung erstellen

In der GUI der IBM Cloud haben wir in[ Session 1 einen App Katalog](https://max-dargatz.gitbook.io/bamf-techcafe/sessions/app-entwicklung-auf-der-cloud/ueubung-1-hello-world-auf-ibm-cloud/starter-app-deployen) mit Starter Kits \(oder Applikationstemplates \) gesehen. Wir haben daraus das Node.JS + Express Starter Kit gewählt.  
Jede Cloud bietet den Zugriff auf diese Templates, angepasst für die sepzifische Deployment-Plattform \(in unserem Falle Kubernetes\), auch über die CLI an. Wir werden in einer späteren Session \(vorr. Session 6\) sehen wie man mit OpenShift so einen Katalog mit Templates auch in der eigenen Organisation anbieten kann.

1. Mit `ibmcloud dev` cloned man sich eine Applikation aus einem Katalog und erstellt lokal den Ordner.

   ```text
   ibmcloud dev create
   ```

   Folgt jetzt den Instruktionen auf der CLI.

2. Wählt `Backend Service / Web App` &gt; `Java - MicroProfile / JavaEE` &gt; `Java Liberty App` aus um eine Java Liberty Starter Anwendung zu erstellen
3. Gebt eurer App einen Namen, alles Kleinbuchstaben`<your-initials>kubeapp`
4. Keine zusätzlichen Service hinzufügen \("n"\)
5. Wählt die 3. Option: "`No DevOps, with manual deployment "`
6. Wählt die 1. Option: "Deploy to Helm-based Kubernetes containers

Damit generiert ihr euch einen Starter \(genau wie in Session 1\), habt ihn aber direkt auf dem Rechner. Dadurch, dass ihr "Helm-based" als Deployment-Option gewählt habt, ist neben dem Dockerfile auch ein Helm Chart im Ordner als Konfigurationsdatei enthalten. 

