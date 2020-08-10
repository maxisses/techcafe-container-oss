# Team für die Arbeit am Code aufsetzen



* geht in euer git Projekt Überblich auf der Cloud

![](../../../.gitbook/assets/image%20%2835%29.png)

* dann im gitlab project overview links runterscrollen und settings --&gt; Members anwählen und entsprechende Collaborator hinzufügen
* da die ssh infrastrukur bereits aufgesetzt ist kann der hinzugefügte jetzt sofort clonen

```text
git clone git@<euer repo name>
```

* um zu testen kann der hinzugefügte jetzt den ordner am besten wieder zu seinem VS Code Workspace und macht rechte maustaste auf ihn "open in terminal"

```text
git branch
git branch neuesfeature_branch 
git branch
git checkout neuesfeaturebranch_euername
git status 
git add . 
git status 
git commit -m "...."
git push
```

Das geht noch nicht, da der erzeugte Branch nur lokal existiert, deshalb:

```text
git push --set-upstream origin neuesfeaturebranch_euername
```



