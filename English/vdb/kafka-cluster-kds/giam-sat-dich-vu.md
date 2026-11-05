# Service Monitoring

When you create a Kafka Cluster, the system automatically collects the cluster's metrics through vMonitor Platform and displays them in the **Monitor** tab of the cluster detail page. Some metrics are enabled by default, with no extra configuration needed.

To view metrics:

1. Go to the Kafka Cluster detail page.
2. Select the **Monitor** tab.
3. Select **Cluster metric** to view metrics for the whole cluster, optionally filtered by topic, or **Node metric** to view metrics for each broker.
4. Select the time range in the top-right corner, from 15 minutes to 1 day.

Main charts available in the Monitor tab:

| View | Group | Charts |
| --- | --- | --- |
| Cluster metric | Topics and partitions | Topics, Partitions, Replicas, In Sync Replicas, Under Replicated Partitions |
| Cluster metric | Messages and consumer groups | Messages in per second, Messages consumed per second, Consumer Group Lag, Latest Offsets, Oldest Offsets |
| Node metric | Broker status | Brokers Online, Active Controllers, Offline Partitions Count, Unclean Leader Election |
| Node metric | Resources | CPU Usage, Memory Usage, Available Disk Space, Log Size |
| Node metric | JVM | JVM Memory Used, JVM GC Time, JVM GC Count, JVM Thread Count |
| Node metric | Throughput and requests | Byte Rate, Messages In Per Second, Produce Request Rate, Fetch Request Rate |

To view more metrics beyond the default set, build your own dashboards, or create alarms, select **Monitored by vMonitor Platform** to go to vMonitor Platform and enable Detailed Monitoring. See also:

* [Monitoring vDB with vMonitor Platform](../relational-database-service-rds/working-with-rds/giam-sat-hoat-dong-vdb-bang-vmonitor-platform.md)
* [List vDB's metrics](../../vmonitor-platform/cach-tinh-nang-cua-vmonitor-platform/metrics/danh-sach-metrics-ho-tro/danh-sach-metrics-cua-vdb.md)
