Address Resolution Protocol

Finds the MAC address for a given IP address.

Within a local network data is moved via [[OSI#OSI Layer 2 - Data]] Frames over [[OSI#OSI Layer 1 - Physical]]. ARP discovers which MAC is related to a given IP.

ARP broadcasts on Layer 2. It asks who has the destination IP address. The destination has ARP software running which responds with the info.

Step 1: ARP Request (to all devices on the local network).
Step 2: ARP Reply: The device on the local network recognizes it's own IP address in the ARP request and sends back an ARP reply. This reply contains it's MAC address, effectively saying "I am the device with the requested IP address and here is my MAC address"
Step 3: Address Resolution: Upon recievign the ARP reply. the device now knows the MAC addresses associated with the IP Address. It then uses L2 to construct Ethernet frames, and Layer 1 for transmission.

![[Pasted image 20240217140107.png]]
Fig. ARP in Action