# Attention & Limitations

## A. Performance Optimization

Load Balancers are central to maintaining high availability and low latency across your application architecture. Optimizing performance ensures your Load Balancers efficiently handle high traffic volumes without creating bottlenecks.

To achieve maximum throughput on high-throughput or long-fat networks (LFN), ensure that:

1. Adequate Bandwidth Allocation: You have enabled an adequate Bandwidth package to support your peak traffic demands (see [Bandwidth](https://docs.greennode.ai/vserver/compute-hcm03-1a/vpc/bandwidth) Guidelines for details).

2. OS Kernel & Socket Buffer Tuning: Your client and backend servers (both ends of the traffic) are tuned at the OS kernel level so that socket buffer limits do not become a bottleneck. GreenNode's vLB are pre-tuned to deliver maximum throughput while maintaining traffic stability.

Below is an example configuration for Linux kernel socket buffer and congestion control optimization:

```bash
# Increase maximum socket receive/send buffer sizes
sudo sysctl -w net.core.rmem_max=134217728 
sudo sysctl -w net.core.wmem_max=134217728 

# Tune TCP receive/send buffer memory (min default max)
sudo sysctl -w net.ipv4.tcp_rmem="4096 131072 67108864" 
sudo sysctl -w net.ipv4.tcp_wmem="4096 131072 67108864" 

# Enable BBR congestion control and Fair Queueing
sudo sysctl -w net.ipv4.tcp_congestion_control=bbr 
sudo sysctl -w net.core.default_qdisc=fq 
```

To persist these changes across reboots, add the settings above to `/etc/sysctl.conf` and run `sudo sysctl -p`.


> **Trade-offs**: Aggressive kernel buffer increases and congestion control adjustments on your endpoints can utilize more network capacity, but it also increases memory (RAM) consumption per socket. We recommend monitoring your backend server's memory utilization (`free -m`) and network socket state (`ss -s`) when applying high-buffer `sysctl` parameters in production environments.