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