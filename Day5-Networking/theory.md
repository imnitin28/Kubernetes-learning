# Service
* What?
It is an abstract way to expose an application running on a set of Pods as network service.
K8s gives Pods their own IP address and a DNS name for a set of Pods and can load balance across them.

* Why?
K8s pods are nonpermanent i.e mortal.
Which means if we are using Deployment to run app, it can create and destroy Pods dynamically.

Each Pods gets it's own IP address. However this IP can change when Pod dies and new Pod is created by K8s.
This leads to a problem. 
Like suppose if a POD provides functionality to other POD inside our cluster. And a moment later a POD dies, then how the other one will keep track of it ?

* Types
 * * Cluster IP
 use case : Pod1 : frontend | Pod2 : backend | both in same cluster | Cluster Ip to make communication b/w them.
 * * NodePort
 External access like : 
   30000 to 32767
 * * LoadBalancer
 External access via cloud load-balancer

* ways to create services
* * Imperatively
kubectl expose pod hello-pod --name=hello-svc --target-port=8080 --type=NodePort


 -> --name=hello-svc  | registered in DNS

* * Declaratively

### Service Discovery
Troubleshooting and defining and deploying services.

kubectl exec -it <Podname> nslookup <ip address>
