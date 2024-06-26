1. **Server-side encryption** is the encryption of data at its destination by the application or service that receives it. AWS Key Management Service (AWS KMS) is a service that combines secure, highly available hardware and software to provide a key management system scaled for the cloud.
  - **Amazon S3 uses AWS KMS customer master keys (CMKs)** to encrypt your Amazon S3 objects.
  - **SSE-KMS encrypts** only the object data. Any object metadata is not encrypted. 
  - If you use **customer-managed CMKs, you use AWS KMS via the AWS Management Console** or AWS KMS APIs to centrally create encryption keys, define the policies that control how keys can be used, and audit key usage to prove that they are being used correctly. 

  - You can use these keys to protect your data in Amazon S3 buckets.


  - A **customer master key (CMK)** is a logical representation of a master key. The CMK includes metadata, such as the key ID, creation date, description, and key state. 
    - The CMK also contains the key material used to encrypt and decrypt data. 
    - You can use a CMK to encrypt and decrypt up to 4 KB (4096 bytes) of data. 
    - Typically, you use CMKs to generate, encrypt, and decrypt the data keys that you use outside of AWS KMS to encrypt your data. 
    - This strategy is known as **envelope encryption**.

  - You have three mutually exclusive options depending on how you choose to manage the encryption keys:
    - Use **Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)** 
      - **Each object is encrypted with a unique key.** 
      - As an additional safeguard, it encrypts the **key itself with a master key** that it regularly rotates. 
      - Amazon S3 server-side encryption uses one of the **strongest block ciphers** available, **256-bit** Advanced Encryption Standard (AES-256), to encrypt your data. 
    - Use **Server-Side Encryption with Customer Master Keys (SSE-CMKs)** 
      - Stored in AWS **Key Management Service (SSE-KMS)** – Similar to SSE-S3, 
      - but with some additional benefits and charges for using this service. 
      - There are separate permissions for the use of a CMK that provides **added protection against unauthorized access of your objects in Amazon S3**. 
      - SSE-KMS also provides you with an **audit trail that shows when your CMK was used and by whom**. 
      - Additionally, you can create and manage customer-managed CMKs or **use AWS managed CMKs that are unique to you**, your service, and your Region. 
    - Use **Server-Side Encryption with Customer-Provided Keys (SSE-C)**
      - You manage the encryption keys and Amazon S3 manages the encryption, as it writes to disks, and decryption when you access your objects.

  - Ans to the **Q** In the scenario, the company needs to store financial files in AWS which are accessed every week and the solution should use **envelope encryption**. This requirement can be fulfilled by using an Amazon S3 configured with Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS). Hence, using Amazon S3 to store the data and configuring Server-Side Encryption with AWS KMS-Managed Keys (SSE-KMS) are the correct answers.


- Configuring **Server-Side Encryption with Customer-Provided Keys (SSE-C) and configuring Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)** are both incorrect. 
  - Although you can configure automatic key rotation, these two do not provide you with an **audit trail that shows when your CMK was used** and by whom, unlike Server-Side Encryption with AWS KMS-Managed Keys **(SSE-KMS)**.


2. **Encryption**
   - SSE-S3:
     - AWS S3 manages its own keys
     - Keys are rotated every month
     - Request Header - x-amz-server-side-encryption(AES256)
   - SSE-KMS:
     - Customer manages keys in KMS
     - Request Headers - x-amz-server-side-encryption(aws:kms) and x-amz-server-side-encryption-aws-kms-key-id(ARN for key in KMS)
   - SSE-C:
     - Customer sends the key with every request
     - S3 performs encryption and decryption without storing the key
     - HTTPS is mandatory
   
   - Note:- You can choose to have AWS KMS automatically rotate KMS keys in a configurable range of days (from 90 days to 2560 days (7 years) or use the RotateKeyOnDemand API to invoke immediate key rotation (lifetime limit of 10 on-demand rotations per key). Automatic key rotation is not supported for imported keys, asymmetric keys, HMAC keys, or keys generated in a AWS CloudHSM cluster using the AWS KMS custom key store feature. You can rotate keys stored in the external key store (XKS), and you manage all key lifecycle events for external keys in your key manager.  

1. ![img_6.png](img_6.png)