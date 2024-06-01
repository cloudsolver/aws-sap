IPSec adds encryption and authentication to make the Internet Protocol (IP) more secure. It scrambles the data at its source and unscrambles it at its destination. It also authenticates the source of the data. [Source](https://aws.amazon.com/what-is/ipsec/)

### Phases
- IKE Phase 1 (Slow and Heavy)
	- Authenticate: Pre-shared key-/passwords shared
	- Using Asymmetric encryption to agree on, an create a shared Symmetric Key: Diffie-Hellman (DH) Keys created via public keys - symmetric encryption.
	- IKE SA Created 
- IKE Phase 2 (Fast and Agile)
	- Uses the keys agreed in phase 1
	- Agree encryption method, and keys used for bulk transfer
	- Created IPSEC SA - phase 2 tunnel (architecturally running over IKE Phase 1)

### IPSEC Types


**Policy Based**: "Who and What" focus. Based on source, destination IP addresses, protocol and port. When a traffic matches a policy, it is encrypted and sent through the tunnel. Simple, and static.

**Route Based**: "How" focus. Creates a Virtual interface (aka tunnel interface); routing protocols or static routes are ten used to direct traffic to this tunnel interface without needing to specify source IP. Scalable and complex.

### IPSec Modes

![[IPSec Modes.png|512]]
Fig. Modes [Source](https://www.twingate.com/blog/ipsec-tunnel-mode)

Site-to-Site [[VPN]] supports Internet Protocol security (IPsec) VPN connections.
-   **Transport**: IPSec transport mode encrypts only the data packet's payload and leaves the IP header in its original form. The unencrypted packet header allows routers to identify the destination address of each data packet. Therefore, IPSec transport is used in a close and trusted network, such as securing a direct connection between two computers. 
	- Transport mode can be used over [[DX]].
    
-   **Tunnel**: An encrypted link where data can pass from the customer network to or from AWS. The IPSec tunnel mode is suitable for transferring data on public networks as it enhances data protection from unauthorized parties. The computer encrypts all data, including the payload and header, and appends a new header to it.
    
    Each VPN connection includes two VPN tunnels which you can simultaneously use for high availability.
    
    See: [[GW]]
    
