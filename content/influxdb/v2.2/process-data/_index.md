---
title: Process data with InfluxDB tasks
seotitle: Process data with InfluxDB tasks
description: >
  InfluxDB's task engine runs scheduled Flux tasks that process and analyze data.
  This collection of articles provides information about creating and managing InfluxDB tasks.
menu:
  influxdb_2_2:
    name: Process data
weight: 6
influxdb/v2.2/tags: [tasks]
related:
  - /resources/videos/influxdb-tasks/
---

Process and analyze your data with tasks in the InfluxDB **task engine**. Use tasks (scheduled Flux queries)
to input a data stream and then analyze, modify, and act on the data accordingly.

Discover how to create and manage tasks using the InfluxDB user interface (UI)
and the `influx` command line interface (CLI).
Find examples of data downsampling, anomaly detection _(Coming)_, alerting
_(Coming)_, and other common tasks.

{{% note %}}
Tasks replace InfluxDB v1.x continuous queries.
{{% /note %}}

{{< children >}}
