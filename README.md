Headless service:-(Video:- https://www.youtube.com/watch?v=NOjCunqu3VA&t=984s)

1. why do we need headless service when we already have clusterIP?
If pod 4 want to access other pods(pod0,1,2) using clusterIP service it is accessible using clsuterIP name/IP address but the issue here is clusterIP service loda balances the requests to all the pods(0,1,2) based on Round Robin.
In case of Stateful applications, requests should not be balanced between all the pods(2,3,4) because the pod2 will always act as primary pod and all the write requests should go to pod0, pod1,2 are replicas that supports with read requests. so we are using Headless service.
2. Headless service creates DNS names to the pods, so pod4 can directly communicate with the pod(0,1,2) using DNS names.
3. My doubt is y do we need DNS names for ss pods because pods already have static names irrespective of their IPaddress?
K8s DNS does not automatically expose pod names. There is no DNS entry for pod-0 whhich means if u try to "ping pod-0" it will fail.
with headless service it will create DNS entries. Now "ping <podname>.<servicename>" pod is accessible

Stateful sets:-(Video:- https://www.youtube.com/watch?v=qLL5wf0ShZY&t=570s)

1. SS are for staeful applications that required databases.
2. when we create deployments the pods will have randomn names with deployment name like dep1-1234-id1, dep1-1234-id2.
3. when we create SS, the pos will be created in ordinal index like app1-0, app-1. these names are very important because each pod has a different role, pod-0 always write, other pods always read. To avoid data corruption.
4. in SS, the pods will created sequentially in the same order like app-0, app-1 and deleted in the same order.
5. For SS create a headless service, the service with clusterIP as none is headless service it has no internal n externalip.
6. For deployments service is optional but for SS headless service is mandatory.
7. 🔴 Why NOT parallel like Deployment?
Because in stateful apps, order matters.
🔹 1. 🧩 Dependency between Pods
Example (database):
db-0 = Primary
db-1 = Replica (needs primary to exist)
👉 If created in parallel:
db-1 starts
Tries to connect to db-0
db-0 not ready yet ❌
💥 Replication fails

NOTE:-
1. When should we go for Stateful sets:- If the database itself runs inside the pod, then we should go for ss.
3. Using deployments with shared disk is not suggested for database related pods because data corruption will happen when multiple pods write to same storage.
4. When you are using managed database services like Amazon RDS, Azure SQL Databases, then you dont have to use stateful sets because the database is not running inside the kubernetes and filelocking is not supported
5. Only your app backend apis,microservices run in k8s, these just connect db via connection string and dont store data locally.


Demo:-

1. create a k8s cluster, and in the worker node create directories for each pod so that their data can be mounted.
2. Create headless service and then crr

