
- A General Purpose SSD EBS volume is limited to 16,000 IOPS for each volume.
- A Provisioned IOPS SSD EBS volume provides up to 64,000 IOPS for each volume.
- A Throughput Optimized HDD EBS volume is an HDD-backed storage device that is limited to 500 IOPS for each volume.
- A Cold HDD volume provides low-cost magnetic storage that defines performance in terms of throughput rather than IOPS. Cold HDD volumes are a good fit for large, sequential cold-data workloads.


- A **customer gateway** is required for the VPN connection to be established. A customer gateway device is set up and **configured in the customer's data center**.
- A **virtual private gateway is attached to a VPC to create a site-to-site VPN connection to AWS**. You can accept private encrypted network traffic from an on-premises data center into your VPC without the need to traverse the open public internet.


- An IAM role is an IAM entity that is assumable by an IAM user. An IAM role has permissions policies that define what the entity can and cannot do. However, an IAM role does not control access to an application.
- Amazon Cognito provides **authentication, authorization, and user management** for your web and mobile apps. Users can sign in directly with a user name and password, or through a trusted third party.
- You can use **AWS STS** to create and provide trusted users with **temporary security credentials** that can **control** access to your **AWS resources**. However, AWS STS **does not control access to an application**.


- **Storage optimized instances** are designed for workloads that require high, sequential read and write access to very large datasets on local storage. These instances are optimized to provide applications with **tens of thousands of low-latency, random IOPS.** The instance **store has no additional cost**.
  - example  400 GB of storage for temporary data and required approximately 40,000 

- A private subnet is one component to use to secure the database tier. Internet traffic is not routed to a private subnet. When you place DB instances in a private subnet, you add a layer of security.
- Security groups can restrict access to the DB instances. Security groups provide access from only the application tier on only a specific port.
