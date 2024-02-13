# AWS-Solutions-Architect-Associate

it has vary specific notes on the use cases of AWS components and helps in understanding each of them with short
descriiption

1. **AWS Transit Gateway**
    - Create a route table for the transit gateway and add a route that allows traffic between VPC A and VPC B's CIDR
      blocks. Associate this route table with VPC A and VPC B attachments.
2. **AWS Global Accelerator**
    - You are designing the architecture for a global SaaS application that will be deployed in the AWS cloud across
      multiple regions. The application needs to provide fast, reliable access for users across the globe. You want to
      improve performance and availability for users by routing traffic through the AWS global network.
3. **Cross-region replication**
    - copies objects between S3 buckets in different regions
4. **CloudFront**
    - used for caching content at the edge
5. **Snowball**
    - used for physical data transport
6. **Amazon Direct Connect**:
    - Move GB/s of data to the cloud, over a private secure network
    - from its on-premises data center to AWS
	
7. **Amazon Snowball**
    - Move PB of data to the cloud
    - migrate 50 TB of data from on-premises data centers to Amazon S3.
    - AMAZON Snowmobile
    - migrate 100 PB of data to Amazon S3. The company's Internet connection is only 10 Gbps. Ship the - data to AWS using Snowmobile to transfer the data offline.

8. **Amazon DataSync**
    - Move large amount of data between on-premises and S3, EFS, FSx for Windows
    - migrate 10 TB of data from an on-premises NAS device to Amazon S3. The data transfer needs to start - immediately and complete within 12 hours. Your on-premises network has a 1 Gbps connection to AWS.

9. **Transfer Acceleration**
    - a media company that frequently transfers large video files between an on-premises data center and Amazon S3. The
      company would like to accelerate these transfers to improve efficiency.
    - uses the AWS global network and edge locations to accelerate uploads to and downloads from an S3 bucket over long
      distances. This would help accelerate transfers between the on-premises data center and S3
10. **Virtual private gateway**.
     - Explanation: A virtual private gateway enables communication between a VPC and an on-premises network over an
       IPsec VPN tunnel. It supports overlapping IP address ranges and meets the requirements stated in the scenario.
11. **NAT gateway**
     - Instances in the private subnet can access the internet by using a NAT gateway.
     - The NAT gateway will perform source NAT and translate the private IP to a public IP when traffic goes to the
       internet

12. **Internet gateway**
     - Attaching an internet gateway to the VPC allows resources in the VPC such as instances in private subnets to
       connect to the internet by routing their traffic through a NAT gateway. This allows private resources internet
       access while keeping them private.

13. **VPC peering**
    - requirement : You have two VPCs, VPC A (10.0.0.0/16) in us-east-1 and VPC B (10.1.0.0/16) in us-west-2. You need
      to allow resources in VPC A to communicate with resources in VPC B.
    - VPC peering allows resources in two VPCs, even in different regions, to communicate with each other as if they are
      within the same network. A VPC peering connection needs to be created between the VPCs and routes configured to
      route traffic between them. This allows resources in VPC A to communicate with resources in VPC B.
14. **SQS**
    - The messages need to be processed asynchronously and out of order. Your application needs to ensure no messages
      are lost.
    - Amazon SQS provides a message queue service that enables asynchronous message processing. It supports out-of-order
      processing and ensures no messages are lost.
    - by default a msg visibility time 30 seconds, once it pooled by consumer.
    - if consumer has not pooled and deleted the msg from the SQS queue then the msg will be visible after 30 seconds.
    - a consumer could call the ChangeMessageVisibility API to get more time.
    - if visibility timeout is high and consumer crashes, then reprocessing will take place.
    - -SQS -standard Queue.
        - in this Duplicate entry on the queue is allowed
    - SQS -FIFO Queue.
        - in this kind of Queue we can keep orders of the msg send to the queue.
        - limited throughput: 300 msg/s without batching, 3000 msg/s with.
        - Exactly once send capability.(by removing duplicates).
        - Messages are processed in order by the consumer.
    - SQS - long pooling:
        - when a consumer request message from the queue it can optionally wait for the msg to arrive if there are none
          in the queue.
        - Long pooling decreases number of API calls while increasing the efficiency and latency of your application,
          the wait time can be 1 to 20 second. (preferable 20 second). long pooling can be enabled at queue level or at
          the API level using WaitTimeSeconds.
15. **SNS**

    - SNS is designed for fan out messaging and can deliver messages concurrently to a large number of subscribers
      including Lambda functions. This makes it an effective choice for fan out to improve event throughput.
    - Push once in SNS , receive in all SQS queues that are subscribed.Fully decoupled , no data loss.
16. **Kinesis**

    - it makes it easy to collect, process and analyze streaming data in real time.
    - ingest real time data as Application log, Metrics, Website clickstream.
    - Kinesis is of 4 types.
        - Kinesis Data Firehose. - load data stream into AWS data stores.
        - Kinesis Data Analytics. - analyze data stream with SQL or Apache Flink.
        - Kinesis Data stream. - capture, process, store data streams.
        - Kinesis video Streams. - capture process store data stream.

17. **ECS** (Elastic container service)
    - The application consists of a front-end container that communicates with a back-end container. The containers need
      to scale automatically based on demand. You want to deploy the containers on ECS and manage them as a single
      application.
    - The most efficient approach is to use a single ECS service with one task definition running both containers. This
      allows managing them together while still providing auto scaling based on demand.
18. **ECR** (Elastic container Registry)
    - Private Repository.
    - ECR Used to Store and manage Docker image on AWS.
    - Your company is migrating its monolithic application to microservices hosted in containers. The development team
      wants to use ECR to store and manage the container images. The images must be accessible to applications running
      in a VPC with private subnets only.
    - An ECR repository can be configured with a VPC endpoint policy to allow access only from the specified VPC and
      subnets. This meets the requirement to restrict access to the VPC with private subnets only.

19. **EKS** (Elastic Kubernates Service)
    - You are designing a Kubernetes environment on AWS that will run a variety of microservices applications. The
      applications have unpredictable traffic patterns and can scale up rapidly at times. You want to optimize cost
      efficiency while still providing high availability.
    - Deploy Amazon EKS with a mix of spot and on-demand instances in multiple Availability Zones.

20. **Amazon Fargate**
    - The application consists of a front-end and a back-end container. The front-end needs to scale automatically based
      on demand. The back-end needs to run consistently with no interruptions. You want to optimize cost.
    - Deploy both containers to a Fargate service configured with a load balancer and auto scaling.
21. **Amazon CloudFront**
    - it supports JavaScript, can handle million of request per second, max execution time <1 millisecond
    - Max Memory 2 MB , total PKG size 10 KB, free tier available 1/6th price of @Edge.

22. **Lambda@Edge**

    - it supports node.js , python , can handle 1000 of requests , triggers Viewer Request/Response and Origin
      Request/Response.
    - max execution time 5 -10 seconds , max memory 128 MB - 10 GB , total package size = 1 MB -50 MB.
23. **Amazon Lambda**

    - Execution:
        - Memory allocation: 128 MB – 10GB (1 MB increments)
        - Maximum execution time: 900 seconds (15 minutes)
        - Environment variables (4 KB)
        - Disk capacity in the “function container” (in /tmp): 512 MB to 10GB
        - Concurrency executions: 1000 (can be increased)
    - Deployment:
        - Lambda function deployment size (compressed .zip): 50 MB
        - Size of uncompressed deployment (code + dependencies): 250 MB
        - Can use the /tmp directory to load other files at startup
        - Size of environment variables: 4 KB.

24. **CloudWatch**
    - CloudWatch metrics and alarms monitor performance, not API calls.

25. **CloudTrail**
    - it provide governance ,audit and compliance for AWS account.
    - inaccurate resource provisioning
    - hitting service limits
    - Bursts of AWS IAM actions
    - Gaps in periodic maintenance activity
    - The security team has requested that all API calls made within your AWS account be logged for auditing and
      troubleshooting purposes.
    - Enable AWS CloudTrail trail logging across all regions and turn on log file validation.
26. **Amazon EventBridge**
    - EventBridge allows responding to events from various AWS services as well as custom applications. It meets the
      requirements of decoupled architecture, responding to events, and supporting AWS and custom sources.


99. **Others**.

    - **Amazon Polly**: text to audio , Pronunciation Lexicon, Speech synthesis Markup language (SSML)
    - **Amazon Translate**: provides real-time, high-quality, and affordable language translation
    - **Amazon Lex**: build conversational bots – chatbots
    - **Amazon Connect**: cloud contact center
    - **Amazon Comprehend** : natural language processing , natural language processing (NLP) service that uses machine
      learning to find meaning and insights in text.
    - **Amazon Comprehend Medical** - This service is specifically built for natural language processing for medical text.
      It can identify medication names, dosages, symptoms etc. from unstructured clinical text.
    - **Amazon SageMaker** - Fully managed service for developer, /data scientist for Build ML model.
    - **Amazon Forecast** - use ML to deliver accurate forcast.
    - **Amazon Kendra** - fully managed document search service, extract answer from document , it read files ,PDF from
      google Drive and s3….
    - Amazon Personalize - fully managed ML , to build apps with real time personalized recommendation. , also send sms
      and email ,
    - **Amazon textract** - help to extract text , analyze and data will be given .
    - **Amazon Rekognition** : face detection, labeling, celebrity recognition , remove pornographic content
    - **Amazon Transcribe** : audio to text (ex: subtitles) , remove any Personally Identifiable Information (PII) from the
      call before it's saved.
    - **Amazon GuardDuty** : uses ML to create intelligent Threat discovery to protect your AWS Account,anomaly detection,
      3rd party data, One click to enable (30 days trial), no need to install software.
    - **Amazon Inspector**
        - Automated Security Assessments and easy Reporting & integration with AWS Security Hub
        - Sends findings to Amazon Event Bridge.
        - Continuous scanning of the infrastructure.
    - **Amazon Macie**
        - Amazon Macie is a fully managed data security and data privacy service that uses machine learning and pattern
          matching to discover and protect your sensitive data in AWS.
        - Macie helps identify and alert you to sensitive data, such as personally identifiable information (PII).