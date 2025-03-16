# prometheus-grafana-installation-on-k8s-killerkoda
## steps to install prometheus and grafana on a kubernetes cluster using helm

```
apt update -y
apt install siege
snap install helm --classic
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana
helm list
kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-ext
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
k run nginx --image=nginx
kubectl expose pod nginx --type=NodePort --port=80
k get svc
```
siege -c 200 -t 10S http://www.google.com     =>or we can use M for minutes

and grafana username = admin

use this in url for source as prometheus always =>  http://prometheus-server-ext.default.svc.cluster.local

15661 =>Dashboard id for grafana

