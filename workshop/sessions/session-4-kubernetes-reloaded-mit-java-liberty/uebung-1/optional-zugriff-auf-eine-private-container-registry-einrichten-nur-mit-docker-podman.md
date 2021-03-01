# optional: Zugriff auf eine private Container Registry einrichten - "nur mit Docker/Podman"

Führt man eben genannte Schritte in einer CI/CD Pipeline aus, möchte man möglicherweise lieber nicht auf eine proprietäre CLI eines Cloud Anbieters oder Container Registry Produktes zurückgreifen.

Dann kann man auf die IBM Container Registry folgendermaßen zugreifen:

```text
docker login -u iamapikey de.icr.io
```

Man muss dazu natürlich wissen, dass die Container Registry "de.icr.io" ist und man muss vorher einen API-Key anlegen, welchen man als Passwort verwendet: [https://cloud.ibm.com/iam/apikeys](https://cloud.ibm.com/iam/apikeys)

![](../../../.gitbook/assets/image%20%2863%29.png)

![](../../../.gitbook/assets/image%20%2873%29.png)



