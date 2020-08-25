# optional: lokale Tests in Delivery Pipeline einbinden

Nach der Build Phase ist hilfreich zu testen ob die lokalen Tests auch auf der Cloud Infrastruktur erfolgreich sind. Dafür kann man eine weitere Test Phase einsetzen und im einfachsten Falle folgendes im Skript der Phase einfügen. 

```text
#!/bin/bash
#Invoke tests here
set -e
npm install
npm run test
echo "$?"
```

![](../../.gitbook/assets/image%20%2832%29.png)

{% hint style="info" %}
Bei node.js Anwendungen kann man in package.json zb "npm run test" definieren. In diesem Falle wird mit mocha getestet. Die Files sind im Ordner "test".
{% endhint %}



