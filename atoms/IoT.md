AWS IoT Core #AWSService 

#Question What are the two primary ways for IoT devices to communicate with AWS?
- Device Gateway
	- The Device Gateway is the entry point for IoT devices connecting to AWS. It manages all active device connections and implements semantics for multiple protocols to verify that devices can securely and efficiently communicate with AWS IoT Core. Currently, the Device Gateway supports the [MQTT], [WebSockets], and HTTPS protocols.
- Message Broker