Border Gateway Protocol allows different networks to connect to each other and exchange information about how to route traffic. It is the foundation of the Internet, and without BGP, the Internet would not be able to function.

At it's core BGP is a routing protocol used to exchange routing information between different networks on the internet. BGP is the protocol that enables the internet to function as a global network of interconnected networks. BGP is responsible for choosing the best path for network traffic to follow from one network to another, and for announcing that path to other routers on the internet.

BGP is a complex protocol, but it can be summarized as follows:

-   BGP routers exchange information about their networks with each other.
-   This information includes the routes that each router knows how to reach other networks.
-   When a BGP router receives new information, it updates its routing table and uses that information to route traffic.
- BGP picks the path with the least hops. No performance considerations. ASPATH pre-pending can make paths look worse. It only advertises the shortest paths to routes.

iBGP => Internal BGP - Routing within an AS.
eBGP => External BGP - Routing between AS's.


![[Autonomous System]]