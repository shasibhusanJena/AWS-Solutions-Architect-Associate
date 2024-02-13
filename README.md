# AWS-Solutions-Architect-Associate
it has vary specific notes on the use cases of AWS components and helps in understanding each of them with short descriiption


1.  AWS Transit Gateway
    -   Create a route table for the transit gateway and add a route that allows traffic between VPC A and VPC B's CIDR blocks. Associate this route table with VPC A and VPC B attachments.
2.  AWS Global Accelerator
    -   You are designing the architecture for a global SaaS application that will be deployed in the AWS cloud across multiple regions. The application needs to provide fast, reliable access for users across the globe. You want to improve performance and availability for users by routing traffic through the AWS global network.
3.  Cross-region replication 
    -   copies objects between S3 buckets in different regions
4.  CloudFront
    -   used for caching content at the edge
5.  Snowball
    -   used for physical data transport
6. Transfer Acceleration
    -   a media company that frequently transfers large video files between an on-premises data center and Amazon S3. The company would like to accelerate these transfers to improve efficiency.
    -   uses the AWS global network and edge locations to accelerate uploads to and downloads from an S3 bucket over long distances. This would help accelerate transfers between the on-premises data center and S3
7.  Virtual private gateway. 
    -   Explanation: A virtual private gateway enables communication between a VPC and an on-premises network over an IPsec VPN tunnel. It supports overlapping IP address ranges and meets the requirements stated in the scenario.
8.  NAT gateway
    -   Instances in the private subnet can access the internet by using a NAT gateway.
    -   The NAT gateway will perform source NAT and translate the private IP to a public IP when traffic goes to the internet

9.  Internet gateway
    -   Attaching an internet gateway to the VPC allows resources in the VPC such as instances in private subnets to connect to the internet by routing their traffic through a NAT gateway. This allows private resources internet access while keeping them private.

10. VPC peering
    -   requirement : You have two VPCs, VPC A (10.0.0.0/16) in us-east-1 and VPC B (10.1.0.0/16) in us-west-2. You need to allow resources in VPC A to communicate with resources in VPC B.
    -   VPC peering allows resources in two VPCs, even in different regions, to communicate with each other as if they are within the same network. A VPC peering connection needs to be created between the VPCs and routes configured to route traffic between them. This allows resources in VPC A to communicate with resources in VPC B.
11. SQS
    - The messages need to be processed asynchronously and out of order. Your application needs to ensure no messages are lost.
    - Amazon SQS provides a message queue service that enables asynchronous message processing. It supports out-of-order processing and ensures no messages are lost.
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
        - when a consumer request message from the queue it can optionally wait for the msg to arrive if there are none in the queue.
        - Long pooling decreases number of API calls while increasing the efficiency and latency of your application, the wait time can be 1 to 20 second. (preferable 20 second). long pooling can be enabled at queue level or at the API level using WaitTimeSeconds.