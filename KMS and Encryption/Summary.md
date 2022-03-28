## KMS Summary
- CMK = Customer Master Keys
- setting up a CMK
  - create alias with a description and select where the key-material comes from
    - KMS provided, self-provided, or CloudHSM
  - configure key admin permissions: IAM users and roles that can administer the keys through KMS APIs
    - add, list, delete, update, etc.
  - configure key usage permissions: IAM users and roles that can use the key to encrypt/decrypt the data
- AWS-Managed CMK: AWS-provided and managed CMK and used on your behalf with other AWS services
  - is as easy as clicking a checkbox in the console
  - cannot manage, rotate, or change their key policies nor can you use them directly
- Customer-Managed CMK: you can provide your own CMK which you can use to encrypt/decrypt files
- Data Key: use this key to encrypt/decrypt large amounts of data (created using the CMK)
- KMS encryption keys (CMKs) are single-region by default
  - multi-region is possible in advanced options

## Envelope Encryption
- encrypt the key that encrypts the data
- CMK = used to create/encrypt/decrypt the data key (envelope key)
- data key = encrypts/decrypts the data
- used for files > 4KB
- Performance/Network benefits

## API Calls
- `encrypt`: plaintext --> ciphertext (using CMK)
- `decrypt`: cipher --> plaintext
- `re-encrypt`: re-encrypt an encrypted file with another key
- `enable-key-rotation`
- `generate-data-key`: uses CMK to generate data key