# Pipeline anlegen

Nun erstellen wir eine generische Pipeline, welche für die Schritte

* Liniting
* Testing
* Building

genutzt werden kann.

Öffnet in der "Developer" Ansicht die Sektion "Pipelines" und klickt auf "Create Pipeline".

![](../../../.gitbook/assets/screenshot-2021-04-11-at-10.03.30.png)

Tragt den Namen `hello-world-pipeline` ein.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-10.04.47.png)

Wählt den Task "git-clone" aus.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-10.06.00.png)

Erstellt einen Parameter `git-url`.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.31.36.png)

Klickt auf den `git-clone` Task und fügt den Parameter `url` ein \(`$(params.git-url)`\).

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.33.07.png)

Fügt die Tasks `golangci-lint`, `golang-test` und `buildah-v0-16-3` als squentielle Task ein.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.34.58.png)

Das Ergebnis sieht dann so aus.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.37.27.png)

Erstellt drei Parameter `package`, `context` und `image`.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.40.33.png)

Passt das Package und den Context im `golangci-lint` und `golang-test` Task an.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.42.15.png)

Fügt den Parameter `image` und `context` im Buildah Task ein.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-13.43.38.png)

Da wir die interne Registry nutzen werden, müssen wir die TLS Verifikation ausschalten.

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.16.53.png)

Klickt auf "Save".

