# Legend
- [[#Types of Storage]]
- [[#Storage Options]]
- [[#Section 1 Elastic Block Store]]
- [[#Section 2 S3]]
- [[#Section 3 Elastic File System]]
- [[#Section 4 S3 Glacier]]


# Types of Storage
- Instance/Ephemeral -> Temporary storage added to EC2
- Amazon EBS -> Persistent, mountable storage for EC2s. Only same availability zone, 1 : 1 
- Amazon EFS -> Shared file system for multiple EC2 Many : 1
- s3 -> Persistent object storage 
- S3 Glacier -> Cold storage for data that is not accessed frequently

# Storage Options
Two types of storage available
- Block
- Object

>[!note] High Level Overview
>![](https://i.imgur.com/B19xk0m.png)


Block storage:
- Only change a piece of the file 
- Faster and less bandwidth; However more expensive 

Object:
- Entire file must be updated
- Slower but cheaper

---

# Section 1 Elastic Block Store

Go to legend: [[#Legend]]
Go to Sections:
- [[#Section 2 S3]]
- [[#Section 3 Elastic File System]]
- [[#Section 4 S3 Glacier]]

Go to internal Sections:
- [[#What is EBS]]
- [[#Volume types]]
- [[#Pricing]]

## What is EBS

A Non-volatile block storage volume used with EC2 [[Compute]] instances
- High availability and durability
- Low-latency performance
- Scalable

Features of EBS:
- Block level storage
- Directly attached to EC2
- Data is retained after EC2 shuts down
- Volumes Automatically replicated within AZ
- Backed up through snapshots which can be saved in S3
- Encryption at transit for no additional cost
- Easily change type file system or storage size without stopping instances

Snapshots:
- First is called baseline snapshot
- Afterwards capture differences 
- Can share to others or copy to different regions

Uses of EBS:
- Boot volumes for EC2
- Data storage for file system
- Database host
- Enterprise applications

## Volume types

>[!note] Table about volume types
>![](https://i.imgur.com/DpUsRNe.png)
>- Only SSDs can be used as boot volumes for EC2 Instance

### Volume type use cases

>[!note] Table about use cases
>![](https://i.imgur.com/sAt1lNi.png)

## Pricing
### Volumes
- Persistent independently from instance (means if instance is gone it will still exist)
- Charged by amount that is provisioned in GB per month until storage release 

### IOPS
- I/O is included in price for General Purpose SSD volumes
- For magnetic volumes, I/O is charged by number of request you make on that volume
- With Provisioned IOPS SSD volumes, charged by amount you provision in IOPS

### Snapshots (Optional)
- There is added cost per GB-month for data stored  

### Data transfer
- Inbound data is free
- Snapshot copying will be charged for data transferred across regions

---

# Section 2 S3

Go to legend: [[#Legend]]
Go to Sections:
- [[#Section 1 Elastic Block Store]]
- [[#Section 3 Elastic File System]]
- [[#Section 4 S3 Glacier]]

Go to internal sections:
- [[#What is S3]]
- [[#Storage classes]]
- [[#Bucket URLs]]
- [[#Designed for Seamless Scaling]]
- [[#Common use cases of buckets]]
- [[#S3 pricing in general]]
- [[#Factors of S3 pricing]]

## What is S3

A cloud managed storage solution
- Durable
- High capacity

Features:
- Data is stored as objects
- Object can be any data file
- A object can be maximum 5TB in size
- Globally unique names
- No need to manage infrastructure

How data is handled:
- Data is stored redundantly across multiple facilities and devices in the specified region
- Design for 11 9s durability (99.999.. of not failing)

Accessing S3:
- Managed console
- CLI
- SDK
- Rest-based endpoints
- HTTP, HTTPS
- URL-based access
- VPC endpoints 

Additional features:
- Per object ACL
- Optional encryption of data at rest or transit
- Event notifications whenever a specified one occurs (trigger Lambda functions)
- S3 Analytics for optimal lifecycle and transition less frequently accessed data to S3 Standard -IA
- You can configure a storage class analysis policy to monitor an entire bucket, a prefix, or an object tag.
- Bucket access controlled

## Storage classes

### S3 standard
- High performance object storage
- Used for frequently accessed data 
- Low latency and high throughput

### S3 Intelligent-Tiering
- Automatically moves data to most cost-effective access tier 
- Small monthly fee per object
- No retrieval fees and when moving between access tier
- Long term data with unpredictable access 

### S3 Standard-Infrequent Access
- Data accessed less frequently
- Rapid access when needed
- High throughput and low latency
- Low per-GB storage price and per-GB retrieval fee
- Long term storage, backups or disaster recovery

### S3 One Zone-Infrequent Access
- Similar to Standard-Infrequent
- Stored in 1 AZ compared to a minimum of 3 AZ
- Even less cost 
- Do not need availability of S3 Standard-IA
- Storying secondary backup copies or re-creatable data
- Data can be replicated via S3 cross-region replication 

### S3 Glacier 
- Low cost for data archival
- 3 Different retrieval options to keep costs low
- Can use lifecycle policies to transfer into here
- Might be cheaper than on-premise

### S3 Glacier Deep Archive
- Lowest-cost storage
- Data accessed one or twice in a year
- Replicated across at least 3 geographically dispersed AZ and can be restored within 12 hours
- Good alternative to magnetic tape 
- Good for industries that store datasets for 7-10 years or more for compliance

## Bucket URLs 
Buckets
- Contains your data
- Acts as a prefix for a set of files
- Uniquely named across all of S3 globally

Uploading data
- Create bucket in region
- Upload object 

>[!note] Two types of URLs
>![](https://i.imgur.com/GhTOFUe.png)

## Data is redundantly stored in the region
- Creating buckets and storage of data in them are stored across multiple AZ within the region

>[!note] Image on replication
>![](https://i.imgur.com/qgDPfMW.png)

## Designed for Seamless Scaling
- S3 automatically manages stored in bucket when data grows
- Scales to handle high volume requests, only billed for what you use

## Common use cases of buckets
- Store application assets
- Static web hosting
- Backup and disaster recovery
- Staging area for big data

## S3 pricing in general
Pay for you what use
- GBs per month
- Transfer OUT to other regions
- PUT, COPY, POST, LIST, and GET requests

Do not need to for pay
- Transfers IN to S3
- Transfers OUT from S3 to CloudFront or EC2 in same region

## Factors of S3 pricing

Storage class type
- Each class has different rates
- Standard S3 -> 11 9s durability and 4 9s of availability
- S3 S-IA -> 11 9s durability and 3 9s of availability (cheaper)

Amount of storage
- Number and size of objects stored in bucket

Requests
- Number and type of request 
- `GET, PUT, COPY` all have different rates
- GET needs READ access
- PUT needs WRITE access
- COPY needs both 

Data transfer
- Amount of data being transferred out of S3 Region

---

# Section 3 Elastic File System

Go to legend: [[#Legend]]
Go to Sections:
- [[#Section 1 Elastic Block Store]]
- [[#Section 2 S3]]
- [[#Section 4 S3 Glacier]]

Go to Internal Sections:
- [[#What is EFS?]]
- [[#EFS Architecture]]
- [[#EFS Implementation]]
- [[#EFS Resources]]

## What is EFS?
It is a fully managed service for easy setting up and scaling file storage 

Features:
- Petabyte scaling 
- Multiple EC2's can access a EFS at a time 
- No minimum fee or setup costs, pay for the storage you use
- Supports NFS 4.0 and 4.1 
- Compatible with all Linux-based AMIs for EC2
- Encryption optional
- Low latency

Used cases:
- Big data analytics
- Media processing workflows
- Home directories

## EFS Architecture

>[!note] High level Overview of mounting an EFS to VPC
>![](https://i.imgur.com/NTD54MF.png)
>- 1 mount target per AZ and only can be in 1 subnet
>- However can just access mount target from other AZ but not recommended

Mountings:
- Mount EFS directly onto EC2 Instance with Linux AMI
- Mount EFS to entire VPC 

## EFS Implementation
Some steps for implementing a EFS
1. Creating EC2 resource and launch it   (LINUX AMI)
2. Create EFS file system
3. Create mount targets in appropriate subnets
4. Connect EC2 instance to mount targets
5. Verify resources and protection of AWS account

## EFS Resources

In EFS a filesystem is a primary resource, each file system has properties such as:
- ID
- Creation token
- Creation time
- File system size in bytes
- Number of mount targets that are created for file system
- File system state

Primary resources can be configured with supporting resources like
- Mount target
- Tags

### Mount Target
Allows you to access file system for resources in VPC

Properties of mount target
- ID
- Subnet ID for subnet it was created in
- File system ID for the file system where it was created
- IP address where file system can be mounted
- Mount target set 

We can use IP address or DNS name in mount command

### Tags
- Helps us organize file systems in EFS
- Can assign meta data to each file system
- key : value pair

---

# Section 4 S3 Glacier

Go to legend: [[#Legend]]
Go to Sections:
- [[#Section 1 Elastic Block Store]]
- [[#Section 2 S3]]
- [[#Section 3 Elastic File System]]

Go to Internal Sections:
- [[#What is Glacier?]]
- [[#Lifecycle policies]]
- [[#Comparison Standard to Glacier]]
- [[#Server-side Encryption]]
- [[#Security with S3 Glacier]]

## What is Glacier?

>[!note] Quick high level overview
>![](https://i.imgur.com/VaoE0yo.png)


A data archiving service designed for security, durability, and an extremely low cost
- 11 9s durability
- Encryption of data at rest or in transit
- Unique feature, Vault Lock, enforces compliance through a policy

Caveats:
- Cannot retrieve data immediately when you want
- Will take several hours to retrieve 

Three key terms:
- Archive
	- Each object you store is a base unit of storage, each one can have their own unique ID and description
- Vault
	- A container for storing archives, it has a vault name, and region
- Vault access Policy
	- Accession permissions and what operations they can do. Vault lock policy to make sure it cannot be altered. Each vault can have 1 of each

Three options for retrieving data:
- Expedited
	- Retrievals made available within 1-5 min (highest cost)
- Standard
	- Retrievals are complete within 3-5 hours
- Bulk
	- Retrievals take 5-12 hours (lowest cost)

Use cases:
- Media asset archiving
- Healthcare information archiving
- Digital preservation

How to access
- Management console (limited to certain instructions)
- REST APIs, AWS Java or .NET SDKs, or CLI (all operations)

## Lifecycle policies

>[!note] High level overview
>![](https://i.imgur.com/xYrWD8f.png)

Helps automate lifecycle of data stored in S3 
- Reduces overall cost as you pay less for data that becomes less important
- Can be per object or per bucket 

## Comparison Standard to Glacier

>[!note] Table that outlines comparisons
>![](https://i.imgur.com/czzYb5N.png)
>- Faster access means higher cost/gb per month
>- Retrieval is higher in glacier as it is designed for less-frequent access to data

## Server-side Encryption
Both S3's are able to transfer data over HTTPS

S3 standard
- Application must enable server-side encryption (protecting data at rest)

S3 Glacier
- Data is encrypted by default

## Ways to encrypt data in S3
1. Using S3-managed encryption keys (SSE-S3)
	- Multi-factor encryption for each object with a unique key
	- Key is also encrypted using a main key which is regularly rotate
2. Using Customer-provided Encryption Keys (SSE-C)
	- Can utilize own keys
	- Users include encryption key as part of request and S3 manages the rest
3. AWS Key Management Service (KMS)
	- Use Customer Encryption Keys to encrypt objects
	- Accessing KMS, through Through “Encryption Keys” section in IAM console OR through KMS API
	- Using the API we can centrally create encryption keys and policies to control and audit key usage

## Security with S3 Glacier
- Enable and control access to Glacier using IAM and its policies
- Data security is default and encrypts with AES-256
- Glacier manages user keys for users 