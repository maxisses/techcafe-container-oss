# Tasks anlegen \(2/2\)

### Helm-Chart Image Namen aktualisieren

Da wir ArgoCD für das Deployment nutzen wollen, müssen wir nun noch das Helm-Chart anpassen.

Und zwar mit dem Namen des gerade gepushten Image. Dafür nutzen wir den Folgenden Task:

```text
kubectl apply -f https://raw.githubusercontent.com/maxisses/golang-presentation/main/exercises/helloWorldAPI/tekton/update-helm-image.yaml
```

Die erforderlichen Parameter werden wie gehabt mit den bereits bekannten $\(params.image\) & $\(params.context\) befüllt. Im Task läuft nun ein Script ab, welches anhand des Image Params, die values.yaml des Helm-Charts updated.

### Änderungen ins git zurückpushen 

Dafür nehmen wir einen Cluster Task: "git-cli" und fügen ihn über die GUI nach dem helm-update Task hinzu. Diesem müssen wir vorher noch ein Kubernetes Secret zur Verfügung stellen zur Authentifizierung bei github.com, welches so aussieht \( Token: [https://github.com/settings/tokens](https://github.com/settings/tokens)\):

```text
kind: Secret
apiVersion: v1
metadata:
  name: push-helm-update-to-git
  annotations:
    tekton.dev/git-0: 'https://github.com'
data:
  password: <base 64 encoded github token>
  username: <base 64 encoded username>
type: kubernetes.io/basic-auth

```

{% hint style="info" %}
Man beachte die "annotation", welche tekton dieses secret bekannt macht und gleichzeitig den git server - github.com angibt.
{% endhint %}

Nun müssen wir noch den Task hinzufügen. Das geht tatsächlich am besten in der YAML-Ansicht der Pipeline um das "GIT\_SCRIPT" korrekt einzufügen.

```text
    - name: git-cli
      params:
        - name: BASE_IMAGE
          value: 'alpine/git:latest'
        - name: GIT_SCRIPT
          value: |
            echo | ls -al
            git fetch
            git checkout main
            git add .
            git commit -m "helmupdate"
            git push
        - name: GIT_USER_NAME
          value: <euer username>
        - name: GIT_USER_EMAIL
          value: <eure email>
      runAfter:
        - update-image-name-in-helm
      taskRef:
        kind: ClusterTask
        name: git-cli
      workspaces:
        - name: source
          workspace: shared-data
        - name: input
          workspace: shared-data
```

