Virtual LANs are possible with `802.1Q` Ethernet Frame adds a 32-bit field. 802 standard Ethernet frame.

VLAN, or Virtual Local Area Network, is a way to divide a single physical network into multiple logical networks. VLANs are commonly used to improve network performance, security, and manageability. Trunks are a way to carry VLAN traffic between network switches, while QinQ is a VLAN stacking technique that allows multiple VLAN tags to be added to a single Ethernet frame.

- Create separate L2 network segments
- Isolated - traffic isolation
- Different customers
- Different Networks (AWS [[DX]])
- Separate broadcast domains
- 802.1Q (VLANS), 802.1AD (nested QinQ VLANS)

The 802.1Q field enables virtualization as it contains 4096 values (0, 1 values are reserved for NO VLAN, MGMT) Frame.

![[Pasted image 20240218175749.png]]
The additional field allows for VLANs via tagging frames.

Default behavior for broadcasts is for switches to remove VLAN tagging.A tagged frame will only be sent to other access ports with the same VID or over a TRUNK port. Trunk ports include VLAN tagging.

![[Pasted image 20240218181635.png]]

