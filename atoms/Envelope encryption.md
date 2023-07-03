Is the practice of encrypting plaintext data with a data key and then encrypting the data key under another key. You must store the encrypted form of the data key so that you can use the data key to decrypt the encrypted data in the database. #secure 
[[KMS]] uses this technique, and [[S3]] benefits.

---

#Question  Data larger than 4KB needs to be encrypted, however [[KMS]] has a limit of 4KB. How can this be accomplished?

 `GenerateDataKey` API can be used for Envelope encryption. 
 The API call returns a symmetric Data Encryption Key - in plaintext and encrypted. The key is used to encrypt the data on the client side. 
 Then the encrypted file and the encrypted DEK are together sent for storage. KMS will decrypt the DEK with it's own key, and then use the DEK to decrypt the payload on the serverside. 
 `GenerateDataKeyWithoutPlaintext` gives you the key in its encrypted form, but it cannot be used immediately without another call to [[KMS]] to decrypt. Encryption SDK is provided by AWS, which implements this pattern. It can cache with its Data Key Caching feature.
 
![[KMS Envelop Encryption.png]]
Fig. Envelope Encryption with KMS Encrypted DEK
