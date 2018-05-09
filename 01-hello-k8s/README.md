# `hello kubernetes`

To run our first pod, we'll first need a kubernetes cluster. We'll use `minikube`, which is essentially a single node cluster. to get `minikube` installed on your machine, follow the instructions [here](https://kubernetes.io/docs/tasks/tools/install-minikube/)

To start a `minikube` machine, run the following from a terminal - 

```bash
$ minikube start --memory 4096
```

You can find additional information in the official [docs](https://kubernetes.io/docs/getting-started-guides/minikube/)

Once `minikube` finishes the bootstrapping process, we can start interacting with the cluster (through the API server) using `kubectl`. Note that `minikube` wrote an entry the `kubeconfig` file and set the context to `minikube` itself.

Let's explore what components are in out cluster - 

```bash
$ kubectl get pods
```

You'll get nothing. Why? because we haven't deployed any resources to our cluster. However, we can list the control plane components which are found in the `kube-system` namespace - 

```bash
$ kubectl get pods --namespace kube-system
```

There, better.

Now, to run our first pod - 

```bash
$ kubectl run nginx --image nginx:alpine --port 80
```

This is very similar to a `docker run` command. We tell `kubectl` to create a `deployment` called nginx with the `nginx:alpine` image and use container port 80. While we haven't told `kubectl` to create a `deployment` explicitly, it does so by default since we haven't defined the restart policy.

To see our new pod starting, we can run -

```bash
$ kubectl get pods
```

And see it's status. From here we can use other commands to get information about the pod such as `kubectl describe` and `kubectl logs`. To scale the application we could run -

```bash
$ kubectl scale deployment nginx --replicas=3
```

And see other pods start as well.

Our pods are running but are not yet accessible from outside our cluster. To expose them, we use -

```bash 
$ kubectl expose deployment nginx --type NodePort --name nginx
```

This will create a service of type `NodePort`. to see a list of services we run `kubectl get services`. note the external port for out service (the high one, above 30000). We can than get the minikube VM ip using `minikube ip` and point our browser to `http://<minikube-ip>:<service-port>` 