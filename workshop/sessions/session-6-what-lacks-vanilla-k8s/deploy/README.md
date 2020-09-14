# Übung 1: Bauen & Deployen nach OpenShift

In dieser Übung werden wir einige der zahlreichen Möglichkeiten kennenlernen, wie man Applikation in OpenShift bauen und deployen kann. 

Die Applikation BookInfo dient uns hier als Beispiel für eine einfache Webanwendung. Sie stellt einen einfachen Buchshop dar, auf dem wir Details über das Buch, Rezensionen und Bewertungen angezeigt bekommen. Die gesamte Applikation setzt sich aus 4 Services zusammen, die wir auf unterschiedliche Art deployen werden:  

1. Rating Service - Deployment des Images per YAML Manifest über das Openshift CLI _oc_.
2. Reviews Service - Deployment des Images per YAML Manifest über das OpenShift Web Ui. 
3. Details Service - Build per Dockerfile und anschließendes Deployment des Images via Web Ui.
4. Product Page - Build per Source2Image und anschließendes Deployment des Images via Web Ui.

![Aufbau der Bookinfo Applikation](../../../.gitbook/assets/noistio.svg)

## 

