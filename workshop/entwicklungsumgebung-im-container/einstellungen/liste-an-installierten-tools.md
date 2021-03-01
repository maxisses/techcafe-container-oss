# Liste an installierten Tools

| CLI Tool | Dokumentation |
| :--- | :--- |
| ibmcloud | [https://cloud.ibm.com/docs/cli?topic=cli-getting-started](https://cloud.ibm.com/docs/cli?topic=cli-getting-started) |
| git | [https://git-scm.com/docs](https://git-scm.com/docs) |
| kubectl | [https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) |
| helm | [https://helm.sh/docs/](https://helm.sh/docs/) |
| buildah | [https://github.com/containers/buildah/tree/master/docs](https://github.com/containers/buildah/tree/master/docs) |

Docker ist in dieser Umgebung aktuell nicht verfügbar. Deshalb muss statt

```text
docker build ...
```

```text
buildah bud
```

verwendet werden.

