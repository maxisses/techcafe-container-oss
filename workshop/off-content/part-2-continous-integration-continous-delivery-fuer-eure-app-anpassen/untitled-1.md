# Neue Delivery Pipeline auslösen

Änderung pushen und "neue" delivery pipeline damit auslösen:

```text
git add .
git commit -m "manifest für staging phase angepasst"
git push
```

Falls ihr die App bereits so geändert habt, dass die Testcases schief laufen könnt ihr auch:

```text
git commit -m "manifest für staging phase angepasst" --no-verify
```

