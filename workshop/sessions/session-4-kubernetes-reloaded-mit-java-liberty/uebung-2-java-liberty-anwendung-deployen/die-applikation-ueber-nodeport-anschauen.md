# Die Applikation über NodePort anschauen

## Anzeigen der Applikation

1. Zeigt die Kubernetes services im Cluster an:

   ```bash
   kubectl get services --all-namespaces
   ```

2. Sucht den zu eurer Applikation passenden service. Der Name ist der gleiche wie euer Projekt.

   Falls im Namen "-" enthalten sind, kann es sein dass die entfernt werden, z.B. `my-project` wird zu  `myproject`.

3. Merkt euch den Port des service. Der Port ist eine 5-stellig Nummer\(z.B., 31569\). Den Wert findet ihr unter `PORT(S)`.
4. Holt euch die externe IP des worker nodes mit:

   ```bash
   kubectl get nodes -o wide
   ```

5. Ihr könnt auf die Applikation unter `http://worker-ip-address:portnummmer/` zugreifen.

