# Introduction
This data repository includes large-scale performance data of Hadoop and Spark applications on Alibaba Cloud, HUAWEI Cloud, Tencent Cloud and UCloud. Since performance varies with different inputs, our data includes multiple combinations of applications and inputs. We use workload to describe an application and its input. The workloads are extracted from HiBench.

## VM Types

### Alibaba Cloud
* g6.large, g6.xlarge, g6.2xlarge
* c6.large, c6.xlarge, c6.2xlarge
* r6.large, r6.xlarge, r6.2xlarge
* hfg6.large, hfg6.xlarge, hfg6.2xlarge
* hfc6.large, hfc6.xlarge, hfc6.2xlarge
* hfr6.large, hfr6.xlarge, hfr6.2xlarge

### HUAWEI Cloud
* s6.large.2, s6.large.4, s6.xlarge.2, s6.xlarge.4, s6.2xlarge.2, s6.2xlarge.4
* c6.large.2, c6.large.4, c6.xlarge.2, c6.xlarge.4, c6.2xlarge.2, c6.2xlarge.4
* m6.large.8, m6.xlarge.8, m6.2xlarge.8

### Tencent Cloud
* s5.medium4, s5.medium8, s5.large8, s5.large16, s5.2xlarge16, s5.2xlarge32
* c3.large8, c3.large16, c3.2xlarge16, c3,2xlarge32
* m5.medium16, m5.large32, m5.2xlarge64

### UCloud
* N 2CPU 4GB, N 2CPU 8GB, N 2CPU 16GB
* N 4CPU 8GB, N 4CPU 16GB, N 4CPU 32GB
* N 8CPU 16GB, N 8CPU 32GB, N 8CPU 64GB

## Workloads
For each application, we use four different inputs—either data inputs or input parameters. Since some workloads cannot complete on some of the VM types, we totally have about 50 workloads with full performance data on 55 VM types.

## Dataset Formation
Each record id is encoded by its configuration and workload. Taken

```
alibaba/g6.xlarge/hadoop_aggregation_large_2
```
for example, it represents

* Alibaba Cloud g6.xlarge
* terasort on Hadoop2.7
* input is large
* the second run (3 runs in this dataset)

Others follows the same rule.

## Data Record
Each data record contains a execution result (report.json) and a history of low-level performance information (sar.csv).  An example execution result is
```
{
    "completed": true,
    "datasize": "small",
    "elapsed_time": "119.742",
    "framework": "spark",
    "input_size": "3200000000",
    "program": "ScalaSparkTerasort",
    "throughput_cluster": "26724123",
    "throughput_node": "26724123",
    "timestamp": "2020-09-24 14:05:47",
    "workload": "terasort"
}
```
The main fields are the *elapsed_time* and *completed*.  The output of low-level metrics has a timestamp and 72 metrics.
* timestamp
* cpu.[%usr, %nice, %sys, %iowait, %steal, %irq, %soft, %guest, %gnice, %idle]
* task.[proc/s, cswch/s]
* swap.[pswpin/s, pswpout/s]
* paging.[pgpgin/s, pgpgout/s, fault/s, majflt/s, pgfree/s, pgscank/s, pgscand/s, pgsteal/s, %vmeff]
* io.[tps, rtps, wtps, bread/s, bwrtn/s]
* memory.[kbmemfree, kbavail, kbmemused, %memused, kbbuffers, kbcached, kbcommit, %commit, kbactive, kbinact, kbdirty, kbanonpg, kbslab, kbkstack, kbpgtbl, kbvmused]
* swap.[kbswpfree, kbswpused, %swpused, kbswpcad, %swpcad]
* load.[runq-sz, plist-sz,ldavg-1, ldavg-5, ldavg-15, blocked]
* disk.[tps, rd_sec/s wr_sec/s, avgrq-sz, avgqu-sz, await, svctm, .%util]
* network.[rxpck/s, txpck/s, rxkB/s, txkB/s, rxcmp/s, txcmp/s, rxmcst/s, %ifutil]

```
timestamp,cpu.%usr,cpu.%nice,cpu.%sys,cpu.%iowait,cpu.%steal,cpu.%irq,cpu.%soft,cpu.%guest,cpu.%gnice,cpu.%idle,task.proc/s,task.cswch/s,swap.pswpin/s,swap.pswpout/s,paging.pgpgin/s,paging.pgpgout/s,paging.fault/s,paging.majflt/s,paging.pgfree/s,paging.pgscank/s,paging.pgscand/s,paging.pgsteal/s,paging.%vmeff,io.tps,io.rtps,io.wtps,io.bread/s,io.bwrtn/s,memory.kbmemfree,memory.kbavail,memory.kbmemused,memory.%memused,memory.kbbuffers,memory.kbcached,memory.kbcommit,memory.%commit,memory.kbactive,memory.kbinact,memory.kbdirty,memory.kbanonpg,memory.kbslab,memory.kbkstack,memory.kbpgtbl,memory.kbvmused,swap.kbswpfree,swap.kbswpused,swap.%swpused,swap.kbswpcad,swap.%swpcad,load.runq-sz,load.plist-sz,load.ldavg-1,load.ldavg-5,load.ldavg-15,load.blocked,disk.tps,disk.rd_sec/s,disk.wr_sec/s,disk.avgrq-sz,disk.avgqu-sz,disk.await,disk.svctm,disk.%util,network.rxpck/s,network.txpck/s,network.rxkB/s,network.txkB/s,network.rxcmp/s,network.txcmp/s,network.rxmcst/s,network.%ifutil
```


## How data is collected?
We run the sar tool in the background with a sampling interval of 5 seconds.

```
sar -p -A -o sar.dat 5
```