
# Discovering Data Collection Targets with File-Based Service Discovery

Prometheus offers a versatile range of options for discovering scraping targets, including support for Kubernetes, Consul, and more. If your system doesn't support service discovery natively, Prometheus’ file-based service discovery mechanism is an excellent alternative. This allows you to list scraping targets and associated metadata in a JSON file.

In this guide, we'll explore how to:

1. Install and run Node Exporter.
2. Configure and run Prometheus with file-based service discovery.
3. Dynamically update the targets list.
4. Visualize and analyze discovered metrics.

---

**Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)**

---

## Installing and Running Node Exporter

To begin, follow the instructions for installing Node Exporter in the [Node Exporter Guide](https://hulining.gitbook.io/prometheus/guides/node-exporter#installing-and-running-the-node-exporter).

Node Exporter runs on port 9100. Verify that it's exposing metrics by running the following command:

```bash
curl http://localhost:9100/metrics
```

You should see metrics output similar to this:

```plaintext
# HELP go_gc_duration_seconds A summary of the GC invocation durations.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 0
go_gc_duration_seconds{quantile="0.25"} 0
go_gc_duration_seconds{quantile="0.5"} 0
...
```

---

## Installing, Configuring, and Running Prometheus

Like Node Exporter, Prometheus is a static binary that can be installed using a tar package. [Download the latest version of Prometheus](https://prometheus.io/download#prometheus) suitable for your platform and extract it.

Replace the contents of the extracted `prometheus.yml` configuration file with the following:

```yaml
scrape_configs:
  - job_name: 'node'
    file_sd_configs:
      - files:
        - targets.json
```

This configuration sets up a job named `node` (for Node Exporter) that retrieves host and port information for Node Exporter instances from a `targets.json` file.

**Note:** For simplicity, this guide uses a manually created JSON configuration. In production, consider using a JSON generation tool.

Now, start Prometheus:

```bash
./prometheus
```

If Prometheus starts successfully, you'll see the following in the logs:

```plaintext
level=info ts=2018-08-13T20:39:24.905651509Z caller=main.go:500 msg="Server is ready to receive web requests."
```

---

## Exploring Discovered Metrics

Once Prometheus is up and running, you can use its [expression browser](https://hulining.gitbook.io/prometheus/visualization/browser) to view metrics exposed by `node`. For example, querying the metric `up{job="node"}` will show the Node Exporter instance discovered at `localhost:9100`.

---

## Dynamically Updating the Targets List

With Prometheus’ file-based service discovery, the instance listens for changes to the JSON file and updates the scraping target list dynamically without requiring a restart.

To demonstrate, launch another Node Exporter instance on port 9200. Then, modify the `targets.json` file to include the new instance:

```json
[
  {"targets": ["localhost:9100", "localhost:9200"]}
]
```

After saving the changes, Prometheus will automatically detect the updated targets list. Querying the metric `up{job="node"}` will now display two instances with `instance` labels: `localhost:9100` and `localhost:9200`.

---

## Summary

In this guide, we covered:

- Installing and running Node Exporter.
- Configuring Prometheus with file-based service discovery to dynamically discover scraping targets.
- Using Prometheus to retrieve and analyze metrics exposed by Node Exporter.

This workflow demonstrates how Prometheus' flexible file-based discovery mechanism simplifies the process of managing and dynamically updating scraping targets.

---

**Optimize your web scraping with ScraperAPI! Say goodbye to CAPTCHAs and proxies while extracting structured data from any source. Try it free today: 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)**

_Last updated 4 years ago._
