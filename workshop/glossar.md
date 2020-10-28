# Glossar

## Grundlagen & Container

| Begriff | Erklärung |
| :--- | :--- |
| Container Image | Layered file system where each layer references the layer below |
| Dockerfile | build script für Containerimage |
| Container Prozess | runtime instance of an image plus a read/write layer |
| OCI | Open Container Initiative - Standard wie Container Images gebaut werden |
| CRI | Container Runtime Interface - Standard für Container Engines um von Kubernetes genutzt werden zu können |
| Cloud Foundry | Platform-as-a-Service Angebot mit starkem Entwicklerfokus um deployments so einfach wie möglich zu machen. Nutzt für den Anwender nicht sichtbar ebenfalls container - man deployed aber keine docker images selber. |
| Delivery Pipeline | Übernimmt automatisiertes Deployment in mehreren Stages, mit Test, Integration und in mehrere Umgebungen |
| Toolchain | Eine DevOps Toolchain geht über CI/CD und Delivery Pipelines hinaus und integriert z.B. ein git aber auch Slack/Teams, Monitoringtools, externe Testsuiten, Definition von Quality Gates etc. |
| git | Source Control Management |
| gitlab | Ein SCM Produkt neben Bitbucket und github. |
| container registry \(image registry\) | hier werden gebaute container images abgelegt, in versionskontrolle & entsprechend getagged |
|  |  |

## Kubernetes

| Begriff | Erklärung |
| :--- | :--- |
| Pod | Wrapper für ein oder mehrere Container mit eigener IP |
| ReplicaSet | Definiert den "desired state" für eine Anwendung, welche aus n Pods bestehen kann |
| Deployment | Definiert die UpdateStrategie für eine Anwendung und wie neue Versionen von Pods ausgerollt werden |
| Kubernetes Service | Internes load-balancing und erreichbarkeit von pods |
| Liveness Probes | Lieber Pod, gibts dich noch? |
| Readiness Probes | Lieber Pod, kannst du Traffic vertragen oder bist du zu beschäftigt? |
| Canary Deployments | Ein _Canary-Release_ verwendet man, um das Risiko bei der Einführung einer neuen Software-Version zu vermindern |
| HPA - horizontal pod autoscaling | Der Horizontal Pod Autoscaler skaliert automatisch die Anzahl der Pods eines Replication Controller, Deployment oder Replikat Set basierend auf der beobachteten CPU-Auslastung. |

