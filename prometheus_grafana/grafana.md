### Install Grafana ###
Add a grafana repo to get helm charts.
```
helm repo add grafana https://grafana.github.io/helm-charts 
helm repo update
```
Create a data source manifest file for prometheus data sources.
```
vim prometheus-datasource.yaml
```
Add the following to the file -
```
datasources:
  datasources.yaml:
    apiVersion: 1
    datasources:
    - name: Prometheus
      type: prometheus
      url: http://prometheus-server.prometheus.svc.cluster.local
      access: proxy
      isDefault: true
```
Create namespace for grafana.
```
kubectl create namespace grafana
```
Install Grafana with helm and set up.
```
helm install grafana grafana/grafana \
    --namespace grafana \
    --set persistence.storageClassName="gp2" \
    --set persistence.enabled=true \
    --set adminPassword='EKS!sAWSome' \
    --values prometheus-datasource.yaml \
    --set service.type=LoadBalancer 
```
Check all the configurations made with following commands -
```
kubectl get all -n grafana
kubectl get service -n grafana 
```
Now, copy the Public AWS IP address and open it in the browser to get grafana dashboard.
