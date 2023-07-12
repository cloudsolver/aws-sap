### Summary of Encryption
Encrypt is a way of scrambling data so that only authorized parties understand it. #secure 


### Symmetric and Asymmetric Encryption 

- There are two types of encryption: symmetric and asymmetric. 
- `Ciphertext` is the algorithm that takes `plaintext` as the input and generates the key material as the output. 
- Encryption algorithms can be executed on the client side or server side.

**Symmetric Encryption** 

Shared key to encrypt and decrypt the data. e.g. session key between an authenticated server and browser

**Asymmetric Encryption**

Public key and private keys. A public key is used by the public to encrypt the data and is sent over an unsecured network. The server uses a secret private key

The use of a private key to sign a message is a crucial component of many security protocols, such as SSL/TLS, S/MIME, and [[PGP]], as well as digital certificates and other forms of digital identity verification.

**Hashing**

A one-way hash produces a unique `ciphertext` that can not be reversed to its original.

This is useful to validate integrity via independent checks.

**Encryption Algorithms**

> [[AES]] (Advanced Encryption Standard): Symmetric Key Encryption.
>[[RSA]] (Rivest-Shamir-Adleman): Asymmetric Key Encryption.
>[[Diffie-Hellman]]: Key exchange protocol

**Ciphertext**
> Is the encrypted text which is the output.


**Key Material**
>The actual secret key or keys used in a cryptographic system to encrypt and decrypt data

**Client-Side Encryption**

The server can never decrypt.
The server should never be able to decrypt.

**Envelope encryption**

The data key is used to encrypt the data on the client side. Then the data key is encrypted with the master key. The encrypted data key and encrypted data are stored together. The master key can decrypt the data key to decrypt the data.



## Resources

 1.  https://www.cloudflare.com/learning/ssl/what-is-encryption/
