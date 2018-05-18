[![Node.js, Docker, and Kubernetes](docs/images/container-banner.jpg)](https://nodesource.com/)

## Overview

This repository is for deploying a sample [Node.js](https://nodesource.com/products/nsolid) application with [Kubernetes](http://kubernetes.io/) and [GKE](https://cloud.google.com/kubernetes-engine/).

![Kubernetes Relationships](docs/images/kubernetes-scopes.png)

### Table of Contents
- [Installing Kubernetes](#a1)

<a name="a1"/>

## Installing kubernetes

* [kubernetes on aws](http://kubernetes.io/docs/getting-started-guides/aws/) - Amazon Web Services
* [kubernetes on ACS](http://kubernetes.io/docs/getting-started-guides/azure/) - Microsoft Azure Container Service


## Quickstart

Notes:
1. Make sure your `kubectl` is pointing to your active cluster.

It can take a little while for Kubernetes to download the N|Solid Docker images.  You can verify
that they are active by running:

```
kubectl --namespace=nodespace get pods
```


<a name="a5"/>

## Deploy Sample App with N|Solid

### Quick Start

```bash
cd sample-app
docker build -t sample-app:v1 .
kubectl create -f sample-app.service.yml
kubectl create -f sample-app.deployment.yml
```

**NOTE:** the container image in `sample-app.deployment.yml` must be set to match your docker image name. E.g. if you are using `minikube` and ran `eval $(minikube docker-env)`, set the image to:

```bash
    spec:
      containers:
        - name: sample-app
          image: sample-app:v1
```

If you are working in a cloud environment, you will need to push the sample-app to a public Docker registry
like [Docker Hub](https://hub.docker.com/), [Quay.io](https://quay.io), the [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/), or the [IBM Bluemix Container Registry](https://console.bluemix.net/docs/services/Registry/registry_images_.html#registry_images_), and update the sample-app Deployment file.


#### Accessing your App

```bash
kubectl get svc {service-name}
```

The `EXTERNAL-IP` will access the application.  
Open `EXTERNAL-IP`.  If using Bluemix _Lite_ cluster, get EXTERNAL-IP [this way](./docs/misc/bluemix-external-ip.md).


<a name="a21"/>

### Accessing Node.js Kubernetes objects

Make sure you use the `--namespace=nodespace` flag on all `kubectl` commands.

<a name="a22"/>
