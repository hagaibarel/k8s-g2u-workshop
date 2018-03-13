# k8s-g2u-workshop

In this repo you can find example files used in the kubernetes from the ground up workshop.

These files are meant to accompany the workshop and might not make much sense with out the context.

## Disclaimer

The files in this repo are example files and are not supposed to represent real world use-cases or recommanded ways to define kubernetes application. They are for educational purposes only, not production usage.

## Pre-requisites

you should have the following installed on your machine and available in your $PATH:
1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
2. [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/)
3. [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
4. [Vagrant](https://www.vagrantup.com/downloads.html)
5. [Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md)

## Workshop structure

### Session 1
We begin the workshop with a general introduction to kubernetes. We'll discuss it's origin and the challenges it aims to solves. By the end of the first session we'll run `hello kubernetes`, which you can find instructions for in the [01 hello k8s](./01-hello-k8s) folder.

### Session 2
Next, we'll take a closer look on the control plane components - the API server, schedular, controller manger and node components such as the kubelet. We will also move to declarative configuration instead of imperative and see how we can manage resources using files. A simple toy can be found in [02-deep-dive](./02-deep-dive) folder which illustrates how such a manifest file looks like.

### Session 3
In the third session will talk about multi node clusters, moving away from minikube. We'll look at different ways to affect scheduling considerations in pod assignment such as `nodeSelector`, taints and tolerations. We'll also talk about configuration management and introduce two new kubernetes resources - the `ConfigMap` and `Secret`. Lastly, we'll talk about managing a pod's compute resources and setting requests and limits to it's CPU and memory parameters. All the relevant files for the third session can be found under [03-multi-node-clusters](./03-multi-node-clusters) folder.

in order to use all of the features we'll discuss in session 3, we'll need a cluster with more than one node so `minikube` won't do. While there are numerous ways to get a cluster running (e.g as a manged service), you can use the [k8s-vagrant project](https://github.com/HagaiBarel/k8s-vagrant) which bootstraps a local kubernetes cluster using `vagrant` to provision the VMs and `kubeadm` for the cluster components.

### Session 4
In the final session we'll talk about helm, the kubernetes package manager. We'll look at what charts are and what possibilities we have when authoring one. We'll finish off with discussing chart functions and repositories

## Contributions

While I took special care to prepare things as best as possible, mistakes might have fallen in the example files found here. Feel free to submit an issue if you'd like or a PR to fix something.