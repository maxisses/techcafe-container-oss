# \[Optional\] Image testen

Wer mag kann gerne das Go Image schon einmal testen.

Unter Topology wählen wir "Container Image" aus.

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.50.10.png)

Wählt "Image stream from internal registry" aus und wählt euer Image und Tag aus. Dann klickt auf "Create".

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.50.57.png)

Wenn die Applikation gestartet ist, klicken wir auf die Route.

![](../../../.gitbook/assets/screenshot-2021-04-14-at-22.53.20.png)

Als Ergebnis erhalten wir 

```text
{"message": "not found"}
```

Wenn wir an die Ende der Route noch `/api/v1/hello` hinzufügen \(`<...>cloud/api/v1/hello`\) erhalten wir

```text
{"message": "Hello World"}
```

