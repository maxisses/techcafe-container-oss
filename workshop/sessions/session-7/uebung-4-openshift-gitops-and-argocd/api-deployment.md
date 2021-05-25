# API Deployment

Wir erstellen eine neue Applikation indem wir auf "New App" klicken.

![](../../../.gitbook/assets/screenshot-2021-04-17-at-15.35.17.png)

Wir geben unserer Applikation einen Namen "&lt;eure Initialien&gt;-api" und wählen als Project "default" aus. Für die "Sync Policy" wählen wir "Automatic" und machen ein Häckchen bei "Prune Resources" und "Self Heal". Damit synchronisiert ArgoCD den Stand im git konstant mit dem Stand im Cluster. \(Das testen wir später auch noch\).

![](../../../.gitbook/assets/screenshot-2021-04-17-at-15.40.12.png)

In der "Repository URL" tragen wir die URL unseres geforkten git-Repos ein und setzen den "Path" auf den Helm Chart "./exercises/helloWorldAPI/charts/go-api/". ArgoCD überprüft sofort das Repository und stellt die folgenden Settings für einen Helm Chart ein.

![](../../../.gitbook/assets/screenshot-2021-04-17-at-15.39.31.png)

Für das Ziel der Applikation wählen wir die "Cluster URL" https://kubernetes.default.svc aus. Das funktioniert, da die ArgoCD Instanz im selben Cluster läuft. Im Feld "Namespace" tragt ihr euren Namespace ein.

![](../../../.gitbook/assets/screenshot-2021-04-17-at-15.39.38.png)

Man kann nun sehen, dass ArgoCD erkannt hat, dass wir mittels Helm-Chart deployen wollen und der in der Pipeline definierte Name des Images sollte hier auftauchen.

![](../../../.gitbook/assets/screenshot-2021-04-17-at-16.06.39.png)

{% hint style="info" %}
Wer bereits mit Helm tiefer gearbeitet hat wird hier erkennen, das ArgoCD eine schöne Möglichkeit bietet die [Parameter](https://helm.sh/docs/topics/charts/#templates-and-values) eines [Charts](https://helm.sh/docs/topics/charts/) anzupassen.
{% endhint %}

Dann klicken links oben wir auf "Create".

