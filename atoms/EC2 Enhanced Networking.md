#Question When should EC2 Enhanced Networking (ENA) be used? 

To support throughput near or exceeding 20K packets per second (PPS) on the VIF driver - Enhanced networking uses [[EC2 SR-IOV | single root I/O virtualization]] (SR-IOV) to provide high-performance networking capabilities on supported instance types.


#Question  How to enable enhanced networking?

[[EC2]] support Enhanced Network in two ways [[EC2 SR-IOV]] (ENA, VF) and [[EFA]].


See:[EC2 Enhanced Networking Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/enhanced-networking.html)

#### modinfo ena

On EC2 instances, ena is installed; however, not all types have an ena driver

```
[ec2-user@ip-172-31-9-177 ~]$ modinfo ena
filename:       /lib/modules/6.1.27-43.48.amzn2023.x86_64/kernel/drivers/amazon/net/ena/ena.ko
version:        2.8.3g
license:        GPL
description:    Elastic Network Adapter (ENA)
author:         Amazon.com, Inc. or its affiliates
srcversion:     7B3ACA8992B03F016F1770B
```

#### ethtool -i enX0

Driver is vif on EC2 T2
Note: eth0 is replaced by enX0 on 2023 Linux AMI
```
[ec2-user@ip-172-31-9-177 ~]$ ethtool -i enX0
driver: vif
version: 6.1.27-43.48.amzn2023.x86_64
firmware-version:
expansion-rom-version:
bus-info: vif-0
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: no
```


#### ethtool -i ens5
On EC2 T3 driver is **ena**

```
[ec2-user@ip-172-31-3-129 ~]$ ethtool -i ens5
driver: ena
version: 2.8.3g
firmware-version: 
expansion-rom-version: 
bus-info: 0000:00:05.0
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: yes
```