Container -> Pod

Ideally 1 container per pod but in some cases, you can run multiple containers in a pod.

```
kubectl run nginx --image nginx - created pod automatcaaly and runs nginx container
```

How to make this service available?


Controller
Have many controller

1. ReplicationController
    HighAvil
    brings up pods when they die
    load balancing
ReplicationController spans across nodes. Because you can have many pods which RC can manage and ensure are running


Replica Set is new way of doing it.

```
apiVersion: apps/v1
kind: RelicaSet
metadata
    name: mappp
    type: front-end
```

# define pod template which will be used to manage the replica set. this template is used by the contrller
# is same as regular k8s yaml config except apiVersion and kind
spec:
    - template:
        metadata
    relicas:
    selector: // what pods fall under it? because it can also manage pods not created by the Replica Set. If selector
    is defined. then matchLabels: must also be defined

```

Labels
RS monitor the pod.
What pods to monitor?
it used Labels 

# K8s Services
Enable communication between aplications

e.g. 
```
USers <-> Frontend <-> backend <-> DataSource 
```

### Problem statement: 
Pod is deployued as web app
how to acces the web app?

1. node has an IP same 
2. Internal pod network is diffrent 

How can I access the pod from my laptop?

This is where k8s service come in.

It's an object that that listenes on specific port 
and forwards the traffic tro specifiied port to the service in the node.

### Types of services

- NodePort
- Cluster
- LoadBalancer

 Exposes the service on each Node's IP at a static port (the NodePort). A ClusterIP service, to which the NodePort service will route, is automatically created. You'll be able to contact the NodePort service, from outside the cluster, by requesting <NodeIP>:<NodePort>.

NodePort range: 30000 - 32767

service.yaml
```
apiVersion: v1
kind: service
metadata:
    name: name-of-service

spec:
    type: NodePort  
    ports:
        - targetPort: 80
        port: 80
        nodePort: 30008 <- allocated automatuicaly; if not specicied
    selector:
        app: myapp
        type: front-end

```

ClusterIP: Creates an internal IP address which allows communication within the cluster.

```
apiVersion: v1
kind: service
metadata: 
    name: 
spec:
    type: ClusterIP <-- default type
    ports:
        - targetPort: 80
          port: 80
    selector:
        app: myapp
        type: back-end
```
LoadBalancer: Creates an external load balancer in the cloud provider which allows traffic to be routed into the cluster.

