 
# Section 1 Elastic Load Balancing

## Elastic Load Balancing
- When websites/app server thousands of users
- There needs to be a way to manage traffic
- ELB will help handle it

### What does EBL do?

>[!note] High Level Overview
>![](https://i.imgur.com/vMlX912.png)

It is a service that **distributes** the **incoming application** or **network traffic** across multiple **targets** in a **single AZ** or **multiple AZs**
- Targets -> EC2s, containers, IP addresses, and lambda functions
- **Scales** the **load balancer** as traffic to your **application changes over time**

### Types of Load Balancers
1. Application Load Balancer
	- Ideal for **HTTP and HTTPS traffic**
	- Routes traffic to targets **based on content of request**
	- Has advanced **request routing** to modern app architectures like **microservices** and **containers**
	- **Ensures security** by using latest **SSL/TLS** encryption and protocols
	- **Operates** at **Application Layer** (Layer 7)
2. Networking Load Balancer
	- Used for **TCP, UDP, and TLS traffic** when **extreme performance** is needed
	- Routes traffic to targets **based on IP protocol data**
	- Can handle **millions of requests** per second while maintaining **ultra-low** latencies
	- Optimized to **handle volatile** traffic patterns
	- **Operates** at **Transport Layer** (Layer 4)
3. Classic Load Balance (Previous Generation)
	- Ideal for **HTTP, HTTPS, TCP, and SSL traffic**
	- Load balancing across **multiple EC2 instances**
	- **Operates** at both **Application and Transport Layer**

### How ELB works
Load balancer **accepts incoming traffic** from clients and then **routes requests** to its **registered targets** in **one or more AZ**

We need to configure 1 or more **Listeners** to accept incoming traffic
- A **listener** checks for specific **connection requests**
- Configured with a **protocol** and **port number** for connection **between clients and load balancer** and **target group to forward traffic to**

Load Balancers can be configured to do **health checks**
- Instance with **high utilization** is considered **unhealthy**
- Use to monitor health of **registered** targets
- Load balancer only sends **requests** to healthy targets only
- Load balancer will stop routing traffic to unhealthy target until it becomes healthy

### Configurations of Targets for each type of Load Balancer
1. Application and Network Load Balancer
	- Register targets into target groups
	- Traffic is routed to the target group
2. Classic LB
	- We register instances with LB directly

### Use cases of Elastic Load Balancing (Remember main points)

**Achieve high availability and better fault tolerance for your applications**
- Can route to multiple AZs
- If unhealthy will route to other target

**Automatically load balance your containerize applications**
- Can load balance multiple ports on the same EC2 instance
- Deep integration with ECS
- Auto detection of ports and dynamically configures them

**Automatically scale your applications**
- Works with Cloud Watch and EC2 Auto Scaling
- When new instance is created from Auto scaling, ELB will register in target group

**Use ELB in VPC**
- Can be used as entry point into VPC or route requests between tis of application in VPC
- Security Groups can be assigned to ELB to control which ports are open to specified allowed sources
- Existing ACLs and route tables continue to provide additional network controls
- LB can be public (default) or internal in VPC only (no need for IGW) and private IP of LB is used in DNS record

**Enable hybrid load balancing**
- ELB allows load balancing across AWS and on-premise by using same LB
- We can register all resources to same target group with 1 LB for this use
- We can also do DNS-based weighted LB by using 2 LB, 1 for AWS 1 for on-premise
- Can be used to benefit separate applications where 1 is in VPC and 1 is on-premise
- Can put VPC targets in 1 group and on-premise targets in 1 group
- Then do content-based routing to route traffic for each group

**Invoking Lambda functions over HTTP(s)**
- ELB can invoke Lambda functions to serve HTTP or HTTPS requests
- Enables users to access serverless application from any HTTP client (incl. browsers)
- Lambda functions can be registered as targets and we can use content-based routing rules in Application LB to route requests to different functions
- Application LB can be used as a common HTTP endpoint for applications that use servers and serverless computing

### Load Balancer Monitoring

There are features and services to help monitor load balancers, analyze traffic patterns, and troubleshoot issues

**Amazon Cloud Watch Metrics**
- ELB publishes data points to Cloud Watch 
- Can retrieve statistics about data points in the form of metrics
- Can use metrics to trigger alarms to initiate an action

**Access Logs**
- Stored in S3
- Capture detailed information about requests made to load balance

**AWS Cloud Trail Logs**
- Captures detailed information about calls made to ELB API 
- Stored in S3 
- Can determined who, what, when, where etc of calls

# Section 2 Amazon Cloud Watch

## Amazon Cloud Watch
To use resources effectively, we need information (such as usage) about them
- Monitors utilization, usage, etc.
- DOES NOT monitor API calls, that is CloudTrail

### Cloud Watch
Monitors
- AWS resources and Applications that run on AWS
Collections and tracks
- Standard and custom metrics
Alarms
- Send notifications to Amazon SNS 
- Perform EC2 auto scaling or actions
Events
- Define rules that match incoming events/changes and route them to targets for processing
- CW Events becomes aware of changes as they occur and takes corrective action defined by user

### Cloud Watch Alarms
It watches a single Cloud Watch metric or a result of math expression based on the metric
- Created based on static threshold, anomaly detection, or metric math expression

When creating a Static Threshold Alarm we need to specify
- Namespace -> (Cloud Watch Metric, AWS/EC2)
- Metric -> (A variable you want to measure)
- Statistic -> (average, sum, sample count etc)
- Period -> (Time period for one data point)
- Conditions -> (>, >=, < etc. than threshold value)
- Additional configuration information -> (Number of data points or how to treat missing data)
- Actions -> (What to do)

# Section 3 Amazon EC2 Auto Scaling

## Why is scaling important

>[!note] Graph showing usage
>![](https://i.imgur.com/UKCLiM7.png)
- We need to increase/decrease capacity of application to adopt to varying workloads (dynamic)
- Provision **what we need** to use Provision **less** when **demand is less** Provision **more** when **demand is more**
- Leads to reduced cost

## EC2 Auto-scaling
A service that **automatically** adds or removes EC2 instance according to **conditions** you define
- Helps **maintain health** and **availability** of fleet
- Detects **impaired** and **unhealthy** instances/applications and **replaces them automatically**

Auto-scaling provides several ways to adjust scaling
- Add or remove EC2 **manually**, on a **schedule**, in **respond to demanding change**, or with AWS **Auto-scaling for predictive scaling**
- **Dynamic scaling** and **predictive** can be used together for **faster scaling**

### Auto Scaling Groups

>[!note] High Level Overview 
>![](https://i.imgur.com/k7SnoYi.png)

It is a **collection** of EC2 instances that is treated as a logical grouping
- **Initial size** of group depends on number of **Desired Capacity**
- Auto Scaling will not go below **Minimum Size**
- Auto Scaling will not go above **Maximum Size**
- **Scaling policies** can help **launch or terminate instances** as demand on your application **increases of decreases**

### Scaling out versus scaling in

>[!note] Overview on scaling in and out
>![](https://i.imgur.com/WpCPLWd.png)

Also called horizontal scaling
- When launching instances -> Scaling out
- When terminating instances -> Scaling in

### How auto scaling works

>[!note] High Level Overview
>![](https://i.imgur.com/owMcqSi.png)

To launch EC2 Instances
- Auto scaling group uses a launch configuration which is a instance configuration template 
- We also need to define min, max, and desired capacity
- Then launch it into a VPC subnet (can also integrate with Elastic Load Balancing to attach 1 or more Load Balancers to an AS group) ELB auto registers the instances in the group and distributes traffic across them

Launch configuration
- AMI
- Instance type
- IAM Role
- EBS Volumes
- Security groups

When you want scaling event to occur
- Maintain current instance levels at all times
	- EC2 auto-scaling uses health checks -> if there is unhealthy instance, a new one will be created and the old one terminated
- Manual scaling
	- Specify only change in max, min, or desired cap of auto scaling group
- Scheduled scaling
	- Scaling actions are performed automatically   during a date and time, good for predictable workloads
- Dynamic scaling
	- Define parameters that control scaling
	- Example: Web application running on 2 instances and we want CPU Utilization to stay at 50% as demand changes
	- Useful for scaling in response to changes
	- Also gives us extra capacity to handle traffic spikes without excessive idle resources We can use scaling policy to trigger EC2 AS with CW Alarms
- Predictive scaling
	- Use EC2 auto-scaling with auto-scaling
	- Predicts demand and scales instances (recurring load patterns)
	- Uses data collected from EC2 usage and billions of data points
	- Uses machine learning models
	- Model needs at least 1 day of data and evaluated every 24 hours to forecast next 48 hours Prediction process produces a scaling plan that can be used on ≥ 1 EC2 AS group

### Implementing Dynamic Scaling

>[!note] High Level Overview
>![](https://i.imgur.com/VSff1NF.png)
- Use cloud watch, elastic load balancing, and ec2 auto scaling
- A common configuration for dynamic scaling involves CW alarm based on performance info from EC2 instances or LB
- Cloud watch Alarm will trigger the EC2 auto scaling
- CW, EC2 AS and ELB work well individually but they work even better together that increases control and flexibility of handling demand
>[!example] On overview
>- You create an Amazon CloudWatch alarm to monitor CPU utilization across your fleet of EC2 instances and run automatic scaling policies if the average CPU utilization across the fleet goes above 60 percent for 5 minutes.
>- Amazon EC2 Auto Scaling instantiates a new EC2 instance into your Auto Scaling group based on the launch configuration that you create.
>- After the new instance is added, Amazon EC2 Auto Scaling makes a call to Elastic Load Balancing to register the new EC2 instance in that Auto Scaling group.
>- Elastic Load Balancing then performs the required health checks and starts distributing traffic to that instance. Elastic Load Balancing routes traffic between EC2 instances and feeds metrics to Amazon CloudWatch.

## AWS Auto Scaling
A **separate service from EC2 AS** that monitors applications and auto adjusts capacity to maintain predictive performance at lowest possible cost

Works in conjunction with EC2 AS to implement Predictive Scaling

Build **scaling plans** for resources including:

- EC2 instances and Spot Fleets
- ECS tasks
- DynamoDB tables and indexes
- AWS Aurora Replicas

We can use AWS AS to scale resources for other AWS services