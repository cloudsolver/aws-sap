### OSI Layer 2 - Data
**Switches | Frames | MAC Address** 
Local. Layer 2 depends on Layer 1. Layer 2 is where frames are moved. It knows data format on the network resides.
![[Pasted image 20240217122254.png]]
 #Q What is the data layer responsible for?
 It is responsible for the reliable transfer of data between two nodes on the same network segment. This layer defines protocols for the access and use of the physical network, such as addressing, flow control, and error detection and correction.

This layer overcomes physical corruption of signal by introducing media access control.
CSMA/CD => Carrier Sense Multiple Access / Collision Detection used in Ethernet networks listens to devices before sending a signal. If a collision is detected, a jam signal is sent, then layer 2 waits a random amount of time before retrying. If a jam is again detected, a random large amount of time is waited.
#Q How does encapsulation work?
Layer 2 will encapsulate its payload before it sends data to layer 1.  Payload is encapsulated in a frame before it is sent down to layer 1.

#Q How does a switch work?
Switches use MAC Address Tables that it learns over time based on usage. It understands frame. 
![[Pasted image 20240217123817.png]]
The switch on layer 2 allows 1:1 (Unicast) and 1:N (Broadcast) communications.
