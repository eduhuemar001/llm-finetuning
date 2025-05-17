# Prometheus Project

This Project sets up a monitoring stack using Docker Compose with the following services:

- `Node Exporter:` Collects host metrics.
- `Prometheus:` Stores and scrapes metrics from Node Exporter.
- `Grafana:` Visualizes metrics and dashboards from Prometheus.

## Step-by-step setup guide

1. Open CMD and navigate to the repository containing the docker compose file.
2. Build and run the container:

   ```bash
   docker compose up -d --build
   ```
   
   If down, container can be rerun with:
   
    ```bash
   docker compose up -d
   ```

3. Open [Grafana](http://localhost:3000).
4. Login with the default username and password `admin`.

### Setup Grafana

Once logged in to Grafana, you can follow these steps to configure Grafana.

#### Setup Prometheus as data source

1. Click on the search bar on right top. 
2. Select **Data Sources** 
3. Click **Add data source**
4. Click on **Prometheus**
5. Enter `http://prometheus:9090` in the **Prometheus server URL** Connection field

![Prometheus connection](/assets/prometheus_connection.png)

6. Click **Save & test** at the Bottom. It should indicate a success.

![Prometheus connected](/assets/prometheus_connected.png)

### Setup Node Exporter Dashboard

1. Click on **Dashboards** on the left global sidebar.
2. Click on the blue **New** button and select **Import**.
3. Enter `1860` into the Dashboard URL field.
4. Click on **load**.

![Node Exporter load](/assets/node_exporter_dashboard.png)

5. Click on **Select a Prometheus data source**. 
6. Select the default Prometheus option, that was added before as a data source.

![Prometheus data source](/assets/prometheus_data_source.png)

7. Click on **Import**.
8. Now the Dashboard **Node Exporter Full** should open up.

#### Pie Chart Integration

To use the Pie Chart that was installed with the Dockerfile, follow these steps.

1. In the **Node Exporter Full** dashboard, click the "Edit" Button.
2. Click on **Add** and **Visualization**.
3. Select **Pie Chart** in the **Visualization** Dropdown menu on the right side of the screen.
4. In the **Queries** Panel at the bottom, search for the **Enter a PromQL query …** field.
5. Add a new metric, for example CPU usage distributed by mode:

 ```bash
 sum by (mode) (rate(node_cpu_seconds_total{job="node-exporter"}[1m]))
 ```

![Pie Chart data](/assets/pie_chart_data.png)

6. Click on **Run queries**. The pie chart should be visualized now.
7. Click on **Save dashboard** at the top right.
8. Navigate back to the dashboard.

![Grafana dashboard](/assets/grafana_dashboard.png)
