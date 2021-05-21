In K8s pods are the smallest deployable unit. But pods are mortal which means it dies and K8s creates new Pod as per the desired state. With this the IP of pod also keeps on changing, due to the application will go inacessible with continuing changing pods.
To overcome this, we have service, which basically acts as an abstraction b/w external world and pods.
Service is logical set of pods with help of labels and selectors.

* Service discovery is the actual process of figuring out how to connect to a service.

* * create two namespaces namely development and testing
* * take an image and apply them over both namespaces
* * to be sure that tehy are running describe pods with --all-namespaces
* * 

$ kubectl apply -f jumpod.yml
pod/jumpod created

$ kubectl exec -it jumpod ping 10.244.0.149
PING 10.244.0.149 (10.244.0.149): 56 data bytes

kubectl exec -it jumpod nslookup 10.244.0.149


$ kubectl apply -f app-service-develop.yml
$ kubectl apply -f app-service-production.yml

kubectl get services --all-namespaces

$ kubectl exec -it jumpod nslookup 10.245.150.103

$ nslookup 10.245.150.103

$ kubectl exec -it jumpod wget -- -O - http://hello.develop
Connecting to hello.develop (10.245.150.103:80)
    
$ kubectl exec -it hello-f878d7d65-2qctb env --namespace=develop



$ kubectl scale deployment hello --replicas=0 --namespace=develop
$ kubectl scale deployment hello --replicas=2 --namespace=develop


$ kubectl get pods --namespace=kube-system -l k8s-app=kube-dns



$ kubectl get services --namespace=kube-system -l k8s-app=kube-dns

$ cat /etc/resolv.conf 

