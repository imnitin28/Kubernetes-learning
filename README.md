# Kubernetes-learning

## DAY 1
Introduction
Why & What ?
Benefits of Kubernetes
Compare with other container orchestrator engine
minikube intoduction & setup

## DAY 2

## DAY 3

## How to run

### pod.yml
make sure minikube is running -> if not run "minikube start"
then run **"kubectl apply -f pod.yml"**
to check status **"kubectl get po welcom-pod"**
to get detailed info **"kubectl describe po welcome-pod"**
to delete the pod **"kubectl delete po welcome-pod"**

# initcontainer-nodeapp.yml
kubectl apply -f initcontainer-nodeapp.yml

kubectl get po foss-app-with-init

kubectl describe po foss-app-with-init

kubectl delete -f initcontainer-nodeapp.yml

## Day 4

# ReplicationController | ReplicaSet | Deployment

#### ReplicationController
 kubectl apply -f replication.yml 
 kubectl describe replicationcontrollers/nginx
 kubectl describe rc nginx
 kubectl delete replicationcontrollers/nginx

 List on which node pods are running inside cluster (Since I am using minikube, we'll find no change in node)
 kubectl get po -o wide

 To list all available nodes. (Since working on minikube only one node i.e minikube will be visible)
 kubectl get nodes


###### Scale up
* useful when traffic increases on application.

kubectl describe rc nginx
Observe the replicas

kubectl scale rc nginx --replicas=5
kubectl describe rc nginx
Observe the changes.

kubectl get rc nginx
This will show desired and current state with ready as well.

#### ReplicaSet
<!-- When to use ReplicaSet?
It is recommend to use Deployments instead of directly using ReplicaSets, unless you require custom update orchestration or don't require updates at all. -->

kubectl apply -f replicaSet-MatchExpression.yml 
kubectl get pods
kubectl get rs nginx-rs -o wide
kubectl describe rs nginx-rs

kubectl scale rc nginx-rs --replicas=6
kubectl get pods -o wide
kubectl get po -l app=nginx-app

#### Diff b/w ReplicaController and ReplicaSet
* ReplicaController
supports only Euaility based Selectors
Operators -> ( = , == , !=)
kubectl get pods -l app=nginx 

* ReplicaSet
Supports Equality based and Set based selectors.
Operators -> ( in , notin , exists)


#### Deployment
kubectl create -f deployement.yml 
kubectl apply -f deployement.yml 
kubectl describe deploy nginx-deploy
kubectl get po -l app=nginx-app

* Update version of nginx
###### Way 1
kubectl set image deploy nginx-deploy nginx-container=nginx:1.9.1

###### Way 2
kubectl edit deploy nginx-deploy

What if by mistake we did this nginx-container=nginx:1.91 insted of nginx-container=nginx:1.9.1
-- It will get stucked
-- We need to do rollback to previous stable release
kubectl set image deploy nginx-deploy nginx-container=nginx:1.91
kubectl set image deploy nginx-deploy nginx-container=nginx:1.91 --record
-- with --record K8s will record this command in resource annotation kubernetes.io/change-cause

knoldus@nitin-knoldus:~/Desktop/KubernetesResources/Kubernetes-learning/Day4-Replicas/DocExamples$ kubectl rollout status deployment/nginx-deploy
Waiting for deployment "nginx-deploy" rollout to finish: 1 out of 3 new replicas have been updated...

kubectl rollout history deployment/nginx-deploy
kubectl rollout undo deployment/nginx-deploy
kubectl rollout status deployment/nginx-deploy

* Scale up and Scale down
kubectl scale deployment nginx-deploy --replicas=5
kubectl get deploy
kubectl get po

kubectl scale deployment nginx-deploy --replicas=1
kubectl get deploy
kubectl get po -l app=nginx-app

