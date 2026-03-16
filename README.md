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

