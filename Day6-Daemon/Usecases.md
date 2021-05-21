##### DaemonSet
* when we want some or all k8s node to run the copy a pod. (use nodeSelector to run on specific nodes)
* If we want to run log collection daemon on every node.
* For deploying some background tasks that do not need use intervention.

##### Stateful State
* When working with distributed database that needs persistant volume. Like Cassandra.
  when we have to work with persistant data storage. (data transfer between multiple sessions)
* If we want to use Stateful applications which need scaling and data consistency.
* when we need multiple replica of stateful application. (e.g say mongodb...establish master slave prototype)
* when we want to have the consistent data across all the replicas.
* Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and
 uniqueness of these Pods.
* These pods are created from the same spec, but are not interchangeable: each has a persistent 
  identifier that it maintains across any rescheduling.
* StatefulSet's .spec.updateStrategy field allows you to configure and disable automated rolling 
  updates for containers, labels, resource request/limits, and annotations for the Pods in a StatefulSet.
* clustering --> read write from one pod and rest pods can read only.
* dns same all across cluster.
* read write from particular pod.

##### Headless
When using StatefulSets, Headless service is mandatory in order to contact with any pods.
To avoid requests being load-balanced behind one single ip address, we can explicitly specifying “None”
 for the cluster IP when a single ip address is not desired. Kubernetes won’t allocate any IP address to 
 the service. This type of service is termed as headless service.
 
* # my-svc.my-namespace.svc.cluster-domain.example

##### Deployment
* used for Stateless application and single replica of stateful application.
* mathches current state and desired state.
* Use for stateless but can be made stateful by attatching a persistent volume but in that all pods will be accessing
  same volume and that would lead to data inconsistency. (uses PV)
* When we want fixed number of replicas all the time.