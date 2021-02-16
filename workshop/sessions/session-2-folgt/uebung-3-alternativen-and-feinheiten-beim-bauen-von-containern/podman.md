# optional: podman

Docker ist nicht die einzige Technologie um Container zu erzeugen. Aus diesem Grund wurde der OCI Standard ins Leben gerufen.

{% embed url="https://opencontainers.org" %}

Beispielsweise wird seit Kubernetes Version 1.18 [cri-o](https://cri-o.io) als Container Runtime benutzt.

Eine weitere Technologie ist Podman. Podman basiert auf OCI compatiblen Runtimes.

{% embed url="https://podman.io" %}

Podman ist aktuell nur für Linux verfügbar. Deshalb könnte man es über ein Container Image aufrufen.

{% embed url="https://catalog.redhat.com/software/containers/rhel8/podman/5dc383a0dd19c71643a22a37" caption="Podman Image" %}

