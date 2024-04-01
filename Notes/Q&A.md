  
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
     - This is a backup and restore DR strategy. Backup and restore DR strategies typically have the lowest cost but highest recovery time. A solution that manually rebuilds the hosting infrastructure on premises and downloads the data that a company has backed up could take hours or days
4. Amazon Cognito provides authentication, authorization, and user management for your web and mobile apps. Users can sign in directly with a user name and password, or through a trusted third party.

5. Retrieve instance metadata :- http://169.254.169.254/latest/meta-data/

6. Note
   - **A customer gateway** is required for the VPN connection to be established. A customer gateway device is set up and configured in the customer's data center. 
   - **API Gateway** is a fully managed service for developers to create, publish, maintain, monitor, and secure APIs at any scale. APIs act as the front door for applications to use to access data, business logic, or functionality from backend services. However, API Gateway is not necessary for the implementation of a VPN connection. 
   - A virtual private gateway is attached to a VPC to create a site-to-site VPN connection on AWS. You can accept private encrypted network traffic from an on-premises data center into your VPC without the need to traverse the open public internet. 
   - A **NAT gateway provides a way for private Amazon EC2 instances to send requests to the internet.** A NAT gateway **does not give you the ability to create an encrypted site-to-site VPN connection.**
7. Note
   - Baseline I/O performance for General Purpose SSD storage is 3 IOPS for each GiB, with a minimum of 100 IOPS. For 50 GiB of storage, the baseline performance would be 150 IOPS. 
   - Baseline I/O performance for General Purpose SSD storage is 3 IOPS for each GiB. For 334 GiB of storage, the baseline performance would be 1,002 IOPS. Additionally, General Purpose SSD storage is more cost-effective than Provisioned IOPS storage. 
   - 50 GiB of Provisioned IOPS storage with 1,000 IOPS would be more expensive than 334 GiB of General Purpose SSD storage.

8. Note
   - https://docs.aws.amazon.com/elasticloadbalancing/latest/application/sticky-sessions.html
     - If an EC2 instance were removed from the target group during a scale-in process, the EC2 instance would fail (or would be unhealthy if it were checked). An Application Load Balancer would stop routing requests to that target and would choose a new healthy target.
   - https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html#deregistration-delay
     - Elastic Load Balancing waits 300 seconds before the completion of the deregistration process, which can help in-flight requests to the target become complete. To change the amount of time that Elastic Load Balancing waits, update the deregistration delay value.
   - https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-scaling-cooldowns.html
     - Amazon EC2 Auto Scaling cooldown periods help you prevent Auto Scaling groups from launching or terminating additional instances before the effects of previous activities are apparent.

9. note
   - A **General Purpose SSD**  EBS volume is limited to **16,000** IOPS for each volume.
   - A **Provisioned SSD**  EBS volume provides up to **64,000** IOPS for each volume. offer storage with consistent and low-latency performance, and are designed for I/O intensive applications such as large relational or NoSQL databases.
   - A **Throughput Optimized HDD** EBS volume is an HDD-backed storage ,limited to **500** IOPS for each volume.
   - A **Cold HDD Magnetic volumes** provide the lowest cost per gigabyte of all EBS volume types and are ideal for workloads where data is accessed infrequently, and applications where the lowest storage cost is important. Cold HDD volumes are a good fit for **large, sequential cold-data** workloads.
   
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
    2. persistent type remain alive all the time even if job is completed. 
       1. these job are preferred when continues jobs to run on the data.
       2. is particularly suited for workloads that run for extended periods or indefinitely, providing highly available and durable storage.

17. **Access control lists(ACL)** are used for controlling permissions to a computer system or computer network. They are used to filter traffic in and out of a specific device. Those devices can be network devices that act as network gateways or endpoint devices that users access directly.
18. **A storage optimized instance** is designed for workloads that require high, sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to applications.
19. note
    - **AWS Storage Gateway** connects an on-premises software appliance with cloud-based storage to provide seamless integration with data security features between your on-premises IT environment and the AWS storage infrastructure. 
    - **Elastic Fabric Adapter (EFA)** is a network device that you can attach to your **Amazon EC2** instance to **accelerate High Performance Computing (HPC) and machine learning applications.** EFA enables you to achieve the application performance of an **on-premises HPC cluster with the scalability, flexibility, and elasticity** provided by the AWS Cloud.
20. Global table