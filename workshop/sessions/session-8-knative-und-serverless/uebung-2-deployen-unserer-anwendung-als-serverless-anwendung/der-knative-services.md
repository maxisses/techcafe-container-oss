# Der KNative Services - am Bespiel des ratings Svc

Wie man im yaml unten für den ersten Service - den ratings Service unserer Bookinfo-Anwendung - an der apiVersion sieht implementiert KNative seine eigenen Ressourcen. Eine wesentliche, auf die wir uns heute fokussieren, ist der KNative Service. Es ist **nicht** das gleiche wie ein Kubernetes Service!

Ein KNative Service macht uns einiges leichter, denn er macht das Kubernetes Deployment, einen Kubernetes Services und, wenn nicht anders spezifiziert, sogar eine extern verfügbar Route für unser Deployment. Er verwaltet darüber hinaus Updates am Workload \(z.B. wenn man ein neues Image spezifiziert\) in Revisions, was einem auch wieder Traffic Mgmt Funktionalitäten ermöglicht. 



![](../../../.gitbook/assets/image%20%28125%29.png)

Hier ist das yaml-File um ratings als KNative Service zu deployen.

```text
oc apply -f https://raw.githubusercontent.com/maxisses/knative-on-openshift/master/ratings-kn.yaml
```

```text
apiVersion: v1
kind: ServiceAccount
metadata:
  name: bookinfo-ratings
  labels:
    account: ratings
---
apiVersion: serving.knative.dev/v1
kind: Service
metadata:
  name: ratings
  labels:
    app: ratings
    version: v1
    app.kubernetes.io/part-of: bookinfo
    serving.knative.dev/visibility: cluster-local
spec:
  template:
    metadata:
    spec:
      serviceAccountName: bookinfo-ratings
      containers:
      - name: ratings
        image: docker.io/istio/examples-bookinfo-ratings-v1:1.16.2
        imagePullPolicy: Always
        ports:
        - containerPort: 9080
```

Und OpenShift bringt eine GUI Integration für KNative mit - was die Arbeit und Übersicht deutlich vereinfacht.

![](../../../.gitbook/assets/image%20%28134%29.png)

Und es sollte uns noch etwas bekannt vorkommen, wenn wir auf den Pod clicken und schauen welche container in ihm laufen - wie bei Istio und ServiceMesh kommt der Envoy Proxy auch hier zum Einsatz.

![](../../../.gitbook/assets/image%20%28128%29.png)

Wir sehen auch schnell den "scale-to-zero", welcher per Default eingestellt ist, siehe Pod im Status "Terminating"

![](../../../.gitbook/assets/image%20%28132%29.png)



