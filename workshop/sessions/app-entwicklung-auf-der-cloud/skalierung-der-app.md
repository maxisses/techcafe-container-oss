# Skalierung der App

Nochmal zurück zu eurem Git-Projekt und dem manifest.yaml. Ruft es auf und klickt auf "Edit".

![](../../.gitbook/assets/image%20%282%29.png)

Ändert die "Instances" auf 2 und clickt unten auf Commit.

![](../../.gitbook/assets/image%20%287%29.png)

Geht jetzt in eure Delivery Pipeline um das Ergebnis zu überprüfen. Nämlich ein neues Deployment.

![](../../.gitbook/assets/image%20%2814%29.png)



{% hint style="info" %}
Wichtig ist zu verstehen das nun ein neues Deployment der Webanwendung gemacht wird. Wenn ihr in dem Deployment \(unter Resource List -&gt; CF Apps\) Änderungen gemacht habt werden diese jetzt gänzlich überschrieben. Die Wahrheit liegt im SCM bzw. git. Normalerweise würde diese Änderung nicht direkt auf dem Server im git erfolgen, das ist hier nur so um es zu vereinfachen. 
{% endhint %}

{% hint style="info" %}
Bezogen auf unsere Änderung im manifest kann man hier das Schlagwort Infrastructure-as-Code anbringen, denn es wird nicht imperativ festgelegt, sondern im yaml beschrieben bzwl. deklariert welche specs die Webanwendung haben soll.
{% endhint %}

