### Install Prometheus

 Check the latest downloads on  https://prometheus.io/download/


**Download prometheus**

`curl -LO url -LO https://github.com/prometheus/prometheus/releases/download/v2.35.0/prometheus-2.35.0.linux-amd64.tar.gz`

**Create prometheus user** 

`sudo useradd --no-create-home --shell /bin/false prometheus`


**Run commands**
```
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus
mv prometheus-2.22.0.linux-amd64 prometheus-files

sudo cp prometheus-files/prometheus /usr/local/bin/
sudo cp prometheus-files/promtool /usr/local/bin/
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool


sudo cp -r prometheus-files/consoles /etc/prometheus
sudo cp -r prometheus-files/console_libraries /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries

cp prometheus.yml /etc/prometheus/prometheus.yml
sudo chown prometheus:prometheus /etc/prometheus/prometheus.yml

cp prometheus.service /etc/systemd/system/prometheus.service



sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

### Install node_exporter

**Download node_exporter**
curl -LO https://github.com/prometheus/node_exporter/releases/download/v0.18.1/node_exporter-0.18.1.linux-amd64.tar.gz
Step 2: Unpack the tarball

tar -xvf node_exporter-0.18.1.linux-amd64.tar.gz

Move the node export binary to /usr/local/bin

sudo mv node_exporter-0.18.1.linux-amd64/node_exporter /usr/local/bin/



**Create a node_exporter user to run the node exporter service.**

sudo useradd -rs /bin/false node_exporter


sudo vi /etc/systemd/system/node_exporter.service


```
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```
**Start the node_exporter service**


```
sudo systemctl daemon-reload
restorecon -rv /usr/local/bin/node_exporter
sudo systemctl start node_exporter
sudo systemctl status node_exporter
sudo systemctl enable node_exporter
```


### Install Grafana


```bash
wget https://dl.grafana.com/enterprise/release/grafana-enterprise-8.5.0-1.x86_64.rpm
sudo yum install grafana-enterprise-8.5.0-1.x86_64.rpm
```
