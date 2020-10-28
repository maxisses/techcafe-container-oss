# Code lokal ausführen & testen

* öffnet euren Editor \(in unserem Falle VS Code\)
* hilfreich: fügt links den Ordner mit eurem Code zum Workspace hinzu "Add workspace folder..."

![](../../../.gitbook/assets/image%20%2845%29.png)

* im linken bereich von VS Code rechte maustaste auf euren code ordner und "open in terminal", dadurch seid ihr mit einem Terminal direkt im richtigen Verzeichnis

```text
npm install
npm start
```

* im terminal müsst ihr npm install  \(dauert ca. 30 sec\) und npm start ausführen \(und - den befehl findet ihr übrigens auch in eurem manifest.yml wieder\)
* eure app ist verfügbar auf localhost:3000 bzw. 127.0.0.1:3000

{% hint style="info" %}
Mit Strg-C bzw. Ctrl-C könnt ihr sie beenden \(was notwendig ist, wenn ihr lokal comitten wollt, da die Anwendung für test-driven-development vorbereitet ist und vor jedem git commit standardmäßig tests ausgeführt werden; dazu wird die Anwendung erneut gestartet - was nicht funktioniert wenn Port 3000 bereits belegt ist\)
{% endhint %}

