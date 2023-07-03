#Question What are the features and limitations of Memcached?
**Answer:**
	- No HA, non-persistent, no backup and restore.
	- Multi-node for partitioning #performant

---

#Question How do you vertically scale a Memcached cluster?
**Answer**:
1. Create a new cluster with larger node sizes.
2. Point the application to the new cluster.
3. Delete the older, smaller cluster.

---

#Question How does Memcached cluster communicate about it's other nodes to the application?
Answer:
Once a node is connected to the application, the metadata from the node shares other IP addresses of the other modes in the cluster to the application.
![[Memcached_Autodiscovered.png | 384]]
Fig. Autodiscover nodes