SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces. Enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. There is no additional charge for using enhanced networking. Cluster [[EC2 Placement Groups]] would benefit from utilizing enhanced networking for tightly coupled workloads.

**Elastic Network Adapter (ENA)**

The Elastic Network Adapter (ENA) supports network speeds of up to **100 Gbps** for supported instance types.

The current generation instances use ENA for enhanced networking, except for C4, D2, and M4 instances smaller than `m4.16xlarge`.

**Intel 82599 Virtual Function (VF) interface**

The Intel 82599 Virtual Function interface supports network speeds of up to **10 Gbps** for supported instance types.

The following instance types use the Intel 82599 VF interface for enhanced networking: C3, C4, D2, I2, M4 (excluding m4.16xlarge), and R3.
