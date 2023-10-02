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

### Use cases
- Store and distribute web content and media
- Host static website
- Data store for computation and analytics
- Back up and archive critical data

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
