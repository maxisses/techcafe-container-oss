# Applikation HelloWorldAPI

{% embed url="https://github.com/wumaxd/golang-presentation/tree/main/exercises/helloWorldAPI" %}

Die Applikation basiert auf [Go\(lang\)](https://golang.org) und erzeugt einen simplen HTTP Endpunkt `api/v1/hello`.

Wir werden im folgenden eine Pipeline bauen welche:

* Das Repository cloned
* Linting des Codes
* Unit Tests ausführt
* Ein Container Image erzeugt
* Das Container Image in die interne Registry pushed
* Das Helm Chart patchen mit dem Namen des gepushten Container Images
* Mit einem git push, die Änderung ins git zurückspielen

![](../../../.gitbook/assets/image%20%28180%29.png)

