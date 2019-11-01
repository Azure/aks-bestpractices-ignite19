## AKS Cluster Upgrades Using Node Pools

Besides offering different VM SKUs running under the same AKS cluster, node pools can also help with performing Blue/Green type of cluster upgrades as most of the API calls are node pool level now, please check the [node pools docs](https://docs.microsoft.com/en-us/azure/aks/use-multiple-node-pools) to learn more. 

#### The Demo
We will perform a blue/green cluster upgrade using node pools.

```shell
#lets see what versions are available for us in AKS
$ az aks get-versions -l westeurope -o table
KubernetesVersion    Upgrades
-------------------  ----------------------------------------
1.15.4(preview)      None available
1.15.3(preview)      1.15.4(preview)
1.14.7               1.15.3(preview), 1.15.4(preview)
1.14.6               1.14.7, 1.15.3(preview), 1.15.4(preview)
1.13.11              1.14.6, 1.14.7
1.13.10              1.13.11, 1.14.6, 1.14.7
1.12.8               1.13.10, 1.13.11
1.12.7               1.12.8, 1.13.10, 1.13.11
1.11.10              1.12.7, 1.12.8
1.11.9               1.11.10, 1.12.7, 1.12.8
1.10.13              1.11.9, 1.11.10
1.10.12              1.10.13, 1.11.9, 1.11.10
```

```shell
#Lets spin up a cluster using K8s v1.13.11 with a single node pool called nodepool1311

#define the variables


