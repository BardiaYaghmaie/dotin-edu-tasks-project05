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
4- Write Pod manifests for each microservice.
e.g. a Pod Template:
```
apiVersion: v1
kind: Pod
metadata:
  name: shop-pod
  labels:
    name: shop-pod
    project: pr05
spec:
  containers:
  - name: shop
    image: bardiayaghmaie/pr04-shop:1.0
    ports:
    - containerPort: 80
```

5- Deploy Pod
```
kubectl apply -f shop/shop-pod.yml
```

## Step 3
6- Write Service manifests for each Pod
e.g. a Service Template:
```
apiVersion: v1
kind: Service
metadata:
  name: shop-service
spec:
  type: NodePort
  selector:
    name: shop-pod
    project: pr05
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30003
```
7- Deploy Service
```
kubectl apply -f shop/shop-service.yml
```
## Step 4
8- Access each service via
```
minikube service shop-service
```

## Step 5 (additional step, actually related to project06)
9- Change service types from NodePort to ClusterIP
```
...
~~kind: NodePort~~ kind: ClusterIP
```

10- Create an Ingress manifest in nginx directory
...