# Helm

To get helm running, we first must start the server side component `tiller`. 

Note - If RBAC is enabled in the cluster, you must first configure a service account for tiller before starting the server.

This can by done running the following commands - 

```bash
$ kubectl -n kube-system create sa tiller

$ kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller

$ helm init --service-account tiller
```

To get started with a helm chart run -

```bash
$ helm create my-chart
```

This will create a starter chart with basic resource manifests.