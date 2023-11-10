# Install Prometheus and Grafana

sudo apt-get install -y prometheus prometheus-node-exporter

# Create prometheus.yml file

# Move prometheus.yml to the correct location

sudo mv $HOME/prometheus.yml /etc/prometheus/prometheus.yml

# Update the file permissions**

sudo chmod 644 /etc/prometheus/prometheus.yml

# Ensure Prometheus starts automatically

sudo systemctl enable prometheus.service prometheus-node-exporter.service

# Restart Prometheus to activate latest settings**

sudo systemctl restart prometheus.service prometheus-node-exporter.service

# Check the status, ensure Prometheus has started without errors**

sudo systemctl status prometheus.service prometheus-node-exporter.service


# 2.Install Grafana
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" > grafana.list
sudo mv grafana.list /etc/apt/sources.list.d/grafana.list
sudo apt-get update && sudo apt-get install -y grafana

Ensure Grafana starts automatically

sudo systemctl enable grafana-server.service
sudo systemctl start grafana-server.service
sudo systemctl status grafana-server.service

# 3.Setup Grafana Dashboard
sudo ufw allow 3000/tcp
Ensure port 3000 is open, example of adding to ubuntu firewall In your browser navigate to http://<your validators ip address>:3000. The default login username and password is admin/admin

You will be asked to reset your password, please write it down or remember the password as you will need it for the next login.

You will need to create a datasource. Navigate to **Home**->**Connections->Data sources**

- Click on Add data source

- Click on Prometheus

- Set URL to "localhost:9090", then test and save the connection

- Navigate back to your home page, on the top right in the menu select Import dashboard
- 
Import the Avail Node Metrics file: [https://github.com/availproject/availproject.github.io/blob/6ff2c1862ede87225a1b6ee296ea5762f56f4042/static/grafana/Avail-Node-Metrics.json](https://github.com/ImStaked/MantraChain-Testnet/blob/main/metrics/grafana.json) Download that file to your computer.

You will have a new dashboard that opens and that you can use to monitor your node
