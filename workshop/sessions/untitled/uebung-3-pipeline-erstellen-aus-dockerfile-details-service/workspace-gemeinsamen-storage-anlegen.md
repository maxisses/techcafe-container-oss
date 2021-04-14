# Workspace - gemeinsamen Storage anlegen

Wir erstellen einen PVC welcher genutzt wird zwischen den Tasks Daten zu speichern.

```text
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: tekton-pvc
spec:
  storageClassName: ibmc-block-bronze
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  volumeMode: Filesystem
```



