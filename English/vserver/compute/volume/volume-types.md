# Volume Types

Volume type is profile for performance of volume. GreenNode using Volume Type to implement data QoS on volume. Volume QoS can control the bandwidth and IOPS workload on your volume, you must chose right QoS for your application to have best experience.

## Volume QoS <a href="#volumetypes-volumeqos" id="volumetypes-volumeqos"></a>

IOPS measures the number of read/write operations that can be performed per second. High IOPS is critical for transaction-intensive applications such as database applications. The following table describes all IOPS profiles:

### NVME <a href="#nvme" id="nvme"></a>

**Support Region HCM (Zone 1a, 1b), HAN (Zone 1a, 1b)**

| IOPS  | Minimum Size (GB) | Throughput |
| ----- | ----------------- | ---------- |
| 3000  | 1                 | 200 MB/s   |
| 5000  | 1                 | 400 MB/s   |
| 10000 | 1                 | 600 MB/s   |
| 20000 | 1                 | 600 MB/s   |
| 40000 | 1                 | 600 MB/s   |
| 60000 | 1                 | 800 MB/s   |

​

### SSD <a href="#ssd" id="ssd"></a>

**Support Region HCM (Zone 1c)**

| IOPS  | Minimum Size (GB) | Throughput |
| ----- | ----------------- | ---------- |
| 3000  | 1                 | 200 MB/s   |
| 3200  | 1                 | 200 MB/s   |
| 6400  | 1                 | 400 MB/s   |
| 10000 | 1                 | 400 MB/s   |

​



You can change Volume Type at any time.

<br>
