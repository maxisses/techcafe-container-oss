# Container Image bauen und in die private Registry verschieben.

## Build the container image

1. Zuletzt legen wir uns noch eine Umgebungsvariable für den Namen unserer App an.

   ```bash
   export MYPROJECT=<your-app-name>
   ```

2. Wenn nicht schon geschehen, wechselt in den Ordner der App.

   ```text
   cd $MYPROJECT
   ```

3. Stellt sicher das docker läuft.

   ```text
   docker ps
   ```

4. Baut, tagged \(`-t`\) und pushed das Container Image in die IBM Container Registry.

   ```bash
   docker build -t $MYREGISTRY/$MYNAMESPACE/$MYPROJECT:v1.0.0 .
   ibmcloud cr login
   docker push $MYREGISTRY/$MYNAMESPACE/$MYPROJECT:v1.0.0
   ```

