# Problem 

## Step 1
Deploy a 3-Node K8S cluster using Minikube.

## Step 2
Write a Pod manifest for each microservices you developed in Project03.

## Step 3
Write a Service manifest for each of the mentioned microservices.

## Step 4
Expose your services on a port of your local machine.

-----
# Solution

## Step 1
1- Install minikube 
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

2- Start a 3-node cluster using minikube
```
minikube start --nodes 3
```
or manually add to your control plane and label as worker (recommended)
```
minikube add node
```
3- Label added nodes as workers
```
kubectl label node <node_name> node-role.kubernetes.io/worker=worker   # or kubectl label nodes <node_name> role=worker
```

## Step 2
4- Write Pod manifests for each service.
e.g. a Pod Template: