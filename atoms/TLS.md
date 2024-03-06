Newer version of SSL. 

Secure Socket Layer (SSL) and Transport Layer Security (TLS) are two cryptographic protocols used to provide secure communication over the internet. SSL was developed by Netscape in the mid-1990s and TLS is its successor. These protocols are used to secure web traffic, email, instant messaging, and other types of internet traffic. SSL and TLS use a combination of symmetric and asymmetric encryption to encrypt data, ensuring that information transmitted over the internet is secure and cannot be intercepted by unauthorized parties.

- Privacy and Data Integrity
- Privacy - communications are encrypted
- Asymmetric (initial) and symmetric (easier)
- Identity (server or client/server) verified. Usually client verifies server (although the client can verify itself)

The phases:
1. Cipher Suites: Protocols - key exchange algorithm, bulk encryption algorithm, message authentication code (mac) algorithm. Client and server must agree. TLS begins with an established TCP. Agree on Cipher Suite.
2. Authentication: server valid check, public key check, certificate check; Certificate Authority CA (trusted by OS, browser etc.) - CA signed a certificate, you can verify that the trusted CA signs the cert of the server.
3. Key Exchange: Move from asymmetric to symmetric. Client generates pre-master key by using server's public key which the server can decrypt with its private key. Both sides use pre-master key to generate the master secret which is use to generate ongoing session keys which encrypt and decrypt data.

![[Pasted image 20240218212027.png]]