# Session 3: Kubernetes Basics für eure App

## 

This tutorial walks you through how to scaffold a web application, run it locally in a container, and then deploy it to a Kubernetes cluster created with . Additionally, you will learn how to bind a custom domain, monitor the health of the environment, and scale the application. {:shortdesc}

Containers are a standard way to package apps and all their dependencies so that you can seamlessly move the apps between environments. Unlike virtual machines, containers do not bundle the operating system. Only the app code, run time, system tools, libraries, and settings are packaged inside containers. Containers are more lightweight, portable, and efficient than virtual machines.

For developers looking to kickstart their projects, the  CLI enables rapid application development and deployment by generating template applications that you can run immediately or customize as the starter for your own solutions. In addition to generating starter application code, Docker container image and CloudFoundry assets, the code generators used by the dev CLI and web console generate files to aid deployment into [Kubernetes](https://kubernetes.io/) environments. The templates generate [Helm](https://github.com/kubernetes/helm) charts that describe the application’s initial Kubernetes deployment configuration, and are easily extended to create multi-image or complex deployments as needed.

### Objectives

{: \#objectives}

* Scaffold a starter application.
* Deploy the application to the Kubernetes cluster.
* Bind a custom domain.
* Monitor the logs and health of the cluster.
* Scale Kubernetes pods.

 !\[Architecture\]\(images/solution2/Architecture.png\)

1. A developer generates a starter application with .
2. Building the application produces a Docker container image.
3. The image is pushed to a namespace in .
4. The application is deployed to a Kubernetes cluster.
5. Users access the application.

