# SSH Keys für Kommunikation mit git remote

In der letzten Session habt ihr eine App auf der IBM Cloud deployed. Dazu eine Delivery Pipeline und ein git Repo. Den Code wollen wir jetzt haben um mit ihm lokal zu arbeiten, ihn zu containerisieren und dann auf Kubernetes laufen zu lassen.

Als erstes müssen wir SSH Keys erzeugen für sichere Kommunikation zwischen eurem Rechner und der IBM Cloud bzw. dem gitlab-Server. Dazu macht folgendes:

* IBM Cloud --&gt; Ressource List --&gt; Developer Tools aufklappen --&gt; eure Toolchain anklicken --&gt; git Kachel auswählen --&gt; rechts oben euren Nutzer und Settings auswählen --&gt; links "SSH Keys" anklicken --&gt; "generate one"
* lokal einen Terminal öffnen und folgendes eingeben:

```text
ssh-keygen -t ed25519 -C "nameeuresschlüssels"
```

* Standardeinstellungen bestätigen
* Passwort für euren SSH key setzen \(oder leerlassen\) und bestätigen
* SSH Key kopieren:
  * macOS:

```text
pbcopy < ~/.ssh/id_ed25519.pub
```

* windos: cat ~/.ssh/id\_ed25519.pub \| clip

```text
cat ~/.ssh/id_ed25519.pub | clip
```

* zurück zum Browser und den SSH key einfügen und "Add Key" Button drücken

