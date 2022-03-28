## KMS API Calls Demo
- you need to make sure you have configured the resource with the right IAM user / permissions to be able to use the KMS key
- when encrypting a file, make sure to provide the CMK `key-id`
- if you want to re-encrypt an encrypted file with a new CMK, use the `re-encrypt` command (enables manual key rotation as well)
- `enabled-key-rotation` enables automatic key rotation
  - `get-key-rotation-status` returns if key rotation is enabled
- `generate-data-key` (provided the CMK) will create a data key
  - use AES_256
  - returns both plain text and cypher text output

---
## Exam Tips: KMS API Calls
- `aws kms encrypt`: encrypts plaintext into ciphertext using CMK
  - decrypt does the opposite
- `aws kms re-encrypt`: decrypts ciphertext and re-encrypts it within AWS KMS (useful for rotating the CMK)
- `aws kms enabled-key-rotation`: enable automatic key rotation for 365 days
- `aws kms generate-data-key`: use CMK to generate data key to encrypt data > 4KB