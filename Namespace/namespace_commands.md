### [Create]
Create Namespace from command line.
```
kubectl create namespace <insert-namespace-name-here>
```
Create namespace from yaml fil.
```
kubectl create -f ./my-namespace.yaml  (Imperative Command)
```
OR
```
kubectl apply -f ./my-namespace.yaml
```
### [Get]
Get all Namespaces
```
kubectl get namespaces
```
Get spacific Namespace
```
kubectl get namespaces <name>
```
OR
```
kubectl describe namespaces <name>
```
### [Delete]
```
kubectl delete namespaces <namespace-name>
```
_Warning: This deletes everything under the namespace!_
