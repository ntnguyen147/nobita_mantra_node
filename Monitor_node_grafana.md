# Install Prometheus and Grafana

sudo apt-get install -y prometheus prometheus-node-exporter

# Create prometheus.yml file

Move prometheus.yml to the correct location**
**
sudo mv $HOME/prometheus.yml /etc/prometheus/prometheus.yml

**Update the file permissions**

sudo chmod 644 /etc/prometheus/prometheus.yml

**Ensure Prometheus starts automatically**

sudo systemctl enable prometheus.service prometheus-node-exporter.service

**Restart Prometheus to activate latest settings**

sudo systemctl restart prometheus.service prometheus-node-exporter.service

**Check the status, ensure Prometheus has started without errors**

sudo systemctl status prometheus.service prometheus-node-exporter.service


