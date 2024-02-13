## Section 1 AWS Global Infrastructure
### AWS Global Infrastructure
Designed and built to deliver a **flexible, reliable, scalable**, and **secure** computing environment with good **global network performance**


### AWS Region
An **AWS Region** is a geographical area
- **Data replication** across regions is controlled by you
- Communication between them uses AWS network infrastructure
- Full redundancy and connectivity 
- Consists of two or more **Availability Zones**

#### Availability Zones 
Each **AWS Region** consist of multiple **Availability Zones**
- Each Zone is isolated from each other 
- Designed for fault isolation
- Interconnected to other zones using which speed private networking
- Ability to choose zones

Zone
- Consist of discrete data centers
- Typically 3 data centers

>[!note]
> **For more resiliency**<br>
>Recommended to replicate data and resources between availability zones 

#### Selecting a Region
Some considerations when selecting optimal regions:
1. Data governance and legal requirements
2. Close as possible to users and systems to help reduce **latency**
3. Variations in cost when running a sever

### AWS Data Centers
Data centers are securely designed with several factors in mind:
- Location **evaluated** to mitigate **environmental risk**
- **Redundant design**
- **Critical system components are backed up**
- AWS monitors capacity
- **Locations are not disclosed**
- Automated process moves data traffic if there is failure

AWS uses **custom network equipment** from **multiple original device manufacturers** (ODM's)

### Points of Presence
AWS provides a global network of **Points of Presence** locations

Points of Presence
- Used to deliver better near real-time user experience
- Used for streaming/websites
- Consists of edge locations 
- Smaller number of regional edge locations

Requests going to **Amazon CloudFront** or **Amazon Route 53**  will be routed to the nearest **edge location**

Regional edge caches
- Used when data is not accessed frequently enough to remain in a edge location 

### AWS Infrastructure
AWS **Global Infrastructure** has several valuable features:
- Elastic and scalable 
- Fault tolerant
- High availability
- No Human intervention
