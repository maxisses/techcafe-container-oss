# Glossar

## Grundlagen & Container

<table>
  <thead>
    <tr>
      <th style="text-align:left">Begriff</th>
      <th style="text-align:left">Erkl&#xE4;rung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Container Image</td>
      <td style="text-align:left">Layered file system where each layer references the layer below</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p></p>
        <p>Dockerfile</p>
      </td>
      <td style="text-align:left">build script f&#xFC;r Containerimage</td>
    </tr>
    <tr>
      <td style="text-align:left">Container Prozess</td>
      <td style="text-align:left">runtime instance of an image plus a read/write layer</td>
    </tr>
    <tr>
      <td style="text-align:left">OCI</td>
      <td style="text-align:left">Open Container Initiative - Standard wie Container Images gebaut werden</td>
    </tr>
    <tr>
      <td style="text-align:left">CRI</td>
      <td style="text-align:left">Container Runtime Interface - Standard f&#xFC;r Container Engines um von
        Kubernetes genutzt werden zu k&#xF6;nnen</td>
    </tr>
    <tr>
      <td style="text-align:left">Cloud Foundry</td>
      <td style="text-align:left">Platform-as-a-Service Angebot mit starkem Entwicklerfokus um deployments
        so einfach wie m&#xF6;glich zu machen. Nutzt f&#xFC;r den Anwender nicht
        sichtbar ebenfalls container - man deployed aber keine docker images selber.</td>
    </tr>
    <tr>
      <td style="text-align:left">Delivery Pipeline</td>
      <td style="text-align:left">&#xDC;bernimmt automatisiertes Deployment in mehreren Stages, mit Test,
        Integration und in mehrere Umgebungen</td>
    </tr>
    <tr>
      <td style="text-align:left">Toolchain</td>
      <td style="text-align:left">Eine DevOps Toolchain geht &#xFC;ber CI/CD und Delivery Pipelines hinaus
        und integriert z.B. ein git aber auch Slack/Teams, Monitoringtools, externe
        Testsuiten, Definition von Quality Gates etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">git</td>
      <td style="text-align:left">Source Control Management</td>
    </tr>
    <tr>
      <td style="text-align:left">gitlab</td>
      <td style="text-align:left">Ein SCM Produkt neben Bitbucket und github.</td>
    </tr>
    <tr>
      <td style="text-align:left">container registry (image registry)</td>
      <td style="text-align:left">hier werden gebaute container images abgelegt, in versionskontrolle &amp;
        entsprechend getagged</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

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



