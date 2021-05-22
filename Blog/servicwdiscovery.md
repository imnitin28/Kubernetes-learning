# Service Discovery in Kubernetes
Namespaces are one of the most important part of whole DevOps ecosystem. 
They play a very important role behind various container implementations in the way that they provide an isolation for independent proceses from global system's interference directly.

# Namespace Definition :
A namespace wraps a global system resource in an abstraction that makes it appear to the processes within the namespace that they have their own isolated instance of the global resource. Changes to the global resource are visible to other processes that are members of the namespace, but are invisible to other processes.
       
* Let's go more Simpler

It seems quite obvious and simple that how resources within same namespace can communicate with each other.
Consider it in this way, Inside your house you can communicate with your mother easily i.e you don't need house address for this. But what if you want to communicate with your friend residing at some xyz building. You will have to follow a fixed route to go there.

Service discovery is all about finding that fixed route in the world of kubernetes. Service discovery does that with help of dns. 

# DNS
Domain Name Server aka DNS is basically a standard protocol that helps internet users to discover websites using human readable address i.e domain name.
Users interact with the web browser using the domain name and web browser communicate to server using the IP address. And DNS acts as an support which translates the domain name to IP address for overall workflow.
#####

#### Understanding dns name format for your pod.
IP.podname.namespace.service.cluster.local

# Let's see some use cases for Service Discovery

## Scenario-0

check ENV variable to discover running services.
run deployment
run service
get pods
exec to pod
printenv
---------------------------------------------------
scale down deployment to 0
scale up deployment to 2
get pods
exec to pod
printenv
 ---- observe the ENV variable.

## Scenario-1 

Namespace | N1 | N2
POD       | POD1 | discover that pod here.

kubectl run curl --image=radial/busyboxplus:curl -i --tty -n discovery
nslookup my-cluster-service 


## Scenario-2

Namespace | N1 | N2 |
POD       |pod1|pod2|
ping from pod1 to pod2

describe pod1(default namespace) --> copy IP address
kubectl run curl --image=radial/busyboxplus:curl -i --tty -n discovery
nslookup IP-Pod1 
IP.podname.namespace.service.cluster.local
172-17-0-4.welcome-pod.default.svc.cluster.local
