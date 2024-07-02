1. A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. 
2. Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other services does not leave the Amazon network.
3. In order for you to establish an SSH connection from your home computer to your EC2 instance, you need to do the following:
    - On the Security Group, add an Inbound Rule to allow SSH traffic to your EC2 instance.
    - On the NACL, add both an **Inbound and Outbound Rule to allow SSH traffic to your EC2 instance**. The reason why you have to add both Inbound and Outbound SSH rule is due to the fact that Network ACLs are stateless which means that responses to allow inbound traffic are subject to the rules for outbound traffic (and vice versa). 
    - In other words, if you only enabled an Inbound rule in NACL, the traffic can only go in but the SSH response will not go out since there is no Outbound rule. 
    - Security groups are stateful which means that **if an incoming request is granted, then the outgoing traffic will be automatically granted** as well, regardless of the outbound rules.
4. in an **Auto Scaling** there is a option to do  **step scaling policy and configure an instance warm-up time** condition.that can start application and keep it ready before spike every morning.
5. Although this service can host an ACID-compliant relational database that can handle complex queries and transactional (OLTP) workloads, it is still not scalable to handle the growth of the database. **Amazon Aurora** is the better choice as its underlying storage can grow automatically as needed.
6. Aurora automatically stores and manages database credentials in AWS Secrets Manager. Aurora rotates database credentials regularly, without requiring application changes. Secrets Manager secures database credentials from human access and plain text view.
7. AWS Network Firewall to create the required rules for traffic inspection and traffic filtering for the production VPC
8. if a application running in Prod , and software that access need high I/O then Take EBS snapshots of the production EBS volumes. Turn on the EBS **fast snapshot restore feature** on the EBS snapshots. Restore the snapshots into new EBS volumes. Attach the new EBS volumes to EC2 instances in the test environment. 
9. WS Direct Connect is a network service that allows you to establish a dedicated network connection from your on-premises data center to AWS. This connection bypasses the public Internet and can provide more reliable, lower-latency communication between your on-premises application and Amazon S3.
10. Use AWS Systems Manager Run Command to run a custom command that applies the patch to all EC2 instances.
11. S3 Glacier Deep is more resilience then S3 One Zone-Infrequent Access
12. All certificates in ACM are regional resources, including the certificates that you import. To use the same certificate with Elastic Load Balancing load balancers in different AWS Regions, you must import the certificate into each Region where you want to use it. To use a certificate with Amazon CloudFront, you must import it into the US East (N. Virginia) Region.
13. wants to forward all requests to the website so that the requests will use HTTPS , Create a listener rule on the ALB to redirect HTTP traffic to HTTPS. 
14. Security Group Inbound Rule: Protocol – TCP, Port Range – 22, Source 110.238.98.71/32 for ---- IP address (110.238.98.71) via an SSH connection.
15. "contain critical business data" so one zone IA is not safe in case of zone failure we should consider S3 Standard IA
16. Allows inbound access from the external IP range for the company. Then allow inbound SSH access from only the private IP address of the bastion host.
    1. C. This will restrict access to the bastion host from the specific IP range of the on-premises network, ensuring secure connectivity. This step ensures that only authorized users from the on-premises network can access the bastion host. 
    2. D. This step enables SSH connectivity from the bastion host to the application instances in the private subnet. By allowing inbound SSH access only from the private IP address of the bastion host, you ensure that SSH access is restricted to the bastion host only.
17. Database Migration Service is primarily focused on database migration and replication, and it may not be the most appropriate tool for general-purpose data transfer like JSON files.
18. Aurora Serverless also incurs no compute costs when it is idle
19. DynamoDB is a NoSQL database that supports key-value records. DAX delivers response times in microseconds.
20. **Amazon Certificate Manager (ACM)**
21. to build a site-to-site VPN connection to AWS we need 
    1. An internet gateway is attached to a VPC to allow traffic from the internet to flow into or out of the VPC. A VPN connection does not flow through an internet gateway. The internet gateway is designed to allow traffic from the open internet, not an encrypted VPN connection. 
    2. A customer gateway is required for the VPN connection to be established. A customer gateway device is set up and configured in the customer's data center. 
22. AWS Key Management Service used to store SSL keys not data Keys.

## Date May 2024

23. Use Amazon Rekognition to detect inappropriate content.
24. By default, CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE). 
25. Change the web architecture to access the financial data through a Gateway VPC Endpoint.
26. The ApproximateAgeOfOldestMessage metric is useful when applications have time-sensitive messages and you need to ensure that messages are processed within a specific time period. You can use this metric to set Amazon CloudWatch alarms that issue alerts when messages remain in the queue for extended periods of time
27. **Glacier Select** It is primarily used to run queries directly on data stored in Amazon Glacier, retrieving only the data you need out of your archives to use for analytics.
28. using **Cached volumes**, you store your data in Amazon Simple Storage Service (Amazon S3) and retain a copy of frequently accessed data subsets locally in your on-premises network. Cached volumes offer substantial cost savings on primary storage and minimize the need to scale your storage on-premises.
29. **AWS Wavelength** combines the high bandwidth and ultralow latency of 5G networks with AWS compute and storage services so that developers can innovate and build a new class of applications.
30. **AppSync pipeline resolvers** offer an elegant server-side solution to address the common challenge faced in web applications—aggregating data from multiple database tables. Instead of invoking multiple API calls across different data sources, which can degrade application performance and user experience, AppSync pipeline resolvers enable easy retrieval of data from multiple sources with just a single call. By leveraging Pipeline functions, these resolvers streamline the process of consolidating and presenting data to end-users.
31. **file system** that uses an NFS protocol  , **AWS Storage Gateway** storage solutions, only file gateway can store and retrieve objects in Amazon S3 using the protocols NFS and SMB.
32. The **Volume Gateway** is a cloud-based **iSCSI block storage volume** for your on-premises applications. The Volume Gateway provides either a local cache or full volumes on-premises while also storing full copies of your volumes in the AWS cloud.
    1. There are two options for Volume Gateway:
       1. Cached Volumes – you store volume data in AWS, with a small portion of recently accessed data in the cache on-premises. 
       2. Stored Volumes – you store the entire set of volume data on-premises and store periodic point-in-time backups (snapshots) in AWS.
33. Use the AWS Schema Conversion Tool to convert the source schema and application code to match that of the target database, and then use the AWS Database Migration Service to migrate data from the source database to the target database.

## Date June 2024

34. To limit access to this S3 bucket to only users of accounts within the organization in AWS Organizations , **Add the aws PrincipalOrgID global condition** key with a reference to the organization ID to the S3 bucket policy, 
35. A **S3 File Gateway** simplifies file storage in Amazon S3, integrates to existing applications through industry-standard file system protocols, and provides a cost-effective alternative to on-premises storage. It also provides low-latency access to data through transparent local caching.
36. Use AWS Network Firewall to **create the required rules for traffic inspection and traffic filtering for the production VPC**. 
    1. AWS Network Firewall is a managed firewall service that provides filtering for both inbound and outbound network traffic. It allows you to create rules for traffic inspection and filtering, which can help protect your production VPC. 
    2. Option A: Amazon GuardDuty is a threat detection service, not a traffic inspection or filtering service. 
    3. Option B: Traffic Mirroring is a feature that allows you to replicate and send a copy of network traffic from a VPC to another VPC or on-premises location. It is not a service that performs traffic inspection or filtering. 
    4. Option D: AWS Firewall Manager is a security management service that helps you to centrally configure and manage firewalls across your accounts. It is not a service that performs traffic inspection or filtering.
37. EBS fast snapshot restore feature on the EBS snapshots. helps to create a new Snapshot.
    1. Application Load Balancer:
    - Web applications with layer 7 routing (HTTP/HTTPS)
    - Microservices architectures (e.g. Docker containers)
    - Lambda targets
    2. Network Load Balancer:
    - TCP and UDP based applications
    - Ultra low latency
    - Static IP addresses
    - VPC endpoint services
38. Just all static content HTML, CSS, client-side JavaScript, images. Amazon S3 is good enough.
39. Gateway VPC allows direct access to S3 without going through public internet. 
40. AWS Systems Manager Run Command to run a custom command that applies the patch to all EC2 instances
41. Create a Regional API Gateway endpoint. Associate the API Gateway endpoint with the company's domain name. Import the public certificate associated with the company's domain name into AWS Certificate Manager (ACM) in the us-east-1 Region. Attach the certificate to the API Gateway APIs. Create Route 53 DNS records with the company's domain name. Point an A record to the company's domain name.
42. Store the database credentials as a secret in AWS Secrets Manager. Turn on automatic rotation for the secret. Attach the required permission to the EC2 role to grant access to the secret.
43. Secret manager supports AutoRotation. Where as Parameter Store does not support auto rotation. 
    1. Key Autorotation = AWS Secrets Manager
44. Use Amazon EventBridge (Amazon CloudWatch Events) to send a notification when the certificate is nearing expiration
45. A highly available connection with consistent low latency = AWS Direct Connect 
46. Minimize costs and accept slower traffic if the primary connection fails = VPN connection
47. By deploying an S3 VPC gateway endpoint, the application can access the S3 buckets over a private network connection within the VPC, 
    1. eliminating the need for data transfer over the internet. 
    2. This can help reduce data transfer fees as well as improve the performance of the application. 
    3. The endpoint policy can be used to specify which S3 buckets the application has access to.
48. near-real-time + large data + secure = DataSync over DirectConnect
49. **dynamoDB On-demand mode** is a good option if any of the following are true , 
    - You create new tables with unknown workloads.
    - You have unpredictable application traffic.
    - You prefer the ease of paying for only what you use.
50. AWS Systems Manager - for storing and managing secrets. 
    1. AWS Secrets Manager - for storeing credential and for autorotation of secrets
51. The Amazon Aurora MySQL DB provided better spped for cloning the database, while working on a clone we can take another with minimum time and any disruption/ latency.
52. Keyword: "separate read traffic from write traffic" = Read Replica = Option A and B are not the correct answer.
53. Create an S3 bucket with S3 Object Lock enabled. Enable versioning. Add a legal hold to the objects. Add the s3:PutObjectLegalHold permission to the IAM policies of users who need to delete the objects.
54. NAT gateway is used for outbound internet connectivity from private subnets, but it doesn't provide a private route for accessing S3.
    1. creating a VPC endpoint for S3, and linking the endpoint to the route table for private subnets. This ensures that file transfer traffic between the EC2 instances and S3 remains within the private network without going over the internet.
55. **enhanced security** - Configure Amazon CloudFront in front of the website to use HTTPS functionality
56. **static content** - Create the new website and an Amazon S3 bucket. Deploy the website on the S3 bucket with static website hosting enabled
57. **Amazon EBS for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage**
58. **OAI**
    1. An OAI provides secure access between CloudFront and S3 without exposing the S3 bucket publicly. 
    2. The OAI is associated with the CloudFront distribution. 
    3. The S3 bucket policy limits access only to that OAI. 
    4. This ensures only CloudFront can access the objects, not direct S3 access.
59. While CloudFront can accelerate content delivery by caching static content at edge locations, it may not be the most effective solution in this scenario. Since the portal delivers a mixture of static and dynamic content, leveraging Route 53 latency routing for dynamic content delivery ensures that users are directed to the nearest AWS Region hosting the dynamic content.
60. AWS Global Accelerator and Amazon CloudFront are separate services that use the AWS global network and its edge locations around the world. CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery). Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. Both services integrate with AWS Shield for DDoS protection.
61. ECS allows running Docker containers, so the existing monolithic app can be containerized and run on ECS with minimal code changes. 
    1. The app can be broken into smaller microservices by containerizing different components and managing them separately.
62. Use Reserved Instances for the baseline level of usage. Use Spot instances for any additional capacity that the application needs. 
63. **Composite alarms** determine their states by monitoring the states of other alarms. You can **use composite alarms to reduce alarm noise**. For example, you can create a composite alarm where the underlying metric alarms go into ALARM when they meet specific conditions. You then can set up your composite alarm to go into ALARM and send you notifications when the underlying metric alarms go into ALARM by configuring the underlying metric alarms never to take actions.
64. You can use **CloudFront to deliver video on demand** (VOD) or live streaming video using any HTTP origin 
65. **Global Accelerator is a good fit for non-HTTP use cases,** such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses