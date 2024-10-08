  
- i am policy to ensure encrypted EBS volume can be created is :


    {
        "Sid" : "Name001",
        "Effect" : "Allow",
        "Action" : [
            "ec2: createdVolume"
        ],
        "Condition":{
            "Bool": {
                "ec2: encrypted" : "true"
            }
        },
        "Resource": [
            "*"
        ]
    }

- in Convertible Reserved Instances, you are allowed to exchange another Convertible Reserved instance with a different instance type and tenancy.

- **Amazon FSx for Lustre** is an ideal solution for the **animation studio’s** requirements. 
  - FSx for Lustre provides a fully managed, high-performance, scalable storage service, specifically designed for **compute-intensive workloads like 3D** animation rendering.
  - It offers shared storage with sub-millisecond latencies and can deliver up to terabytes per second of throughput, crucial for handling **hundreds of gigabytes** of data daily as in the studio’s case.
  - Lustre is a popular **open-source parallel file system** which stores data across multiple network file servers to maximize performance and reduce bottlenecks.
- **FSx for Lustre scratch file systems** are optimized for high-performance computing applications and provide high throughput and low latency, 
  - they are designed for temporary storage and are not intended for long-term persistence.
- if customer have AWS CloudTrail enabled for logging purposes , then we can **Query with AWS CloudTrail Lake to find specific errors** in CloudTrail logs.

- "a serverless architecture that allows AWS Lambda to access an Amazon DynamoDB table named tutorialsdojo in the US East (N. Virginia) region. The IAM policy attached to a Lambda function allows it to put and delete items in the table. The policy must be updated to only allow two operations in the tutorialsdojo table and prevent other DynamoDB tables from being modified."



    {
        "Version" : "2012-10-17",
	"Statement": [
		{
			"Sid": "tutorialDojo",
			"Effert": "Allow",
			"Action" :[
					"dynamodb:PutItem",
					"dynamodb:DeleteItem"
			],
			"Resource": "arn:aws:dynamodb:us-east-1:1206181206:table/tutorialDojo"
		}
	  ]
    }
- "A serverless application has been launched on the DevOps team’s AWS account. Users from the development team’s account must be granted permission to invoke the Lambda function that runs the application."

  
    {
      "Version" : "2012-10-17",
      "Id":"default",
      "Statement": [
          {
              "Sid": "tutorialDojo-lambda-allow-s3-my-function",
              "Effert": "Allow",
              "Principal":{
                  "Service": "s3.amazonaws.com"
              },
              "Action" :"lambda.invokeFunction",
              "Resource": "arn:aws:dynamodb:us-east-1:1206181206:table/tutorialDojo",
              "Condition": {
                  "StringEquals":{
                      "AWS:SourceAccount": "12345678"
                  },
                  "ArnLike":{
                      "AWS:sourceArn": "arn:aws:s3:::tutorialDojo-lambda-allow-s3-my-function"
                  }
              }
          }
      ]
  }
  

- To determine whether a log file was modified, deleted, or unchanged after CloudTrail delivered it, you can use **CloudTrail log file integrity validation**. 
- This feature is built using industry-standard algorithms: SHA-256 for hashing and SHA-256 with RSA for digital signing.
  - ![img.png](img.png)

    - "The DevOps Team at Agila Corporation aims to enforce an IAM policy that grants them exclusive permissions to start, stop, and terminate EC2 instances in the us-west-1 region. To maintain strict security measures, any requests originating outside the company’s network range (192.158.1.0/24) should be denied."



      {
          "Version": "2012-10-17",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "ec2:TerminateInstances",
                      "ec2:StartInstances",
                      "ec2:StopInstances"
                  ],
                  "Resource": "*",
                  "Condition": {
                      "StringEquals": {
                          "aws:RequestedRegion": "us-west-1"
                      }
                  }
              },
              {
                  "Effect": "Deny",
                  "Action": "ec2:*",
                  "Resource": "*",
                  "Condition": {
                      "NotIpAddress": {
                          "aws:SourceIp": "192.158.1.0/24"
                      }
                  }
              }
          ]
      }

- **AWS Glue Job bookMarks**  - help AWS Glue **maintain state information and prevent the reprocessing of old data**.
- **The AWS Glue Data Catalog** is a centralized metadata repository for all your data assets across various data sources. It provides a unified interface to store and query information about data formats, schemas, and sources.
- **FLEX execution** class leverages spare capacity within the AWS infrastructure to run **Glue jobs** at a discounted price compared to the **standard execution** class. 
  - Since the data engineer doesn't have specific time constraints, utilizing spare capacity is ideal for cost savings.
  - Today's date it's a checkbox in order to spare capacity and will mean we dont know when is going to finish, which is recommended to increase a timeout

1. How to handle elastic load balancer in the system ?
   - option 1. if the first load balancer fails , we can have a secondary load balancer as backup. 
   - option 2. we can have load balancer in multi AZ for failure proof. 
   - option 3. we can temporarily modify the API gateway to route the traffic directly to the indivisual server or machine.
   - in short ,amazon load balancer are failure proof, only if they are setup on multiple availability zone

2. A company has a large on-premises data center and wants to establish a **dedicated network connection** between their data center and the AWS Cloud. They require a **high-bandwidth, low-latency** connection for transferring large amounts of data securely. Which AWS service should they use? 
     - A. AWS Site-to-Site VPN 
     - B. **AWS Direct Connect** 
     - C. AWS VPN CloudHub 
     - D. AWS Transit Gateway
     - **ANS**:- A. Incorrect. AWS Site-to-Site VPN would allow establishing an **encrypted VPN connection** over the public internet between the on-premises data center and AWS. However, it does **not provide a dedicated high-bandwidth, low-latency** connection. 
     - B. Correct. AWS Direct Connect provides a dedicated private network connection between the on-premises data center and AWS. It offers high bandwidth capacity and low latency for transferring large volumes of data. 
     - C. Incorrect. AWS VPN CloudHub operates on top of AWS Site-to-Site VPN connections. It allows establishing a single VPN connection to AWS and then access multiple VPCs. It does not provide a dedicated high-bandwidth, low-latency connection. 
     - D. Incorrect. AWS **Transit Gateway allows interconnecting multiple VPCs** and on-premises networks using a central hub. However, it does not establish a dedicated network connection between the on-premises data center and AWS. 
     - In summary, answer **choice B** is the correct choice because AWS Direct Connect meets the requirements stated in the question of a high-bandwidth, low-latency dedicated network connection between the on-premises data center and AWS.
3. **Disaster recovery (DR)** 
     - Resiliency can be defined in terms of metrics called 
       - **RTO** (Recovery Time Objective)
       - **RPO** (Recovery Point Objective)
     - **Pilot light DR strategy**. This solution recreates an existing application hosting environment in an AWS Region. This solution turns off most (or all) resources and uses the resources only during tests or when DR failover is necessary. **RPO and RTO are usually 10s of minutes**.
     - **Warm standby DR strategy**. This solution recreates an existing application hosting environment in an AWS Region. This solution serves a portion of live traffic. With this DR strategy, **RPO and RTO are usually a few minutes**. However, **costs are higher** because this solutions **runs resources continuously**.
     - **Backup and restore DR strategy**. This strategies typically have the lowest cost but highest recovery time. A solution that manually rebuilds the hosting infrastructure on premises and downloads the data that a company has backed up could take hours or days
4. **Amazon Cognito** provides authentication, authorization, and user management for your web and mobile apps. Users can sign in directly with a user name and password, or through a trusted third party.

5. Retrieve instance metadata :- http://169.254.169.254/latest/meta-data/

6. Note
   - **A customer gateway** is required for the VPN connection to be established. A customer gateway device is set up and configured in the customer's data center. 
   - **A API Gateway** is a fully managed service for developers to create, publish, maintain, monitor, and secure APIs at any scale. APIs act as the front door for applications to use to access data, business logic, or functionality from backend services. However, API Gateway is not necessary for the implementation of a VPN connection. 
   - **A virtual private gateway** is attached to a VPC to create a site-to-site VPN connection on AWS. You can accept private encrypted network traffic from an on-premises data center into your VPC without the need to traverse the open public internet. 
   - **A NAT gateway** provides a way for private Amazon EC2 instances to send requests to the internet. A NAT gateway **does not give you the ability to create an encrypted site-to-site VPN connection.**

7. Note
   - https://docs.aws.amazon.com/elasticloadbalancing/latest/application/sticky-sessions.html
     - If an EC2 instance were removed from the target group during a scale-in process, the EC2 instance would fail (or would be unhealthy if it were checked). An Application Load Balancer would stop routing requests to that target and would choose a new healthy target.
   - https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html#deregistration-delay
     - Elastic Load Balancing waits 300 seconds before the completion of the deregistration process, which can help in-flight requests to the target become complete. To change the amount of time that Elastic Load Balancing waits, update the deregistration delay value.
   - https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-scaling-cooldowns.html
     - Amazon EC2 Auto Scaling cooldown periods help you prevent Auto Scaling groups from launching or terminating additional instances before the effects of previous activities are apparent.

8. **EBS Volume**
   - A **General Purpose SSD volume**  is limited to **16,000** IOPS for each volume.
   - A **Provisioned SSD volume** provides up to **64,000** IOPS for each volume. offer storage with consistent and low-latency performance, and are designed for I/O intensive applications such as large relational or NoSQL databases.
   - A **Throughput Optimized HDD volume** is an HDD-backed storage ,limited to **500** IOPS for each volume.
   - A **Cold Magnetic HDD volumes** provide the lowest cost per gigabyte of all EBS volume types and are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important. Cold HDD volumes are a good fit for **large, sequential cold-data** workloads.

    ![img_3.png](img_3.png)   

    ![img_4.png](img_4.png)
9. **EBS Volume Encryption**
  - EBS volumes are highly available and reliable storage volumes that can be attached to any running instance that is in the same Availability Zone. 
  - EBS volumes that are attached to an EC2 instance are exposed as storage volumes that persist independently of the life of the instance.
  - When you create an encrypted EBS volume and attach it to a supported instance type, the following types of data are encrypted:
    - Data at rest inside the volume 
    - All data moving between the volume and the instance 
    - All snapshots created from the volume 
    - All volumes created from those snapshots
10. note

    - A company has a web application hosted on Amazon EC2 instances in a private subnet within an Amazon Virtual Private Cloud (Amazon VPC). The instances in the private subnet cannot be accessed directly from the internet for security reasons. To manage and maintain these instances, the company needs to implement a secure solution. 
    - Which of the following approaches would be the most appropriate to address this requirement?
    
    - A. Create a bastion host (jump box) in a public subnet within the same VPC, and use it as an entry point to access the instances in the private subnet.
    - B. Configure a site-to-site VPN connection between the company's on-premises network and the VPC, allowing direct access to the instances in the private subnet.
    - C. Enable public IP addresses on the instances in the private subnet, and configure security groups to allow inbound traffic from specific IP addresses.
    - D. Create an AWS Lambda function that can be invoked from the internet to establish a secure connection to the instances in the private subnet.
    
    ANS:- 
    - A. Correct. Creating a bastion host (jump box) in a public subnet within the same VPC, and using it as an entry point to access the instances in the private subnet, is the most appropriate approach to securely manage and maintain the instances that cannot be accessed directly from the internet. The bastion host acts as a proxy to access the private instances. 
    - B. Incorrect. Configuring a VPN does allow direct access to the instances, but this exposes them to the internet. The goal is to keep them private. 
    - C. Incorrect. Enabling public IPs and configuring security groups exposes the instances directly to the internet, which compromises security. 
    - D. Incorrect. An AWS Lambda function invoked from the internet could allow access to the private instances, but it is more complex and less secure than using a bastion host.
11. note
    - Set up an IAM policy to ensure that only encrypted EBS volumes can be created. Create an AWS Config rule that tracks unencrypted EBS volumes and use an AWS Systems Manager Automation document for remediation.
12. note
    - want to track and log every request access to their S3 buckets including the requester, bucket name, request time, request action, referrer, turnaround time, and error code information. 
      - Enable server access logging for all required Amazon S3 buckets.
13. A multinational corporation is expanding its operations and needs to efficiently monitor and analyze IAM-related errors, specifically **Access Denied and Unauthorized errors** in their AWS accounts. The **company has AWS CloudTrail enabled for logging** purposes.

    - ANS: Query with **AWS CloudTrail Lake** to find specific errors in CloudTrail logs.
14. note : Migrate the RabbitMQ queue to Amazon MQ to a cluster broker deployment setup. Launch a Multi-AZ Auto Scaling group for the Amazon EC2 instances that host the consumer application. Migrate the existing database to Amazon RDS for PostgreSQL in a Multi-AZ Deployment configuration.

15. cloud formation
16. What are the different type of EMR cluster ?
    1. there are two cluster type one is persistent and transient cluster.
    2. **persistent type** remain alive all the time even if job is completed. 
       1. these job are preferred when continues jobs to run on the data.
       2. is particularly suited for workloads that run for extended periods or indefinitely, providing highly available and durable storage.

17. **Access control lists(ACL)** are used for controlling permissions to a computer system or computer network. They are used to filter traffic in and out of a specific device. Those devices can be network devices that act as network gateways or endpoint devices that users access directly.
18. **A storage optimized instance** is designed for workloads that require high, sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to applications.
19. note
    - **AWS Storage Gateway** connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure. 
    - **Elastic Fabric Adapter (EFA)** is a network device that you can attach to your **Amazon EC2** instance to **accelerate High Performance Computing (HPC) and machine learning applications.
      - ** EFA enables you to achieve the application performance of an **on-premises HPC cluster with the scalability, flexibility, and elasticity** provided by the AWS Cloud.

20. note 
    - Use AWS Database Migration Service (AWS DMS) to migrate to a **new Aurora Serverless database** from Aurora cluster. 
    - In the event that your primary database instance goes down. When failing over, Amazon RDS simply flips the canonical name record (CNAME) for your DB instance to point at the standby, which is in turn promoted to become the new primary.
    - **AWS Storage Gateway** - The service enables hybrid storage between on-premises environments and the AWS Cloud. 
    - Enable Cross-Region Snapshots Copy in your Amazon Redshift Cluster to implement a disaster recovery plan while using Redshift cluster. 
    - A VPC endpoint enables customers to privately connect to supported AWS services and VPC endpoint services powered by AWS PrivateLink. Amazon VPC instances do not require public IP addresses to communicate with resources of the service. Traffic between an Amazon VPC and a service does not leave the Amazon network.
    - We can use two types of VPC endpoints to access Amazon S3: **gateway endpoints and interface endpoints**.
      - A **gateway endpoint** is a gateway that you specify in your route table to access Amazon S3 from your VPC over the AWS network.
      - **Interface endpoints** extend the functionality of gateway endpoints by using private IP addresses to route requests to Amazon S3 from within your VPC, on-premises, or from a different AWS Region. Interface endpoints are compatible with gateway endpoints. If you have an existing gateway endpoint in the VPC, you can use both types of endpoints in the same VPC.


21. **Geolocation routing** lets you choose the resources that serve your traffic **based on the geographic location of your users**, meaning the location that DNS queries originate from. For example, you might want all queries from Europe to be routed to an ELB load balancer in the Frankfurt region.
22. Using **Route 53 Weighted Routing** policy just lets you **associate multiple resources** with a single domain name (tutorialsdojo.com) or subdomain name (forums.tutorialsdojo.com) and choose **how much traffic is routed to each resource**.

**Route 53 Health checking**
          - **Active-Active Failover** 
            - Use this failover configuration when you want **all of your resources to be available** the majority of the time. When a resource becomes unavailable, Route 53 can detect that it’s unhealthy and stop including it when responding to queries. 
            - In **active-active failover**, all the records that have the same name, the same type (**such as A or AAAA**), and the same routing policy (such **as weighted or latency**) are active unless Route 53 considers them unhealthy. 
            - Route 53 can respond to a DNS query using any healthy record.
          - **Active-Passive Failover** 
            - Use an active-passive failover configuration when you want a primary resource or group of resources to be available the majority of the time and you want a secondary resource or group of resources to be on standby in case all the primary resources become unavailable. When responding to queries, Route 53 includes only the healthy primary resources. If all the primary resources are unhealthy, Route 53 begins to include only the healthy secondary resources in response to DNS queries.

          **in the above note the  The service should be available 24/7 so the Active -Active Failover is the good choice with zero downtime in** 
23. Note
   - **Expedited retrievals** allow you to quickly access your data when occasional urgent requests for a subset of archives are required. For all but the largest archives (250 MB+), data accessed using Expedited retrievals are typically made available within 1–5 minutes. 
   - Provisioned Capacity ensures that retrieval capacity for Expedited retrievals is available when you need it.

To make an Expedited, Standard, or Bulk retrieval, set the Tier parameter in the Initiate Job (POST jobs) REST API request to the option you want, or the equivalent in the AWS CLI or AWS SDKs. If you have purchased provisioned capacity, then all expedited retrievals are automatically served through your provisioned capacity. 

24. **AWS Elastic Disaster Recovery (AWS DRS)** provides continuous block-level replication, recovery orchestration, and automated server conversion capabilities. These allow customers to achieve a crash-consistent recovery point objective (RPO) of **60 seconds**, and a recovery time objective (RTO) typically ranging between 5–20 minutes.
25. By simply selecting Spot when launching EC2 instances, you can save up to 90% on On-Demand prices. The only difference between On-Demand instances and Spot Instances is that Spot instances can be interrupted by EC2 with two minutes of notification when the EC2 needs the capacity back.
26. Note
  - Create an Amazon Pinpoint journey for the multi-engagement SMS marketing campaign and an Amazon Kinesis Data Stream for analysis. Configure Amazon Pinpoint to send events to the Kinesis data stream for collection, processing, and analysis. Set the retention period of the Kinesis data stream to 365 days.
  - In order for you to establish an SSH connection from your home computer to your EC2 instance, you need to do the following:
    - On the Security Group, add an Inbound Rule to allow SSH traffic to your EC2 instance. 
    - On the NACL, add both an Inbound and Outbound Rule to allow SSH traffic to your EC2 instance.
  - **Cross-origin resource sharing (CORS)** defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. 
    - With CORS support, you can build rich client-side web applications with Amazon S3 and selectively allow cross-origin access to your Amazon S3 resources.
27. Global table , internet gateway vs transient gateway , network LB vs application LB , envelope encryption and automates key rotation. ingress , pilot light disaster recovery (DR) 