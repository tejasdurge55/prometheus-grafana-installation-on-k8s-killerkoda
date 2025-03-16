vm 1 install webapp and node-exporter:
```
apt install nginx
echo "Hi this is tejas nginx website on aws" > /var/www/html/index.nginx-debian.html
cat /var/www/html/index.nginx-debian.html
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.0/node_exporter-1.9.0.linux-amd64.tar.gz
tar -xvf node_exporter-1.9.0.linux-amd64.tar.gz
rm -rf node_exporter-1.9.0.linux-amd64.tar.gz
mv node_exporter-1.9.0.linux-amd64/ node_exporteporter
cd node_exporteporter/
./node_exporter &
```

vm 2 install prometheus  and grafana:
```
wget https://github.com/prometheus/prometheus/releases/download/v3.2.1/prometheus-3.2.1.linux-amd64.tar.gz
tar -xvf prometheus-3.2.1.linux-amd64.tar.gz
rm -rf prometheus-3.2.1.linux-amd64.tar.gz
mv prometheus-3.2.1.linux-amd64/ prometheus
cd prometheus/
vi prometheus.yml
```

add =>
```
  - job_name: node_exporter
    static_configs:
      - targets: ["54.196.193.188:9100"]
```
```
./prometheus &
cat /etc/os-release
sudo yum install -y https://dl.grafana.com/enterprise/release/grafana-enterprise-11.5.2-1.x86_64.rpm
sudo /bin/systemctl daemon-reload
sudo /bin/systemctl enable grafana-server.service
sudo /bin/systemctl start grafana-server.service
```

and grafana username = admin

password = admin

then skip change password

use this in url for source as prometheus always =>  https://9090-port-e66qtpe27vvmu5yd.labs.kodekloud.com/targets

1860 =>Dashboard id for grafana for linux single node monitoring
