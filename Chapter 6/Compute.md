# Section 1 Compute Services
## AWS Compute Services
AWS offers many compute services
- Elastic Compute Cloud **EC2** -> Resizable virtual machines
- EC2 Auto Scaling -> Allows you to define conditions to automatically launch or terminate EC2 instances
- Elastic Container Register **ECR** -> Store and retrieve Docker Images
- Elastic Container Service **ECS** -> Container orchestration service that supports Docker
- VMware Cloud -> Provision a hybrid cloud without custom hardware
- Elastic Beanstalk -> simple way to run web applications
- Lambda -> server less compute solution, pay for compute time used 
- Elastic Kubernetes Service **EKS** -> Run managed Kubernetes on AWS
- Lightsail -> Simple service for building an application or website
- Batch -> Tool for running batch jobs at any scale
- Fargate -> Run containers that reduce the need to manage servers or clusters
- Outposts -> Run select AWS services on on-premise data center
- Serverless Application Repository -> Discover, deploy, and publish serverless applications

The optimal compute service or services that you use will depend on your use case, some aspects to consider:

- What is your application design?
- What are your usage patterns?
- Which configuration settings will you want to manage?
# Section 2 Amazon EC2
Provides virtual machines to host applications
- Secure, resizable compute capacity 
- Supports a wide variety of uses like web servers, game servers etc.
## EC2 Overview
EC2 stands for Elastic Compute Cloud
- Provides virtual machines in the cloud 
- Gives full admin control 
- Launch any number of instances of any size into any availability zone from a AMI
- Traffic can be controlled sing security groups

Hosts OS:
- OS that is directly installed on the hardware that hosts 1 or more virtual machines

Guest OS:
- The os that runs on the virtual machines managed by customers
## Launching EC2 Instance 
### Select AMIs (Step 1)
A Amazon Machine Image (AMI) provides information for launching an EC2

AMIs have these components:
- Template for root volume -> OS information 
- Launch permissions -> Which accounts to use it
- Block device mapping -> Volumes to attach to instances when launched 

AMIs to choose:
- Quick Start -> Pre-built AMIs
- My AMIs -> Created by you
- Marketplace -> Software solutions 
- Community AMIs -> Not checked by AWS
#### Creating a new AMI
>[!NOTE]
> <h3>Quick Overview of creating a AMI</h3>
> <img src="https://i.imgur.com/eZfUssw.png" alt="">

AMI is created from an EC2 instance
- Can import a virtual machine so it becomes a EC2 instance then save it as an AMI
- Can launch a EC2 instance from that AMI

Start using an existing AMI
- Quick start etc.
- Create a EC2 instance from it

Registering AMI
- Create a snapshot
- Launch new instances in the same Region
- Copy to other regions
### Select an instance type (Step 2)
EC2 provides a selection of instance types to fit different cases
- Varying combinations of CPU, RAM, storage, etc.
- Instance type has 1 or more instance size
- Offers family, generation and size
#### Naming and sizes
>[!NOTE]
> <h3>Simplicity sake</h3>
> For example <code>t3.large</code> will be broken down into <code>FN.T</code>

F:
- Family name 

N:
- Generation Number

T: 
- Size of EC2

>[!NOTE]
> Previous example
>
> Going with the previous example <code>t3.large</code>:
>- T is family name
>- 3 is generation
>- large is size
#### Type based on use case

| Purpose               | Types          | Use case                |
| --------------------- | -------------- | ----------------------- |
| General               | a1,m4,m5,t2,t3 | Broad                   |
| Compute optimized     | c4,c5          | High performance        |
| Memory optimized      | r4,r5,x1,z1    | In-memory databases     |
| Accelerated computing | f1,g3,g4,p2,p3 | Machine learning        |
| Storage optimized     | d2,h1,i3       | Distributed file system | 
#### Networking features
Need to consider network bandwidth requirements
- Different types of instances offer different Gbps 

New instances of spread out to minimize correlated failures
- For interdependent instances, they must be placed in a placement group
- Allows them to be placed closer on AWS server (reduce latency)

Instance types allows configuration of enhanced networking using elastic network adapter 
- Allows higher packet Pet second performance
- Lower delay variation in arrival packets

### Specify Network setting (Step 3)
After Steps 1 and 2, you must specify the network location there the instance will be at
- Must be made before you start launch wizard

Defaults:
- A `VPC` a `public IP address` will be assigned

Nondefault:
- A `VPC` the subnet has an attribute that will determine if a `public IP address` is assigned  -> Usually `private IP Address will be assigned`
- Edit public IP addressing attribute of subnet or enable or disabling the feature during launch

### Attach IAM role (Step 4 Optional)

Can attach IAM roles to instances when there is a need to interact with other services
- Use `instance profile`
- Can attach at launch or when in operation

`Instance profile`:
- A container for an IAM role
- A instance profile is created when using management console to create a role for ec2 and is given the same name

### User data script (Step 5 Optional)

When creating an EC2, you can pass user data into it
- Can automate completion of installs and configurations 
- It runs with `Root` privileges during the final phases of boot
- Only runs the **first time** the instance is start up 

### Specify storage (Step 6)

Able to configure storage options when launching EC2
- Size of root volume where guest OS is
- Attach additional storage volumes (some AMIs by default will do this)

Each volume:
- Specify size of disks
- Volume types
- If volume will be destroyed when instance is terminated 
- Encryption 

#### Storage Options

`Amazon Elastic Block Store (EBS)`:
- Durable, Block-level storage
- 4 types of volumes for optimal price and performances
- You can stop the instance and start it again, and the data will still be there
- Designed for EC2 for throughput and transaction-intensive workloads

`Amazon EC2 Instance Store`:
- Block-level storage
- Temporary storage
- If instance is stopped, data will be deleted
- If instance rebooted, data will remain

>[!NOTE]
> <h3>Instances that only have Instance Store</h3>
> An instance with an Instance Store root volume cannot be stopped by an Amazon EC2 API, only can be **stopped within system** which causes termination or **manually terminated**

call. It can only be terminated.

`Amazon Elastic File System (EFS)`:
- A scalable, fully managed Network File System
- Can be used on cloud or on-premises
- Can scale without disrupting applications
- Shrinks and grows automatically

`Amazon S3`:
- Object storage that can project any various data


### Add Tags (Step 7)

A tag is a label which can be assigned to a resource
- Way of attaching meta data to EC2
- Consists of `key` : `value (optional)` 
- Case-sensitive
- Helps categorize resource for easier management

Key names:
- Keys that start with uppercase are displayed in the EC2 instance page
- Keys that start with lowercase will not appear in “Name” column of the list of instances

### Security group settings (Step 8)

A security group acts as a virtual firewall
- Can be modified any time
- All rules evaluated on an instance 
- Only has allow rules
- Stateful -> Return traffic is allowed regardless of inbound rules
- Rules specify the source and which ports and protocol that can communicate with instance

Defining Rules:
- Can specify inbound rules or outbound
- Inbound rules be IP addresses, range of addresses, a security group, a gateway VPC endpoint, or all sources
- Default security group allows all outbound traffic
- If not outbound rules, no outbound traffic is allowed 

Can also use ACLs, see [[Chapter 5 Networking and Content Delivery]] for more information

### Identify or create the key pair (Step 9)

Before launching, a review instance launch window will pop up and check for key pair before being able to launch
- Can use existing
- Launch without
- Create new key pair

Key pair
- public key aws stores
- private key that you store
- Enables secure connections to instance

Public key
- Encrypt data

Private key
- Decrypt data

AMIs
- For Windows AMIs: Private key is used for administrator password to login to instance
- For Linux AMIs: Private key is used for SSH to securely connect to instance

### Alternative options to create instances

EC2 instances can also be created programmatically (via AWS CLI or AWS SDK)

>[!NOTE]
> <h3>Example command on CLI</h3>
> <img src="https://i.imgur.com/tHDjq3Z.png" alt="">
> <img src="https://i.imgur.com/FUAIExm.png" alt="">




## Amazon EC2 instance Lifecycle

>[!NOTE]
> <h3>High level flow chart overview</h3>
> <img src="https://i.imgur.com/aa2FMKW.png" alt="">

Pending:
- Instance is first launched
- Start a stopped instance

Running:
- Fully booted and ready
- From pending 

Rebooting:
- Goes into this and then back to running

Shutting down:
- Before termination

Terminated:
- Remains visible for a while before virtual machine is deleted
- Cannot recover

Backed by EBS:
- Stopping -> before fully stopped state
- Stopped -> VM stopped, can be started or terminated now

## Considering using Elastic IP

For persistent IP addresses
- Allocate a new elastic IP address in region where instance is
- Associate Elastic IP address to instance
- 5 limit per region; However can request for more

When not wanting persistence
- When instance is stopped or terminated, the public IP address will be released
- Cause instance to change public address and  external DNS hostname, private and internal remains the same

## Instance Meta data

It is data about your instance
- Can view when connected to it
- Can be used to configure or manage a running instance

Contains data on:
- Public & private IP address, public hostname, instance ID, security groups, Region, AZ and user data at instance launch
## Cloud Watch for monitoring

Creates readable, near-real-time metrics on EC2
- Recorded in a period of 15 months
- Charts in EC2 monitoring tab to view

Basic monitoring
- Default ec2 monitoring
- Sends data in 5 minute periods

Detailed monitoring
- 1 minute period
- Must be enabled
- Fixed monthly rate for seven pre selected metrics

RAM materics
- CloudWatch does not provide RAM metrics for EC2 instances
- Can configure to collect

# Section 3 Amazon EC2 cost optimization

## EC2 Pricing Models

Per second billing:
- Available for On-demand, Reserved, Spot instances that run Linux or Ubuntu

On-demand instance:
- Pay by hour
- Eligible for AWS Free tier
- No long term commitments

Dedicated hosts:
- A physical server with EC2 instance capacity fully dedicated to your use
- Customers can use existing licenses

Dedicated instance:
- Instances that run in a VPC on hardware that is dedicated to a Single customer
- Physically isolated from other account instances

Reserved Instances:
- AURI, PURI, NURI
- Discount on hourly charge
- 1-year or 3-year term

Scheduled Reserved instance
- Capacity reservation that is always available on a recurring schedule you specify
- 1-year term 

Spot instances:
- Bid on unused EC2 instances, up to 90% savings
- Will run when bid is above spot instance price
- Hourly rate fluctuates depending on supply and demand
- AWS can interrupt the instance

### Benefits

On-demand instances:
- Highest flexibility and low cost

Spot instance:
- Large scale at a significantly discounted price

Reserved Instance:
- Utilize when there is predictable or stead-state compute needs

Dedicated Hosts:
- Use own licenses 
- Meet compliance and regulatory requirements

### Uses cases

On-demand instances:
- Unpredictable workloads
- Short term workloads

Spot instance:
- Application need to tolerate interrupt with a 2 minute warning notification
- Very cheap option
- Uses with urgent on-the-spot computing needs with large amounts of additional capacity

Reserved Instance:
- Long term workloads with predictable usage patterns

Dedicated Hosts:
- When you have existing software licenses
- Address corporate compliance and regulatory requirements

## Four pillars of cost optimization

### Right size
- Choosing appropriate and right balance of instance types to match needs 
- Looking for opportunities to downsize

To right-size:
- Select cheapest instance available that meet requirements
- Review instance utilization to downsize
- Deploy test instance to see which ones offer best performance-to-cost ratio
- Use cloud watch metrics to setup and monitor custom metrics 

### Increase elasticity
- Stop and hibernate EBS-backed instances that are not in use
- Similar to concept of turning off light switch when not in use
- Use more precise automatic scaling for horizontal scaling to meet needs

### Optimal Pricing Model
- Leverage right pricing model for use case
- Optimize and combine purchase types
- Consider using AWS Lambda 

### Optimize storage choices
- Reduce costs while maintaining storage performance and availability
- Analyze storage requirements, reduce unused storage when possible
- Use less expensive option while meeting needs
- Use appropriate storage system for specific data
- Delete EBS snapshots when no longer needed
- Move infrequently
- access data from S3 to S3 Glacier

## Measure, monitor, and improve
Cost optimizations a continuous process 

Recommendations
- Enable cost allocation tagging through billing and cost management console which provides information on what resources is being used and costs incurred
- Encourage teams to architect for cost by using cost explorer
- Use Trusted Advisor

# Section 4 Container Services

## Container Basics

Containers:
- A method of operating system virtualization
- Can run applications and dependencies in resource isolated process 
- Can be created from images

Benefits
- Repeatable
- Self-contained environments
- Environmental consistency
- Software runs the same

## Containers VS Virtual Machines

<img src="https://i.imgur.com/Kt5Za9m.png" alt="">
- 1 EC2 for many containers compared to multiple EC2s for multiple VMS
- 1 : Many
- Many  : Many

## Elastic Container Service
A highly scalable, high performance container management service
- Run applications on a managed cluster of EC2 instances
- Supports many instance types 

Features
- Launch many docker containers in seconds
- Monitor container deployment
- Manage the state of cluster that runs containers
- Schedule containers by using inbuilt or third party scheduler (Apache Mesos or Blox)

### Task Definition
- A text file in ECS that describes up to 10 containers and specifies their parameters
- Can define Elastic container register as a repository  for container images so ECS can restive them

Tasks:
- A task is the starting of a task definition in a cluster
- ECS task scheduler is responsible for assigning and placing tasks in a cluster

>[!NOTE]
> <img src="https://i.imgur.com/koqvdVf.png" alt="">
> EC2 instance running ECS container agent

### AWS Fargate
- Manages and configures EC2 clusters for ECS

### Cluster Options
Three options when creating a cluster:
- Networking Only (powered by Fargate)
- EC2 Linux + Networking 
- EC2 Windows + Networking

>[!NOTE]
> <h3>High level Overview of options</h3>
> <img src="https://i.imgur.com/iGZi18G.png" alt="">

When choosing EC2 option:
- Choose spot or on-demand
- Get more control of cluster 

When backed by fargate:
- Cluster is managed by AWS
- You manage containers, cpu and memory requirements, networking and IAM policies.

## Elastic Kubernetes Service
- Easily run Kubernetes on AWS
- Existing applications compatible with Kubernetes will work with EKS
- Compatible with Kubernetes tools and add-ons
- Supports Linux and Windows containers

## Elastic Container Registry
A fully managed Docker container register
- Store, manage, and deploy images
- Integrated with ECS 
- To utilize, just specify repository in task definition and ECS will pull 
- Use Docker CLI commands or Docker tool to access as it supports Docker Registry HTTP API 

# Section 5 AWS Lambda

>[!NOTE]
> <h3>High level overview</h3>
> <img src="https://i.imgur.com/7FYwsXQ.png" alt="">

## What is it?
A another approach to compute
- Do not need to provision or manage servers
- Event driven
- Allows you to run code without provisioning or managing servers
- Pay for compute time you consume

## Lambda functions
- A AWS resource that contains the code you can upload
- Set Lambda function to be triggered, either on a scheduled basis or response to event

## Benefits
- Supports multiple programming languages 
- Completely automates the administration
- Built in fault tolerance (Multiple compute capacity across AZs)
- Orchestrate multiple Lambda functions
- Per-per-use pricing (pay for compute time)

## Event Source

>[!NOTE]
> <h3>High level Overview</h3>
> <img src="https://i.imgur.com/OzB2cjt.png" alt="">

A AWS service or developer-created application that produces events that trigger a function to run

**Event sources**:
S3 and Cloudwatch
- Publish events to Lambda by invoking function asynchronously

Poll resources
- SQS and DynamoDB do not publish events, you can poll resources then run functions for each message/event

Elastic Loading Balancing and API gateway
- Invoke functions directly

AWS CLI and SDK
- Invoke functions directly

## Troubleshooting

Lambda monitors its functions using Cloud Watch automatically
- Logs generated by code are automatically stored in Cloud Watch Logs 

## Function configuration

>[!NOTE]
> <h3>High level overview of creating functions</h3>
> <img src="https://i.imgur.com/e8a2GmK.png" alt="">

When creating a function through management console includes:
- Function name
- Runtime environment the function will use (version of python etc)
- Execution role (grant IAM premissions)

After creating function, configurations include:
- Adding a trigger (one of the available event sources)
- Add function to code (using code editor or upload)
- Specify memory in MB
- Optionally specify metadata, vpc, tags etc

With Lambda Console, configs above will be in a Lambda deployment package automatically 
- A ZIP archive that has code and its dependencies

Lambda API
- Need to create deployment package

## Examples

>[!IMPORTANT]
> <h3>Schedule-based</h3>
> <img src="https://i.imgur.com/AIbHJf2.png" alt="">

>[!IMPORTANT]
> <h3>Event-based Lambda function</h3>
> <img src="https://i.imgur.com/ThVQ0gC.png" alt="">

## Lambda Limits

Timeout:
- The maximum time a function takes to run

Layers:
- A Zip archive that contains libraries, custom runtime and other dependencies
- Allows us to use libraries without including them in deployment packages
- Allows us to avoid size limit for deployment packages and to share code

Soft limits per region:
- Can be overcome by submitting a support ticket to justify change
- 1000 concurrent executions
- Function and layer storage of 85GB

Hard limits for individual functions:
- Maximum function memory allocation is 10240MB
- Function timeout = 15 minutes
- Deployment package size is 250 MB unzipped including layers
- Container image code package is 10 GB

# Section 6 Elastic Beanstalk

## What is it?
Another compute service option which is a PaaS
- For quick deployment, scaling and management of user’s web application
- Only need to upload code as backend infrastructure is settled
- No additional charge, only pay for underlying resources used

Before hand:
- Ability to choose instance type, database, automatic scaling, update your application, access server log files, enable HTTPS on load balancer

Afterwards:
- AWS handles deployment
- You get full control over resources that power application

## Deployments on Elastic Beanstalk

>[!NOTE]
> <h3>High level overview of deployment</h3>
> <img src="https://i.imgur.com/CzE9Nmv.png" alt="">


Multiple ways to deploying code:
- Management Console
- CLI
- Visual Studio
- Eclipse
- Git Repo

Platforms it supports:
- Java, Python, Node.js, etc.

Beanstalk automatically deploys code on servers based on platform used:
- Apache Tomcat for Java, Apache HTTP Server for PHP and Python apps

## Benefits of Elastic Beanstalk
Fast and simple to start using
- Many ways of deploying code

Increased developer productivity
- Mainly writing code

Difficult to outgrow
- Auto scaling using CPU utilization metrics

Freedom to select AWS resources
