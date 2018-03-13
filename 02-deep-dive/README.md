# `time-printer`

`time-printer` is a simple application that has two goals - 
1. It shows a pod with more than one container in it
2. it illustrates how to use a shared volumes between containers

To run `time-printer` in our cluster - 

```bash
$ kubectl create -f timeprinter.yaml
```

This loads te yaml manifest file to the APi server which validates it, stores it in `etcd` and starts the process of running the pod in the clsuter.

The get the state of the pod, we can again run

```bash
$ kubectl get pods
```

To see the logs of the pod, run 

```bash
$ kubectl logs <pod-name> 
```

and use the `-c` flag to get the logs from a specific container in the pod