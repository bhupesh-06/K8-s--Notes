### [Create]
Create a Pod based on the YAML configuration file.
```
kubectl apply -f <deployment.yaml>
```
### [Get]
Get all deployments from specific namespace.
```
kubectl get deployments -n <namespace>
```
View detailed info of deployment.
```
kubectl describe deployments <deployment-name>
```
To see the ReplicaSet (rs) created by the Deployment.
```
kubectl get rs
```
To see the rollout status
```
kubectl rollout status deployment/<deployment-name>
```
### [set/edit]
To update the image of deployment
```
kubectl set image deployment/nginx-deployment <current_image=new_image>
```
Edit the deployment
```
kubectl edit deployment/<deployment-name>
```
