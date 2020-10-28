# Workspace - gemeinsamen Storage anlegen

Klont euch das Repo für den heutigen Tag.

```text
git clone https://github.com/Javatar81/pipeline-examples.git
```

Legt einen gemeinsamen Workspace für unsere Pipeline-Files \(git Repo & Builds etc\) an, damit mehrere Runs hintereinander deutlich schneller werden.

```text
oc apply -f generic-pipeline/pvc/source-pvc.yaml
```

