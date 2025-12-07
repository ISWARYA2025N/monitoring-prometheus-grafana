📊 System Monitoring Using Prometheus, Node Exporter, and Grafana (Docker-Based)

This project demonstrates end-to-end system monitoring using
Prometheus, Node Exporter, and Grafana, all running with Docker on Windows/WSL2.

You will learn how to:

✔ Pull and run Prometheus
✔ Pull and run Node Exporter
✔ Pull and run Grafana
✔ Configure Prometheus to scrape Node Exporter
✔ Visualize metrics in Grafana

🚀 1. Prerequisites

Make sure you have:

Docker installed (Windows or WSL2)

📁 Project Structure
monitoring/
├── prometheus.yml
└── README.md

🛠 2. Setup Prometheus
2.1 prometheus.yml

Create a file prometheus.yml:

global:
  scrape_interval: 5s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["node-exporter:9100"]

2.2 Run Prometheus using Docker
docker pull prom/prometheus


Run Prometheus and mount your config:

docker run -d \
  -p 9090:9090 \
  -v ${PWD}/prometheus.yml:/etc/prometheus/prometheus.yml \
  --name prometheus \
  prom/prometheus


Access UI:
👉 http://localhost:9090/

🖥 3. Run Node Exporter

Node Exporter collects system metrics (CPU, RAM, Disk, etc.)

docker pull prom/node-exporter


Run it:

docker run -d \
  -p 9100:9100 \
  --name node-exporter \
  prom/node-exporter


Check metrics:
👉 http://localhost:9100/metrics

📈 4. Run Grafana for Visualization

Pull the image:

docker pull grafana/grafana


Run Grafana:

docker run -d \
  -p 3000:3000 \
  --name grafana \
  grafana/grafana


Open Grafana:
👉 http://localhost:3000/

Default login:

Username: admin

Password: admin

📡 5. Add Prometheus as a Data Source in Grafana

Go to Grafana → Settings → Data Sources

Click Add data source

Select Prometheus

Set URL:

http://node-exporter:9090


Click Save & Test

📊 6. Import Grafana Dashboard

A popular dashboard ID for Node Exporter is 1860.

Steps:

Go to Dashboards → Import

Enter 1860

Choose Prometheus as the data source

Import

Now you will see beautiful system metrics!


🧹 7. Useful Docker Commands

Stop containers:

docker stop prometheus grafana node-exporter


Start containers:

docker start prometheus grafana node-exporter


Remove containers:

docker rm -f prometheus grafana node-exporter

✅ Final Output

With this setup, you will have:

✔ Prometheus scraping system metrics

✔ Node Exporter exposing host information

✔ Grafana visualizing everything beautifully

✔ Fully dockerized monitoring stack

🧰 Technologies Used

Docker

Prometheus

Node Exporter

YAML

Windows

👩‍💻 Author

Iswarya N
GitHub: https://github.com/ISWARYA2025N
