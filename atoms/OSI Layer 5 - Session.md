### OSI Layer 5 - Session
Session.
Maintains connections over ports and session.

#Q What is the responsibility of Layer 5?
It is responsible for managing the communication sessions between applications running on different devices. It defines protocols for session establishment, maintenance, and termination, as well as for managing session security and synchronization.

![[Pasted image 20240217145812.png]]
Layer 4: Stateless Firewall requires ports to be opened for both well-known as well as ephemeral. Two rules, one for inbound and one for outbound. [[NACL]] in AWS works this way - that need 
Layer 5: Stateful Firewall understands and remembers the client ephemeral port. [[SG|Security Groups]] in AWS works this way, the in inbound port is opened for the session initiated.