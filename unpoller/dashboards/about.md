# Grafana Dashboards for Unpoller

These dashboards are located in this repo: [Unpoller Dashboards - latest](https://github.com/unpoller/dashboards/tree/master/v2.0.0)

### Note:
For whatever reason, these appear more up to date than the unpoller dashboards listed on the Grafana website.

1. [UniFi-Poller_ Client DPI - InfluxDB.json](https://github.com/unpoller/dashboards/blob/master/v2.0.0/UniFi-Poller_%20Client%20DPI%20-%20InfluxDB.json)
2. [UniFi-Poller_ Client Insights - InfluxDB.json](https://github.com/unpoller/dashboards/blob/master/v2.0.0/UniFi-Poller_%20Client%20Insights%20-%20InfluxDB.json)
3. [UniFi-Poller_ Network Sites - InfluxDB.json](https://github.com/unpoller/dashboards/blob/master/v2.0.0/UniFi-Poller_%20Network%20Sites%20-%20InfluxDB.json)
4. [UniFi-Poller_ UAP Insights - InfluxDB.json](https://github.com/unpoller/dashboards/blob/master/v2.0.0/UniFi-Poller_%20UAP%20Insights%20-%20InfluxDB.json)
5. [UniFi-Poller_ USG Insights - InfluxDB.json](https://github.com/unpoller/dashboards/blob/master/v2.0.0/UniFi-Poller_%20USG%20Insights%20-%20InfluxDB.json)
6. [UniFi-Poller_ USW Insights - InfluxDB.json](https://github.com/unpoller/dashboards/blob/master/v2.0.0/UniFi-Poller_%20USW%20Insights%20-%20InfluxDB.json)

### How to use in Grafana:
1. Click on the Dashboard (github) link above, and Copy the JSON.
2. In Grafana, navigate to `Menu` > `Dashboards` > `New` > `**Import**`
3. In the  "Import via dashboard JSON model, paste the JSON text you copied earlier.
4. Click `Load`
5. **Import dashboard**
  - `Name`: _(whatever you want to name the dashboard you are importing)_
  - `Folder`: _(Select a folder where this dashboard will be sorted into)_
  - `Unique Identifier`: Leave it whatever is set automatically.
  - `Unpoller`: Select the Influxdb dashboard.
  - Click `Import`
  - Repeat these steps for the additional dashboards.
