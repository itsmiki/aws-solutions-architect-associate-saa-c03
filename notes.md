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






