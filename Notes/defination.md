
1. **Amazon S3 Storage classes**
    - The S3 storage classes include 
    - **S3 Intelligent-Tiering** for automatic cost savings for data with unknown or changing access patterns, 
    - **S3 Standard** for frequently accessed data, 
    - **S3 Express One Zone** for your most frequently accessed data, 
    - **S3 Standard-Infrequent Access (S3 Standard-IA)** and **S3 One Zone-Infrequent Access (S3 One Zone-IA)** for less frequently accessed data, 
    - **S3 Glacier Instant Retrieval** for archive data that needs immediate access, 
    - **S3 Glacier Flexible Retrieval (formerly S3 Glacier)** for rarely accessed long-term data that does not require immediate access, 
    - **Amazon S3 Glacier Deep Archive (S3 Glacier Deep Archive)** for long-term archive and digital preservation with retrieval in hours at the lowest cost storage in the cloud.
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
      - Amazon S3 Glacier Instant Retrieval is an archive storage class that delivers the lowest-cost storage for long-lived data that is **rarely accessed and requires retrieval in milliseconds**. 
      - With S3 Glacier Instant Retrieval, you can save up to 68% on storage costs compared to using the S3 Standard-Infrequent Access (S3 Standard-IA) storage class, when your data is accessed **once per quarter**. 
      - S3 Glacier Instant Retrieval delivers the fastest access to archive storage, with the same throughput and milliseconds access as the S3 Standard and S3 Standard-IA storage classes.
    - **Amazon S3 Glacier Flexible Retrieval (Formerly S3 Glacier)**
      - S3 Glacier Flexible Retrieval delivers low-cost storage, **up to 10% lower cost (than S3 Glacier Instant Retrieval)**, for archive data that is accessed **1—2 times per year** and is retrieved asynchronously. 
      - For archive data that does not require immediate access but needs the flexibility to retrieve large sets of data at no cost, such as backup or disaster recovery use cases, S3 Glacier Flexible Retrieval (formerly S3 Glacier) is the ideal storage class.
    - **Amazon S3 Glacier Deep Archive**
      - S3 Glacier Deep Archive is Amazon S3’s lowest-cost storage class and supports long-term retention and digital preservation for data that may be accessed **once or twice in a year**. 
      - It is designed for customers—particularly those in highly-regulated industries, such as financial services, healthcare, and public sectors—that retain data sets for 7—10 years or longer to meet regulatory compliance requirements. 
      - S3 Glacier Deep Archive can also be used for backup and disaster recovery use cases, and is a cost-effective and easy-to-manage **alternative to magnetic tape systems, whether they are on-premises libraries or off-premises services. 
      can be restored within 12 hours.**
    - **S3 Outposts**
      - Amazon S3 on Outposts delivers object storage to your on-premises AWS Outposts environment. 
      - Using the S3 APIs and features available in AWS Regions today, S3 on Outposts makes it easy to store and retrieve data on your Outpost, as well as secure the data, control access, tag, and report on it. 
      - ideal for workloads with local data residency requirements.
    

2. **Fargate** allocates the right amount of compute, eliminating the need to choose instances and scale cluster capacity. 
   - You only pay for the resources required to run your containers, so there is no over-provisioning and paying for additional servers. 
   - By default, Fargate tasks are given a minimum of **20 GiB of free ephemeral storage**
3. **AWS Transit Gateway** is a service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single gateway. 
   - As you grow the number of workloads running on AWS, you need to be able to scale your networks across multiple accounts and Amazon VPCs to keep up with the growth.
4. **Notes**
     - Throttling is the process of limiting the number of requests an authorized program can submit to a given operation in a given amount of time. API gateway can handle this not LoadBalancer.
     - You can use **AWS WAF with your Application Load Balancer to allow or block requests based on the rules** in a web access control list (web ACL).Configure the listener over HTTP and HTTPS to forward traffic to the application target group.
     - Accidental deletion of data in the bucket can be handled by **Enable versioning on the bucket**  and **Enable MFA** on the bucket.
     - Use multipart uploads for faster file uploads into the destination S3 bucket or use S3 Transfer acceleration.
     - When you apply a retention period to an object version explicitly, you specify a Retain Until Date for the object version and Different versions of a single object can have different retention modes and periods
     - ECS with EC2 launch type is charged based on EC2 instances and EBS volumes used. ECS with Fargate launch type is charged based on vCPU and memory resources that the containerized application requests
     - A **security group** acts as a virtual firewall for your instance to control inbound and outbound traffic.
     - Using an Elastic Load Balancer is an ideal solution for adding **elasticity** to your application. 
     - **Karpenter** to automatically adjusts the **number of nodes in the EKS cluster when pods fail or are rescheduled onto other nodes**
     - AWS Transit Gateway and add VPC attachments to connect all departments. Set up AWS Network Firewall to secure the application traffic travelling between the VPCs
     - **RAID 0** configuration enables you to **improve your storage volumes’ performance by distributing the I/O across the volumes** in a stripe. Therefore, if you add a storage volume, you get the straight addition of throughput and IOPS.
     - **RAID 1** configuration is used for **data mirroring**
     - Implement Lake Formation tag-based access control to enable authorization and cross-account permissions for the needed datasets to engineering team accounts. 
       - Integrate with AWS Security Hub to enhance security monitoring and compliance oversight.
5. Note
   - **AWS Application Discovery Service** helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers. 
     - Application Discovery Service is integrated with AWS Migration Hub, which simplifies your migration tracking as it aggregates your migration status information into a single console. You can view the discovered servers, group them into applications, and then track the migration status of each application from the Migration Hub console in your home region.
   - **AWS Migration Hub (Migration Hub)** provides a single place to discover your existing servers, plan migrations, and track the status of each application migration. The Migration Hub provides visibility into your application portfolio and streamlines planning and tracking.
   - **AWS Application migration** is the process of moving software applications from one computing environment to another. 
     - This can include migrating applications from one data center to another, such as from a public to a private cloud, or from a company's on-premises server to a cloud provider's environment.
     - you **can’t assign an Elastic IP address to an Application Load Balancer**. The alternative method you can do is assign an Elastic IP address to a Network Load Balancer in front of the Application Load Balancer.
6. ![img_1.png](img_1.png)

7. **Amazon Aurora Serverless v2** scales instantly to hundreds of thousands of transactions in a fraction of a second. 
   1. As it scales, it adjusts capacity in fine-grained increments to provide the right amount of database resources that the application needs. There is no database capacity for you to manage. You pay only for the capacity your application consumes, and you can save up to 90% of your database cost compared to the cost of provisioning capacity for peak load.
8. note
   - **Predictive scaling** uses machine learning to predict capacity requirements based on historical data from CloudWatch. The machine learning algorithm consumes the available historical data and calculates capacity that best fits the historical load pattern, and then continuously learns based on new data to make future forecasts more accurate.
9. ![img_2.png](img_2.png)
10. Note 
  - **install CloudWatch Agent** to collect more system-level metrics from Amazon EC2 instances. Here’s the list of custom metrics that you can set up:
  - Memory utilization
  - Disk swap utilization
  - Disk space utilization
  - Page file utilization
  - Log collection
12. 
  ![img_5.png](img_5.png)
13. **Scaling**
  - **Target tracking** or step scaling policies can trigger a scaling activity immediately without waiting for the cooldown period to expire. 
  - **Simple scaling** you need to wait for the cooldown period to complete before initiating additional scaling activities. 
  - **Scheduled scaling** is mainly used for predictable traffic patterns.
  - **Suspend and resume scaling** this type is used to temporarily pause scaling activities triggered by your scaling policies and scheduled actions.
14. 