# M-Lab Internet Quality Monitoring

This project sets up an open-source internet quality monitoring stack on a Raspberry Pi using Docker. It runs regular M-Lab NDT7 speed tests, stores the results in Prometheus, and visualizes them using Grafana.

## Architecture

*   **NDT7 Prometheus Exporter:** Runs an M-Lab NDT7 test against the closest server and exposes the results (download, upload, latency, retransmission rate) on port `8080`.
*   **Prometheus:** Scrapes the exporter every 60 minutes and stores the time-series data.
*   **Grafana:** Provides dashboards to visualize the data over time.

## Prerequisites

*   Docker and Docker Compose installed on your Raspberry Pi.
*   The Raspberry Pi should be connected directly to your router via Ethernet for accurate measurements.

## Installation & Usage

1.  Copy this entire directory to your Raspberry Pi.
2.  Navigate to the directory on the Pi:
    ```bash
    cd pi-internet-monitoring
    ```
3.  Start the stack:
    ```bash
    docker compose up -d
    ```
4.  Access the services:
    *   **Prometheus:** `http://<raspberry-pi-ip>:9090`
    *   **Grafana:** `http://<raspberry-pi-ip>:3000` (Default login is `admin` / `admin`)

## Configuration

*   **Test Frequency:** To change how often the speed test runs, edit the `scrape_interval` in `prometheus/prometheus.yml`. By default, it runs every 60 minutes. Running it too frequently may impact your network performance and use significant bandwidth.
*   **Dashboards:** You will need to create or import a dashboard in Grafana and connect it to the Prometheus data source.
