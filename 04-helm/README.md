# Helm

To get helm running, we first must start the server side component `tiller`. 

Note - If RBAC is enabled in the cluster, you must first configure a service account for tiller before starting the server.

This can by done running the following commands - 

```bash
$ kubectl -n kube-system create sa tiller

$ kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller

$ helm init --service-account tiller
```

## Charts

To get started with a helm chart run -

```bash
$ helm create my-chart
```

This will create a starter chart with basic resource manifests.

to debug a chart, we can run - 

```bash
$ helm lint <chart>
```

helm will lint the chart and raise errors if some if the fields are missing or other issues exist. To see the computed values, we can run 

```bash
$ helm install --dry-run --debug <chart>
```

This will output to the console the compiled templates with the computed values.

## Releases

A release is a running instance of a chart. To create a release - 
```bash
$ helm install --name <release-name> <chart>
```

Once a release has been installed in the cluster, we can info on it. To see the revision history of a release - 

```bash
$ helm history <release>
```

To roll back to a previous revision of a release - 

```bash
$ helm rollback <release> <revision>
```