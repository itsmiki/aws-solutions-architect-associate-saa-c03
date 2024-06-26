# Module 2 - Introduction

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Well-Architected Tool
-  Helps you review the state of your workloads and compares them to the latest AWS architectural best practices
-  Gives you access to knowledge and best practices used by AWS architects
-  Delivers an action plan with step-by-step guidance on how to build better workloads for the cloud
-  Provides a consistent process for you to review and measure your cloud architectures

## ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) Best Practises
1. Enable scalibility
2. Automate the environment
3. Treat resources as disposable (do things dynamically - don't run unnecessairy servers, use automatic IP adresses, automate deployment of resources)
4. Use loosely coupled components
5. Design services, not servers
6. Choose the right database solution
7. Avoid single points of failure
8. Optimize for cost
9. Use caching
10. Secure your entire infrastructure

## AWS Structure
- AWS Region (geographical area)
  - Availibility Zones (at least two in every Region)
    - Data centers (at least one in every Availibility Zone)

**AWS Region** - regions are isolated from one another, not every service is avaliable in certain regions. Connected with backbone network.

**AWS Availibility Zone** -  is designed as an independent failure zone, they are physically separated. They are interconnected with other Availability Zones in a Region using high-speed privatelinks. Systems can span multiple Availability Zones. Distributing applications across multiple Availability Zones enables them to remain resilient in most failure situations, including natural disasters or system failures.

**AWS Local Zone** - type of AWS infrastructure deployment that places AWS compute, storage, database, and other select services closer to large population, industry, and IT centers where no AWS Region exists today. Each AWS Local Zone location is an extension of an AWS Region.

**Edge Location / Regional Edge Caches** - to deliver content to end users with lower latency, Amazon CloudFront uses a global network that includes over 200 Points of Presence.

# Module 3 - Storage Layer

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon S3
- Object storage service
- Stores unlimited amounts of unstructured data
- Data is stored as objects in a bucket that you define
- Maximum size of single object - 5TB
- Objects have REST-accessible globally unique URL
- Objects have key, version ID, value (content that is stored), metadata, subresources
- Durability - 11 9s
- Objects in S3 Bucket are private by deafault
- Support for CORS
- Amazon S3 is strongly consistent for all new and existing objects in all Regions
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green)
  - Store and distribute web content and media
  - Host static website
  - Data store for computation and analytics
  - Back up and archive critical data

### Security
- Using Amazon S3 Block Public Access. These settings override any other policies or object permissions.
- Writing AWS Identity and Access Management (IAM) policies that specify the users or roles that can access specific buckets and objects.
- Writing bucket policies that define access to specific buckets or objects. This option is typically used when the user or system cannot authenticate by using IAM.
- Creating S3 Access Points. Access points are unique hostnames that enforce distinct permissions and network controls for requests that are made through it. 
- Setting access control lists (ACLs) on your buckets and objects.
- AWS Trusted Advisor provides a bucket permission check feature.

#### Encryption
- Server-side encryption - set the default encryption option on a bucket.
- Client-side encryption - encrypt the data on the client side before you upload it to Amazon S3.


### ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) Versioning
Versioning is a method of keeping multiple variants of an object in the same bucket. You can use versioning to preserve, retrieve, and restore every version of every object stored in an S3 bucket. Buckets can be in one of three states: unversioned (the default), versioning-enabled, or versioning-suspended. After you enable versioning for a bucket, you can never change it to an unversionedstate. You can, however, suspend versioning on that bucket.

### Storage Classes
1. S3 Standard - offers high durability, availability, and performant object storage for frequently accessed data. Because it delivers low latency and high throughput, S3 Standard is appropriate for a wide variety of use cases.
2. S3 Standard-Infrequent Access (S3 Standard-IA) - offers all the benefits of Amazon S3 Standard, but it runs on a different cost model to store infrequently accessed data. There is a 30-day minimum storage fee applied to any data placed in it, and also a higher cost to retrieve data from S3 Standard-IA than from S3 Standard storage.
3. S3 One Zone-IA - stores data in a single Availability Zone. It is ideal for customers who want a lower-cost option and who do not need the availability and resilience of S3 Standard or S3 Standard-IA. It’s a good choice for storing secondary backup copies.

### ![Static Badge](https://img.shields.io/badge/Service-red) Amazon S3 Glacier
Secure, durable, and low-cost storage class for data archiving. To keep costs low, but suitable for different needs, you have three options for retrieving data, with varying access times and cost:
- Expedited retrievals are typically made available within 1–5 minutes
- Standard retrievals typically complete within 3–5 hours
- Bulk retrievals typically complete within 5–12 hours

Amazon S3 Glacier Deep Archive is the lowest-cost storage class for Amazon S3.

### Lifecycle policy
A lifecycle configurationis a set of rules that define actions that Amazon S3 applies to a group of objects. After an S3 lifecyclepolicy is set, your data will automatically transfer to a different storage class without any changes to your application.

### Upload to S3
- Multipart upload
  - Improved throughput
  - Quick recovery from any network issues
  - Ability to pause and resume object uploads
  - Ability to begin an upload before you know the final object size
  - Ability to upload large objects
- Transfer Acceleration - enables fast and easy data transfer into an S3 bucket by taking advantage of Amazon CloudFront and AWS edge locations. This data is then routed to Amazon S3 over an optimized network path.

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Snowball
AWS Snowball is a petabyte-scale data transport option that doesn’t require you to write any code or purchase any hardware to transfer your data. Snowball appliance will be shipped to you. Attach the appliance to your local network and transfer files directly onto it. 

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Snowmobile
AWS Snowmobile is an even larger data transfer option that operates in exabyte scale. An exabyte is 1 million terabytes or 1 billion gigabytes.

## Choosing Region
- consider data privacy laws and your regulatory compliance requirements
- choose a region that provides low latency for the users
- different service and features availibility
- costs vary by region

# Module 4 - Computer Layer

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon EC2
- provides virtual machines (servers)
- provisions servers in minutes
- can automatically scale capacity up or down as you need
- you pay only for the capacity you use
- possible to choose different CPU and memory capacity
- storage options:
  - instance store (deleted when instance is stopped)
    - for temprorary storage
    - ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) caches, buffers, scratch data 
  - ![Static Badge](https://img.shields.io/badge/Service-red) **Amazon Elastic Block Storage (Amazon EBS)** - isn't deleted even if instance is stopped
    - persistent storage, can be attached to any instance in the same vailibility Zone
    - SSD-backed or HDD-backed can be chosen
    - instances can be EBS optimized - an EBS-optimized instance has a dedicated network connection between itself and an EBS volume
    - ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) stand-alone database, general application data storage
  - ![Static Badge](https://img.shields.io/badge/Service-red) **Amazon Elastic File System (Amazon EFS)** (possible access from multiple instances)
    - for Linux, can be used with NFS, scales automatically up or down
    - ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) home directories, file system for enterprise applications, database backups, media workflows, big data analytics, web serving and content management
  - ![Static Badge](https://img.shields.io/badge/Service-red) **Amazon FSxfor Windows File Server** (possible access from multiple instances)
    - simmilar to EFS, but for Windows   
- **User data** enables you to provide a script that can be used to initialize it. 
 
### Use cases
- complete control over resources is needed
- optimizing costs - on-demand instances, reserved instances, spot instances, saving plans
- ability to run any type of workload

### AMI
AMI is only available in certain region.
AMI includes:
- template for root volume
- launch permissions
- block device mappings (specifies storage volumes attached to EC2)

AMI with instance store VS. AMI with EBS volume:
- EBS boots faster
- EBS max size 16TiB, IS 10 GiB
- EBS can be stopped, IS only reboot/terminate
- EBS instance type can be changed while stopped, IS can't be changed
- different costs

### AMI vs User data
- Full AMI - The applicationsand all dependencies are pre-installed, which shortens boot times but increases build times. Full AMIs typically have a shorter lifespan. Consider your rollback strategy.
- Hybrid (partially configured) AMIs - Only prerequisite software and utilities are pre-installed, which leads to a longer shelf life for the AMI. This approach provides a balance between boot speed and build time. Rollbacks become easier.
- OS-only AMI - This approach is fully configurable and upgradeable over time and shortens build times. However, it makes your EC2 instances slow to boot because all required installations and configurations must be run at boot time.

### EC2 Placement options
- Cluster - Packs instances close together inside an Availability Zone. This strategy enables workloads to achieve low-latency network performance.
- Partition - Spreads your instances across logical partitions so that groups of instances in one partition do not share the underlying hardware with groups of instances in different partitions. (Single Availibility Zone)
- Spread - Strictly places a small group of instances across distinct underlying hardware to reduce correlated failures. (Different Avalilbility Zones)

## ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) EC2 pricing options
1. On demand instances - pay for computing power and capacity, by second or hour, no long term commitment
2. Reserved Instances - 1 or 3 year commitment with massive discount.
    - ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) good choice if you have predictable or steady-state compute needs.
4. Savings Plan - same discounts as in Reserved with more flexibility
5. Spot Instances - instances are used when there are spare ones. There is 2 minutes notification before instance will be stopped.
    - ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) recommended for fault-tolerant, flexible (non-time-critical), stateless workloads.
7. Dedicated Hosts - are physical servers with instance capacity that is dedicated to your use. They are physically isolated at the level of the host hardware from instances that belong to other AWS accounts.
    - ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) good choice when you have licensing restrictions for the software that you want to run on Amazon EC2, or when you have specific compliance or regulatory requirements that preclude you from using other deployment options.

## ![Static Badge](https://img.shields.io/badge/Service-red) EC2 Image Builder
Service that simplifies the creation, maintenance, validation, sharing, and deployment of images. It provides a simple graphical interface to produce AMIs for use on AWS and to generate VM images for use on premises. It can also validate and test images and it provides version control.

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Compute Optimizer
Service that recommends optimal instance types, analyzes workloads and labels instances accordingly.

# Module 5 - Database Layer

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon RDS
Fully managed database service.
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) Application that:
  - have complex data
  - need to combine and join datasets
  - need enforced syntax rules
- database engines used: MS SQL Server, Oracle, MySQL, PostgreSQL, Amazon Aurora, MariaDB.
- possible to create *Read Replicas* (MySQL, MariaDB, PostgreSQL, Oracle)- updates are asynchronously copied to read replica, you can route read queries to it, so main database is offloaded.

## Multi-AZ deployment
- high avalilbility
- failover to standby occurs automatically
- enhanced durability

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon Aurora
Fully managed MySQL and PostgreSQL compatible, relational database.
- 5 times faster than MySQL, three times faster than PostgreSQL at 1/10th cost.
- automatically scales up to 64TB per database instance
- up to 15 read replicas
- continuous backup to S3
- possible replication across 3 AZ
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) often used for online transaction processing (OLTP). OLTP systems must be able to handle a high volume of concurrent users, and be able to run insert and update requests.

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon Redshift
Amazon Redshift is a different AWS relational database offering. It does not run on Amazon RDS. 
- provides a petabyte-scale data warehouse and data lake analytics.
- can access data directly in Amazon S3
- stores very large datasets
- provides consistently fast performance, even with thousands of concurrent queries
- you can query open file formats such as Parquet, JSON, Avro, CSV
- doesn't scale automatically and doesn't support read replicas
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) typically used to store frequently accessed, highly structured data

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon DynamoDB
DynamoBD is a non-relational database.
- It offers consistent, single-digit millisecond response times
- You can build applications with virtually unlimited throughput (more than 20 million requests per secon)
- Serverless
- It supports ACID transactions
- It encrypts all data at rest by default
- Multi-Region replication (global tables) is available 
- It provides fine-grained identity and access control
- You can perform full backups of data with no performance impact
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) Applications that:
  - have simple high-volume data 
  - must scale quickly
  - don't need complex joints (NoSQL)
  - require ultra high throughput and low latency
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) Examples:
  - leaderboard in game (constantly updated with highscores)
  - shopping cart functionality
- Consistency options:
  -  Eventually consistent (consistency within 1 second, data may be 1 second old when read) - default
  -  Strong consistency (response reflects the updates from all previous write operations that were successful) - optional 

## Database security 

### RDS
- run your RDS instances in a virtual private cloud (VPC)
- Use AWS Identity and Access Management (IAM) policies for authentication and to control access.0
- Configure security groups to limit connections.
- Use SSL connections to ensure that all communication to and from your database is secured
- Enable event notifications on important events that can occur on your RDS instance
- Use Amazon RDS encryption to encrypt your data and database snapshots

### DynamoDB
- use **IAM roles** to secure authentication, and use **IAM policies** to define access permissions
- encrypt data as close as possible to its origin so that your data is protected throughout its lifecycle
- DynamoDB provides certain security features by default: protects user data stored at rest and also data in transit between on-premises clients and DynamoDB, and between DynamoDB and other AWS resources within the same AWS Region

## Migrating data into AWS databases

### ![Static Badge](https://img.shields.io/badge/Service-red) AWS Database Migration Service (AWS DMS)
AWS DMS supports migration between the most widely used databases.
- supports both homogenous (same engine) migrations and heterogeneous (different engines) migrations
- performs one-time migration as well as continuous data replication
- can be used with AWS Snowball Edge to transfer large databases without using Internet

# Module 6 - Creating a networking Environment

## ![Static Badge](https://img.shields.io/badge/Service-red) Amazon VPC (Virtual Private Cloud)
A service that enables you to provision a logically isolated section of the AWS Cloud where you can launch your AWS resources. You can select your own IP address range, create subnets, and configure route tables and network gateways.
- VPC belongs to a single Region, but it can host resources deployed in every Availibility Zone from this Region
- When you create a VPC, you provide the set of private IP addresses that you want instances in your VPC to use. You can assign block sizes of between /28 (16 IP addresses) and /16 (65,536 IP addresses).
- VPC supports IPv4 and IPv6 addressing
- VPC can operate in dual-stack mode: your resources can communicate over IPv4, or IPv6, or both. Pv4 and IPv6 addresses are independent of each other, routing must be configured independently.

### Dividing VPC (subnets)
- Subnet is a segment of a VPC’s IP address range where you can allocate a group of resource.
- Subnets are not isolation boundaries around your application, they are only containers for routing policies.
- Subnet CIDR blocks cannot overlap.
- Each subnet must reside entirely within one Availability Zone.
- AWS reserves the first four IP addresses and the last IP address in each subnet CIDR block:
  - 10.0.0.0: Network address
  - 10.0.0.1: VPC local router
  - 10.0.0.2: Domain Name System (DNS) resolution
  - 10.0.0.3: Future use
  - 10.0.0.255: Network broadcast address 

### ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) VPC Best practises
- Create one subnet per available Availability Zone for each group of hosts that have unique routing requirements.
- Divide your VPC network range evenly across all available Availability Zones in a Region.
- Do not allocate all network addresses at once. Instead, ensure that you reserve some address space for future use.
- Size your VPC CIDR and subnets to support significant growth for the expected workloads.
- Ensure that your VPC network range (CIDR block) does not overlap with your organization’s other private network ranges
- ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) When you design and create your network environment, there are a limited number of use cases where a single VPC environment might be appropriate:
  - Small, single applications managed by a small team
  - High performance computing (HPC) environments (such as physics simulations) - a single VPC environment has lower latency than one spread across multiple VPCs
  - Identity management environments—a single VPC might provide best security.

### Multiple VPCs & Multiple accounts
**Multiple VPCs** -  best suited for a single team or organization that maintains full control over the provisioning and management of all resources in each application environment.

**Multiple accounts** - best suited for enterprise customers or organizations that deploy applications managed across multiple teams.

Be aware of Amazon VPC quotas. The default quota is 5 VPCs per Region. However, you can request an increase for this quota.

### VPC elements and configuration
**Public subnet** - to make a subnet public, you must first create an internet gateway and attach it to your VPC. An **internet gateway** serves two purposes. First, it provides a target in your VPC route tables for internet-routable traffic. Second, the internet gateway performs network address translation (NAT) for instances that were assigned public IPv4 addresses.

Creating a public subnet:
1. Create an internet gateway and attach it to the VPC.
2. Add a route to your subnet’s route table that directs internet-bound traffic to the internet gateway.
3. Make sure that your instances have public IP or Elastic IP addresses.
4. Make sure that your security groups and network ACLs allow relevant traffic to flow.

**Elastic IP** - a static and public IPv4 address. You can associate an Elastic IP address with any instance or elastic network interface for any VPC in your account. Elastic IP address, you can mask the failure of an instance by rapidly remapping the address to another instance in your VPC. Associating the Elastic IP address with the network interface has an advantage over associating it directly with the instance. You can move all of the attributes of the network interface from one instance to another in a single step.

**Private subnet** - **NAT gateway** enables instances in a private subnet to connect to the internet or other AWS services, but prevents the internet from initiating a connection with those instances.

Connecting private subnet to the internet:
1. Create NAT gateway and attach it to PUBLIC subnet.
2. Create an Elastic IP address and associate it with NAT Gateway.
3. Update or create a route table associated with PRIVATE subnet to point internet-bound traffic to the NAT gateway.

#### ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) Subnets
- Private Subnets - Data Store Instances, Batch-processing instances, Backend instances, Web Application Instances (Load Balancer in Public Subnet)
- Public Subnet - Web Application Instances (In some environments, you must attach web application instances to Elastic IP addresses directly (though you can also attach an Elastic IP address to a load balancer). In those cases, web application instances must be in a public subnet.)

### Bastion Host
- A bastion host is a server that provides access to a private network from an external network, such as the internet.
- Typically runs on an EC2 instance in a public subnet of your VPC.
- Instances in the private subnet are in a security group that allows SSH access from the security group attached to the bastion host. Bastion host users connect to the bastion host so they can connect to instances in private subnet.
- The bastion host should be the only source of SSH traffic to your Linux instances.

## Security 

### Security Groups 
Security group is a stateful firewall that controls inbound and outbound traffic. Stateful means that return traffic is automatically allowed, regardless of any rules.
- Acts at instance level or network interface
- Traffic can be restricted by any internet protocol, service port, and source or destination IP address (individual IP address or CIDR block).
- By default security group allows all outbound traffic and no inbound traffic.
- It is only possible to add *allow* rules, everything else is denied by default.
- ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) Create security group for every tier in the application, create inbound rules only form certain security groups so traffic can go only one way. The security groups act as firewalls to prevent a security breach in one tier from automatically providing subnet-wide access of all resources to the compromised client.

### Network ACLs
Stateless firewall that requires explicit rules for inbound and outbound traffic.
- Acts at subnet level.
- By default allows all inbound and outbound traffic.
- Optional layer of security, cts as a firewall for controlling traffic in and out of one or more subnets.
- You can associate a network ACL with multiple subnets. However, a subnet can be associated with only one network ACL at a time.  If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL. Each subnet in your VPC must be associated with a network ACL.
- By default, each custom network ACL denies all inbound and outbound traffic until you add rules.

### ![Static Badge](https://img.shields.io/badge/Best%20Practise-blue) Best practise
As a best practice, you should secure your infrastructure with multiple layers of defense.
- Define both security groups and network ACLs to further protect your infrastructure at the infrastructure and subnet levels, respectively.
- When you implement both network ACLs and security groups as a defense-in-depth way of controlling traffic, a mistake in the configuration of one of these controls will not expose the host to unwanted traffic.

# Module 7 - Connecting Networks

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Site-to-Site VPN
- Used to securely connect your on-premises network or branch office site to your VPC.
- Each connection uses IPSec protocol in order to create encrypted tunnels between locations.
- Can be connected to Virtual Private Gateway or ![Static Badge](https://img.shields.io/badge/Service-red) AWS Transit Gateway.
- Provides two VPN tunnels across multiple Availability Zones that you can use simultaneously for high availability. You can stream primary traffic through the first tunnel and use the second tunnel for redundancy. If one tunnel goes down, traffic will still get delivered to your VPC.
- Charged for each VPN connection-hour.

When you create a Site-to-Site VPN connection, you must specify the type of routing that you plan to use and you must update the route table for your subnet.
- If your device supports it, use BGP, specify dynamic routing when configuring Site-to-Site VPN. Dynamic routing supports up to 100 propagated routes per route table.
- if your device does not support BGP, use static routing. It requires that you specify the routes (IP prefixes) for your network that should be communicated to the virtual private gateway. Static routing supports 50 non-propagated routes per route table by default, up to a maximum of 1,000 non-propagated routes.
-  ![Static Badge](https://img.shields.io/badge/Use%20Cases-green) Use BGP-capable devices because the BGP protocol offers robust liveness detection checks that can assist failover to the second VPN tunnel if the first tunnel goes down.

### Connecting multiple VPNs
-  To maintain high availability of your customer gateway, you can set up redundant customer gateway devices. Each device will advertise the same prefix fe. 0.0.0.0/0 to the Virtual Private Gateway (BGP is used for routing). If one gateway fails VPG will direct traffic the other customer gateway.
-  It is possible to establish multiple customer gateway devices to one virtual private gateway using ![Static Badge](https://img.shields.io/badge/Service-red). It can be used to provide redundancy and failover.
- AWS VPN CloudHub operates on a hub-and-spoke model to enable multiple sites to access your VPC or to securely access each other. Each customer gateway device needs to advertise site-specific prefix such as 10.0.0.0/24, 10.0.1.0/24.

## ![Static Badge](https://img.shields.io/badge/Service-red) AWS Direct Connect






















