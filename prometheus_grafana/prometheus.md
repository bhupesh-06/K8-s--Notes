## Prometheus & Grafana Installation on Kubernetes Cluster

### Prequisites:
#### a. AWS CLI
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
#### b. eksctl
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```
#### c. kubectl
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl 
sudo mv ./kubectl /usr/local/bin

#### d. Helm Chart
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
#### e. Create Kubernetes Cluster in AWS using eksctl
```
eksctl create cluster --name pro-graf-cluster-1 --version 1.22 --region eu-central-1 --nodegroup-name worker-nodes 
--node-type t2.large --nodes 2 --nodes-min 2 --nodes-max 3
```
#### f. Kubernetes Metrics Server
```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```
### Install Prometheus
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts 
helm repo update 
```
Create a namespace for prometheus.
```
kubectl create namespace prometheus
```
Install prometheus with helm
```
helm install prometheus prometheus-community/prometheus \
    --namespace prometheus \
    --set alertmanager.persistentVolume.storageClass="gp2" \
    --set server.persistentVolume.storageClass="gp2" 
```
Set port for accessing prometheus
```
kubectl port-forward deployment/prometheus-server 9090:9090 -n prometheus
```
