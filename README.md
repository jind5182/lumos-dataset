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