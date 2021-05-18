In K8s pods are the smallest deployable unit. But pods are mortal which means it dies and K8s creates new Pod as per the desired state. With this the IP of pod also keeps on changing, due to the application will go inacessible with continuing changing pods.
To overcome this, we have service, which basically acts as an abstraction b/w external world and pods.
Service is logical set of pods with help of labels and selectors.

* Service discovery is the actual process of figuring out how to connect to a service.

* * create two namespaces namely development and testing
* * take an image and apply them over both namespaces
* * to be sure that tehy are running describe pods with --all-namespaces
* * 
