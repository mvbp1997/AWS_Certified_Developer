## Envelope Encryption
- its a process for encrypting your data
- generally applies for files > 4KB in size

### Envelope Encryption in Action
- in the AWS KMS, using the CMK, generate a data key
  - use the GenerateDataKey API
  - Data Key is sometimes referred to as the Envelope Key
- use the Data Key to encrypt data
- CMK = encrypt data key
- Data Key = encrypt data 
  - data key is stored locally with your data
  - data keys are not stored anywhere in AWS KMS 

### Decryption in Action
- locally stored data and data key
- use the KMS API to decrypt your Data Key against the CMK stored in KMS 
  - returns plaintext data key
- use the decrypted data key to decrypt the data
  - after decryption it deletes the local data key from memory

### Why use Envelope Encryption
- Network: when you encrypt data directly with KMS, the data must be transferred over the network
- Performance: with envelope encryption, only your data key is transmitted over the network
- Benefits: data key is used locally in your application or AWS service, avoiding network transfers

---
## Exam Tips: Envelope Encryption
- all about encrypting the key that encrypts our data
- CMK is used to encrypt data key (or envelope key)
- data key encrypts the data
- used for encrypting data over 4KB
- using the Envelope Encryption process improves performance by avoiding sending all your data into KMS over the network
- `GenerateDataKey` API call generates local data keys