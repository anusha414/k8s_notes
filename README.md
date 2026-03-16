Stateful sets:-

1. SS are for staeful applications that required databases.
2. when we create deployments the pods will have randomn names with deployment name like dep1-1234-id1, dep1-1234-id2.
3. when we create SS, the pos will be created in ordinal index like app1-0, app-1.
4. in SS, the pods will created sequentially in the same order like app0-app-1 and deleted in the same order.
5. For SS create a headless service, the service with clusterIP as none is headless service it has no internal n externalip.
6. For deployments service is optional but for SS headless service is mandatory.

Demo:-

1. create a k8s cluster, and in the worker node create directories for each pod so that their data can be mounted.
2. Create headless service and then crr


Daemon Sets:-

1. when you create a deployment with 3 replicas on a k8s cluster of 4 nodes, it might randomnly assign the 3 pods on the 4 nodes based of resource availability and makes sure that 3 repliacs are always running.
2. In case of deamon set if there are 4 nodes it will create 4 pods on each of the k8s nodes.
3. If a new node gets added to the cluster then it will add a new pod to that node.
4. Lets assume if there is a pod with same labels as deployment selectors, deployment will not delete the pod or consider it as part of deployment replica because replicaset adds a new label pod-template-hash to the deployment pods.
5. In case of DaemonSet if there is any Pod that is running with same label then it will delete the pod.
6. DaemonSet is manily used for monitoring(resource information), logging and kubecproxy(default daemon set in kube-system namespace).

eg:-
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: dep1
spec:
  selector:
    matchLabels:
      type: frontend
  template:
    metadata:
      name: pod2
      labels:
        type: frontend
    spec:
      containers:
      - name: con2
        image: nginx
