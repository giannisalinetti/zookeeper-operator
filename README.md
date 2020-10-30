# ZooKeeper Operator

## Overview
The ZooKeeper Operator is an Ansible Operator that manages the creation of a 
stateful ZooKeeper cluster in OpenShift.

The operator provides a Customer Resource Definition and the logic to create
the statefulset that manages the ZooKeeper cluster, client service,
headless services for server and leader election and a PodDisruptionBudget 
object to guarantee that cluster quorum will be preserved during updates and
roullouts.


## The ZooKeeper CRD

## Operator Installation
First install the CRD:
```
$ make install
```

Build and push the zookeeper-operator image:
```
$ IMG=<some-registry>/<project-name>:<tag> make docker-build docker-push
```

Deploy the zookeeper-operator in your cluster:
```
$ IMG=<some-registry>/<project-name>:<tag> make deploy
```

## CR Installation
Install the ZooKeeper custom resource using the config sample or generating 
a new CR.

The following example shows the usage of the config sample:
```
apiVersion: zookeper.example.com/v1
kind: ZooKeeper
metadata:
  name: zookeeper-example
spec:
  replicas: 3
  image_name: k8s.gcr.io/kubernetes-zookeeper
  image_tag: 1.0-3.4.10
```

Install it with the kubectl CLI:
```
$ kubectl apply -f config/samples/zookeper_v1_zookeeper.yaml
```

## CR Removal
Uninstall the ZooKeeper custom resource
```
$ kubectl delete -f config/samples/zookeper_v1_zookeeper.yaml
```

## Operator Removal
Using the Makefile the operator removal is very easy:
```
$ make undeploy
```

Remove the CRD:
```
$ kubectl delete crd/zookeepers.zookeeper.example.com
```

## Contributing
Contributions to this project are welcome.

## Maintainers
- Gianni Salinetti  
  Cloud Solution Architect  
  <gsalinet@redhat.com>


