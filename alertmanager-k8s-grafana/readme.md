

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
kubectl create ns monitoring
wget https://raw.githubusercontent.com/iam-veeramalla/observability-zero-to-hero/refs/heads/main/day-2/custom_kube_prometheus_stack.yml
helm install monitoring prometheus-community/kube-prometheus-stack -n monitoring -f ./custom_kube_prometheus_stack.yml
kubectl wait --for=condition=Ready pods --all -n monitoring --timeout=300s
kubectl port-forward service/prometheus-operated -n monitoring 9090:9090 --address 0.0.0.0 &
kubectl port-forward service/monitoring-grafana -n monitoring 8080:80 --address 0.0.0.0 &
kubectl port-forward service/alertmanager-operated -n monitoring 9093:9093 --address 0.0.0.0 &
k get svc -n monitoring
```

Grafana UI: user is `admin`

Grafana UI: password is `prom-operator`

Use `http://monitoring-kube-prometheus-prometheus.monitoring:9090/` as prometheus server url

clone repo and go to day 4

```
git clone https://github.com/iam-veeramalla/observability-zero-to-hero.git
cd observability-zero-to-hero/day-4
kubectl create ns dev
kubectl apply -k kubernetes-manifest/
```

convert app token to base64 and add it to email-secret.yaml
```
echo "1234 5678 9123" | base64
```

configure alertmanager by provideing your email by changing alertmanagerconfig.yml
```
kubectl apply -k alerts-alertmanager-servicemonitor-manifest/
```

To crash the application container, hit the following endpoint

<<LOAD_BALANCER_DNS_NAME>>/crash
