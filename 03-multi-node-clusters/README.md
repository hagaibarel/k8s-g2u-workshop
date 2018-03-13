# Pod assignment

The schedular does a decent job when it comes to schedule pods to nodes. There are however use cases where we want to schedule pods to specific nodes or reserve nodes for dedicated workloads.

## `nodeSelector`

Using labels, `nodeSelector` allows to target a pod on to a specific node. To do so, we first have to label a node - 

```bash
$ kubectl label node kube-worker1 disktype=ssd
```

We can than run our `deployment` with a `nodeSelector` field - 

```bash
$ kubectl create -f node-selector.yaml
```

Even of we scale our application to multiple replicas (using ```kubectl scale```) all of our replicas will land on `kube-worker1` as only that node satisfies the constraint defined in the node selector field.

## `taints` and `tolerations`

A `nodeSelector` is a property of pods that attracts them  to certain nodes. Taints on the other hand allow for nodes to repel pods that don't tolerate the taint. 

`nodeSelector`, `taints` and `tolerations` work together when we would like to reserve a node for dedicated workloads, for example a node with a GPU.

We can use the following steps:
1. Taint the node, which will prevent pods from landing on it
2. Add a label to the node
3. Define a `nodeSelector` and `toleration` in the pod manifest

We'll use the node we labeled before (`kube-worker1`) and add the following taint - 

```bash 
$ kubectl taint node kube-worker1 dedicated=gpu:NoSchedule
```

And create a deployment -
```bash
$ kubectl create -f taint.yaml
```

# Configuration management

kubernetes provides us with 3 built in ways to manage a configuration for a pod - 
1. Environment variables
2. ConfigMaps
3. Secrets

All of them can be found under the config-mgmt folder, and loaded to the cluster at once - 

```bash
$ kubectl create -f config-mgmt/ 
```