## Autonomous System

#Q What is AS (Autonomous System)?
AS is a large network or a group of networks under a single management - often an ISP, large organization or university. Within an AS the network admins can use their own policies for routing traffic internally.
#Q How does BGP utilize AS?
 BGP is made up of many self managing networks called AS. An AS can be a large collection of routers. It is treated as a black box. All BGP needs is a black-box what goes in and out of AS.
#Q What is an ASN?
Autonomous System Number.
 ASN are unique 16-bit and allocated by IANA (0-65535), 64512 - 65535 are private. There is also a 32-bit number.
 BGP operates on TCP/179 - it is reliable.
 Not automatic - peering is manually configured.
 #Q What is ASPATH?
 BPG is a path-vector protocol. It exchanges best path to destination between peers called ASPATH.