# Tasks anlegen

Es gibt eine Übersicht an Tekton Tasks welche von der Open Source Community maintained werden.

{% embed url="https://github.com/tektoncd/catalog" %}

{% embed url="https://hub.tekton.dev" %}

Navigiert zum Tekton Hub und sucht nacht "Golang".

![](../../../.gitbook/assets/screenshot-2021-04-11-at-09.56.04.png)

Wählt "golangci lint" aus und kopiert den "install" Befehl.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-09.57.32.png)

![](../../../.gitbook/assets/screenshot-2021-04-11-at-09.57.42.png)

```text
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/golangci-lint/0.1/golangci-lint.yaml
```

Die gleichen Schritte führt ihr für den "golang test" Tasks aus.

```text
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/golang-test/0.1/golang-test.yaml
```

Danach sollten beide Tasks in der "Administrator" Übersicht unter "Pipelines" unter "Tasks" auftauchen.

![](../../../.gitbook/assets/screenshot-2021-04-11-at-10.00.37.png)



