**Transport Control Protocol | Ephemeral Ports| Well-Known Ports**

Connection-oriented transport protocol that sends data as an unstructured stream of bytes [[OSI Layer 4 - Transport]]

#Q What are TCP features?
- Provides sending node with delivery information about packets transmitted to a destination node. 
- If data has been lost in transit from source to destination, TCP can retransmit the data
- Recognize duplicate messages and will discard them appropriately. 
- If transmission is too fast for the receiving computer, TCP can employ flow control mechanisms to slow data transfer.
- Communicates delivery information to the upper-layer protocols and applications it supports


#Q How does TCP work?
TCP Segments are contained/encapsulated in IP packets. Packets carry segments - each segment has a source and destination ports, sequence number, acknowledgement, flags'n'things*, window - number of bytes between acks, checksum - error checking. Urgent pointer - used by FTP, etc.

![[Pasted image 20240217142234.png]]
Fig. TCP

#Q What are the flags in TCP?
Connection oriented.

ACK => Acknowledge (a segment)
FIN => Finish (to close)
SYN => Synchronize (sequence numbers)

Client and Server establishes a connection via a 3-way handshake.

1. SYN: Client sends a random sequence number within a segment called an Initial Sequence Number (ISN). cs.
2. SYN-ACK: cs+1, ss.
3. ACK: ss+1, cs+1
![[Pasted image 20240217145035.png]]

See [[IP]]