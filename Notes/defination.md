
1. **Amazon S3 Storage classes**
    - The S3 storage classes include 
    - **S3 Intelligent-Tiering** for automatic cost savings for data with unknown or changing access patterns, 
    - **S3 Standard** for frequently accessed data, 
    - **S3 Express One Zone** for your most frequently accessed data, 
    - **S3 Standard-Infrequent Access (S3 Standard-IA)** and **S3 One Zone-Infrequent Access (S3 One Zone-IA)** for less frequently accessed data, 
    - **S3 Glacier Instant Retrieval** for archive data that needs immediate access, 
    - **S3 Glacier Flexible Retrieval (formerly S3 Glacier)** for rarely accessed long-term data that does not require immediate access, 
    - **Amazon S3 Glacier Deep Archive (S3 Glacier Deep Archive)** for long-term archive and digital preservation with retrieval in hours at the lowest cost storage in the cloud.
   
    - 
    - **Amazon S3 Standard (S3 Standard)**:-
      - Standard offers high durability, availability, and performance object storage for frequently accessed data.
      - appropriate for a wide variety of use cases, including cloud applications, dynamic websites, content distribution, mobile and gaming applications, and big data analytics. 
    - **Amazon S3 Intelligent-Tiering (S3 Intelligent-Tiering)**
      - is the first cloud storage that automatically reduces your storage costs on a granular object level by automatically moving data to the most cost-effective access tier based on access frequency, without performance impact, retrieval fees, or operational overhead. 
      - S3 Intelligent-Tiering delivers milliseconds latency and high throughput performance for frequently, infrequently, and rarely accessed data in the Frequent, Infrequent, and Archive Instant Access tiers. 
      - You can use S3 Intelligent-Tiering as the default storage class for virtually any workload, especially data lakes, data analytics, new applications, and user-generated content.
    - **Amazon S3 Express One Zone**
      - is a high-performance, single-Availability Zone storage class purpose-built to deliver consistent single-digit millisecond data access for your most frequently accessed data and latency-sensitive applications. 
      - S3 Express One Zone can improve data access speeds by 10x and reduce request costs by 50% compared to S3 Standard.
    - **Amazon S3 Standard-Infrequent Access (S3 Standard-IA)**
      - S3 Standard-IA is for data that is accessed less frequently, but requires rapid access when needed. 
      - S3 Standard-IA offers the high durability, high throughput, and low latency of S3 Standard, with a low per GB storage price and per GB retrieval charge. 
      - This combination of low cost and high performance make S3 Standard-IA ideal for long-term storage, backups, and as a data store for disaster recovery files. 
    - **Amazon S3 Glacier Instant Retrieval**
      - Amazon S3 Glacier Instant Retrieval is an archive storage class that delivers the lowest-cost storage for long-lived data that is rarely accessed and requires retrieval in milliseconds. 
      - With S3 Glacier Instant Retrieval, you can save up to 68% on storage costs compared to using the S3 Standard-Infrequent Access (S3 Standard-IA) storage class, when your data is accessed once per quarter. 
      - S3 Glacier Instant Retrieval delivers the fastest access to archive storage, with the same throughput and milliseconds access as the S3 Standard and S3 Standard-IA storage classes.
    - **Amazon S3 Glacier Flexible Retrieval (Formerly S3 Glacier)**
      - S3 Glacier Flexible Retrieval delivers low-cost storage, **up to 10% lower cost (than S3 Glacier Instant Retrieval)**, for archive data that is accessed **1—2 times per year** and is retrieved asynchronously. 
      - For archive data that does not require immediate access but needs the flexibility to retrieve large sets of data at no cost, such as backup or disaster recovery use cases, S3 Glacier Flexible Retrieval (formerly S3 Glacier) is the ideal storage class.
    - **Amazon S3 Glacier Deep Archive**
      - S3 Glacier Deep Archive is Amazon S3’s lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed once or twice in a year. 
      - It is designed for customers—particularly those in highly-regulated industries, such as financial services, healthcare, and public sectors—that retain data sets for 7—10 years or longer to meet regulatory compliance requirements. 
      - S3 Glacier Deep Archive can also be used for backup and disaster recovery use cases, and is a cost-effective and easy-to-manage alternative to magnetic tape systems, whether they are on-premises libraries or off-premises services. 
      - can be restored within 12 hours.
    - **S3 Outposts**
      - Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment. 
      - Using the S3 APIs and features available in AWS Regions today, S3 on Outposts makes it easy to store and retrieve data on your Outpost, as well as secure the data, control access, tag, and report on it. 
      - ideal for workloads with local data residency requirements.
    
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
3. **Notes**
     - Throttling is the process of limiting the number of requests an authorized program can submit to a given operation in a given amount of time. API gateway can handle this not LoadBalancer.
     - You can use **AWS WAF with your Application Load Balancer to allow or block requests based on the rules** in a web access control list (web ACL).Configure the listener over HTTP and HTTPS to forward traffic to the application target group.
     - Accidental deletion of data in the bucket can be handled by **Enable versioning on the bucket**  and **Enable MFA** on the bucket.
     - Use multipart uploads for faster file uploads into the destination S3 bucket or use S3 Transfer acceleration.
     - When you apply a retention period to an object version explicitly, you specify a Retain Until Date for the object version and Different versions of a single object can have different retention modes and periods
     - ECS with EC2 launch type is charged based on EC2 instances and EBS volumes used. ECS with Fargate launch type is charged based on vCPU and memory resources that the containerized application requests
     - A **security group** acts as a virtual firewall for your instance to control inbound and outbound traffic.
     - Using an Elastic Load Balancer is an ideal solution for adding **elasticity** to your application. 
     - **Karpenter** to automatically adjusts the number of nodes in the EKS cluster when pods fail or are rescheduled onto other nodes
     - AWS Transit Gateway and add VPC attachments to connect all departments. Set up AWS Network Firewall to secure the application traffic travelling between the VPCs
     - RAID 0 configuration enables you to **improve your storage volumes’ performance by distributing the I/O across the volumes** in a stripe. Therefore, if you add a storage volume, you get the straight addition of throughput and IOPS.
     - Implement Lake Formation tag-based access control to enable authorization and cross-account permissions for the needed datasets to engineering team accounts. 
       - Integrate with AWS Security Hub to enhance security monitoring and compliance oversight.