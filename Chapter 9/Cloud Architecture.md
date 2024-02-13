Legend:
- [[#Section 1 AWS Well Architected Framework]]

# Section 1 AWS Well Architected Framework

## Architecture 

>[!NOTE]
> <h3>Overview of how Architects create a structure</h3>
> <img src="https://i.imgur.com/0nxGLdy.png" alt="">


It is about designing and building large structures
- Large systems require architects to manage their size and complexity 

## What do Cloud Architects do?
- Identify business goals and capabilities in need of improvement with decision makers
- Ensure alignment between business goals
- Work with delivery teams to ensure features of the solution are appropriate 

## What is AWS Well-Architected Framework

It is a guide for designing infrastructures that are:
- Secure
- High-performing
- Resilient
- Efficient

Contains a set of foundational questions and best practices
- Allows you to evaluate and implement cloud architectures
- These are learned by reviewing customer architecture

## Pillars of the AWS Well-Architected Framework

There are six pillars
- Operational Excellence
- Security
- Reliability
- Performance Efficiency
- Cost optimization
- Sustainability (Not covered)

Each pillar contains
- A set of design principles
- Best practices

## Operational Excellence pillar

It is to mainly `deliver business value`

Main focus
- Run and monitor systems
- Continually improve supporting processes and procedures

Key topics
- Automating changes
- Responding to events
- Defining standards to manage daily operations

### Design Principles
Perform Operation as code
- Define entire workload as code and update it with code
- Configure code to automatically trigger events
- Limits human errors and gives more consistency 

Making frequency, small, and reversible changes
- Design workloads to enable components to be updated regularly
- Make small changes that are reversible (Think of git committing) 

Refine operations procedures frequently
- Look for opportunities to improve operations
- Evolve procedures as workloads evolve 
- Set regular days to review procedures

Anticipate failure
- Identify and remove potential sources of failure
- Test failure scenarios and validate your understanding on its impact
- Test response procedures
- Set regular days to test workloads and teams response to simulated events

Learn from all operational failures
- Learn from failures and events
- Share the lessons

### Operational Excellence Questions

Organization
- How do you determine hat your priorities are?
- How do you structure your organization to support your business outcomes
- How does your organizational culture support your business outcomes

Prepare
- How do you design your workload so that you can understand its state
- How do you reduce defects, ease remediation, and improve flow into production
- How do you mitigate deployment risks
- How do you know that you are ready to support a workload

Operate
- How do you understand the health of your workload
- How do you understand the health of your operations
- How do you manage workload and operations
- events

Evolve
- How do you evolve operations

## Security Pillar

To `protect and monitor systems`

Main focus
- Protect information, systems, and assets while delivering business value through RA and mitigation strategies

Key topics
- Protecting confidentiality and integrity of data
- Identifying and managing who can do what
- Protecting systems
- Establishing controls to detect security events

### Security Design Principles

Implement a strong identity foundation
- Use principle of least privilege 
- Enforce separation of duties using authorization for each interaction
- Centralize privilege management and don't use long-term credentials

Enable traceability
- Monitor, alert, and audit actions and changes to environment
- Integrate logs and metrics with systems to auto respond and take action

Apply security at all layers
- Apply defense in depth and security controls to all layers of architectures
- Layers like VPC, subnet, every instance, OS and application

Automate security best practices
- Automate security mechanisms to improve your ability to securely scale more rapidly and cost effectively
- Create secure architectures and implement controls that are defined and manages as code in version-controlled templates

Protect data in transit and at rest
- Have sensitivity levels for data
- Utilize encryption, tokenization etc for data

Keep people away from data
- Create mechanisms and tools to reduce or eliminate the need for direct access or manual processing of data

Prepare for security events
- Have a incident management process 
- Run incident response simulations and use automation to increase speed of detection, investigation and recovery

### Security Questions

Security
- How do you securely operate your workload

IAM
- How do you manage identities for people and machines
- How do you manage permissions for people and machines

Detection
- How do you detect and investigate security events

Infrastructure protection
- How do you protect your network resources
- How do you protect your compute resources

Data protection
- How do you classify your data
- How do you protect your data at rest
- How do you protect your data in transit

Incident response
- How do you anticipate, respond to and recover from incidents

## Reliability Pillar

Statement of the pillar: `recover from failure and mitigate disruptions`

Focus
- Ensure a workload performs its intended function correctly and consistently when it's expected to

Key topics
- Designing distributed systems
- Recovery planning
- Handling change

### Reliability design principles

Automatically recover from failure
- Monitor systems for key performance indicators and configure systems to trigger an automated recovery when threshold is breached
- This enables automatic notification, failure-tracking and automated recovery processes that work around or repair the failure

Test recovery procedures
- Test how your systems fail and validate your recovery procedures
- Use automation to simulate different failures or scenarios

Scale horizontally to increase aggregate workload and availability
- Replace a large resource with multiple smaller ones and distribute request's across them 

Stop guessing capacity
- Monitor demand and usage, and automate the addition or removal of resources to maintain the optimal level for demand

Manage change in automation
- Use automation to make changes to infrastructure and manage changes in automation

### Reliability Questions

Foundations
- How do you manage service quotas and constraints
- How do you plan your network topology

Workload Architecture 
- How do you design your workload service architecture
- How do you design interactions in a distributed system to prevent failure
- How do you design interactions in a distributed system to mitigate or withstand failures

Change management
- how do you monitor workload resources 
- How do you design your workloads to adapt to changes in demand
- How do you implement change

Failure management
- How do you back up data
- How do you use fault isolation to protect your workload
- How do you design your workload to withstand component failures
- How do you test reliability
- How do you plan for disaster recovery

## Performance Efficiency Pillar

Pillar Statement: `Use Resources Sparingly`

Main Focus:
- Use resources efficiently to meet system requirements and maintain that efficiency as demand changes and tech evolves

Key topics
- Selecting right resource based on workload
- Monitoring performance
- Making informed decisions to maintain efficiency as business needs evolve

### Design principles

Democratize advanced technologies
- Use technologies as a service 
- Allows us to focus on product instead of resource management

Go global in minutes
- Deploy systems in multiple regions at minimal cost

Use server less architectures
- Removes burden of traditional compute
- Lower transactional costs 

Experiment more often
- Test different resource types and configurations

Consider mechanical sympathy
- Use technology approach that aligns best to what we want to achieve
- For example, consider using data access patterns when selecting databases or storage

### Performance Efficiency Question

Selection
- How do you select the best performing architecture
- How do you select your compute solution
- How do you select your storage solution
- How do you select your database solution
- How do you configure your networking solution

Review
- How do you evolve your workload to take advantage of new releases

Monitoring
- How do you monitor your resources to ensure they are performing

Tradeoffs
- How do you use tradeoffs to improve performance

## Cost Optimization Pillar

Statement Pillar: `Eliminate uneeded expense`

Main Focus:
- Avoid unnecessary cost

Key topic
- Understanding and controlling where money is being spent
- Selecting the most appropriate and right number of resource types
- Analyzing spend over time
- Scaling to meeting business needs without overspending

### Design Principles

Implement Cloud Financial Management
- Invest in cloud financial management and cost optimization
- Build capability through knowledge building, programs, etc
- These lead to financial success and business value realization

Adopt a consumption model
- Pay only for what we require. Increase or decrease usage depending on business needs NOT by elaborate forecasting

Measure overall cost efficiency
- Measure business outputs of workloads and costs incurred with it
- Use this measure to know the gains that we make from increasing output and reducing costs

Stop spending money on undifferentiated heavy lifting
- AWS does the heavy lifting of hardware architecture of Cloud
- We can focus on customers and business projects instead

Analyze and attribute expenditure
- Cloud makes it easy to identify system usage and costs and attribute them to workload owners
- This helps us to measure ROI and gives owners potential to optimize resources and cost

### Optimization Question

Practice cloud financial management
- How do you implement cloud financial management

Expenditure and usage awareness
- How do you govern usage
- How do you monitor usage and costs
- How do you decommission resources 

Cost-effective resources
- How do you evaluate cost when you select services
- How do you meet cost targets when you select resource type, size, and number
- How do you use pricing models to reduce cost
- How do you plan for data transfer changes

Manage demand and supply resources
- How do you manage demand and supply resources

Optimize overtime
- How do you evaluate new services

## AWS Well-Architected Tool
- Helps you review the state of your workloads and compares them to the latest AWS architectural best practices
- Gives you access to knowledge and best practices used by AWS architects, whenever you need it
- Deliver an action plan with step-by-step guidance on how to build better workloads for the cloud
- Provides a consistent process for you to review and measure your cloud architecture
- Available in the Management Console
- Can design workload and answer questions in the areas of pillar

# Section 2 Reliability and Availability

## Reliability definition

It is a measure of the system's ability to provide functionality when desired by user
- Think of it in statistical terms
- Probability that a system will function for a period 
- Measure using MTBF (Mean time between failures) -> Total time divided by number of failures

## Reliability metrics

>[!NOTE]
> <h3>High level overview</h3>
> <img src="https://i.imgur.com/qMiSkHt.png" alt="">

>[!TIP]
> <h3>Example calculations</h3>
> Applications starts on Monday dat Noon <br>
> - Functions normally until Friday noon <br>
> - Time to Failure (length of time it was functioning) = 96 hours <br>
> - Friday noon till Monday noon fixing it <br>
> - Time to Repair = 72 hours <br>
> - It repeats every week <br>
> - Average of the numbers <br>
> - MTTF (to failure) = 96 hour <br>
> - MTTR (to repair) = 72 hours <br>
> - MTBF (between failure) = 168 hours (1week) <br>
> - MTBF is also MTTF + MTTR

## Availability

It is the percentage of time that the system is operating normally or correctly performing 
- Reduced anytime application is not operating normally
- Includes both scheduled and unscheduled interruptions
- Can also be normal operation time ÷ total time (total time is typically 1 year)

Another way to represent availability is number of 9s
- Five 9s means 99.999% availability

## High Availability
Refers to a system that
- Withstand some degradation while being online
- Downtime minimize
- Minimal human intervention

It combines software with open-standard hardware that restores services when failure occurs

A highly available system can be viewed as a set of system-wide shared resources

## Availability Tiers

>[!NOTE]
> <h3>Table on availability tiers</h3>
> <img src="https://i.imgur.com/O6sCdIU.png" alt="">

## Factors that influence availability

Fault tolerance
- Built-in redundancy of components and being able to remain operational when some hardware components fail
- Relies on special hardware to detect failure in a hardware component and switches to a redundant hardware component
- Does not address software failures, which are most common cause for downtime 

Scalability
- Ability to accommodate increase in capacity needs, remain available and perform within standards
- Does not guarantee availability, but contributes to it 

Recoverability
- Restore service quickly without data loss if a disaster makes components unavailable 

Caveats of improving availability
- Increases cost 

# Section 3 AWS Trusted Advisor 

A online tool that provides real-time guidance to help user provision resources following AWS best practices
- Looks at user AWS environment and gives real-time recommendation in 5 categories 

5 categories

1. Cost Optimization
	- TA looks at resource usage and gives recommendations to optimize cost by eliminating unused and idle resources or by committing to reserved capacity

2. Performance
	- Improve performance by checking service limit
	- Ensure we take advantage of provisioned throughput and monitor for overutilized resources

3. Security
	- Improve security by closing gaps and enabling AWS security features and examine permissions

4. Fault Tolerance
	- Increase availability and redundancy by using automatic scaling, health checks, >  1 AZ deployment, and backup capabilities

5. Service limits
	- TA checks for service usage that is **more than 80% of service limit (service quota, each region can prevision up to a fixed amount of resources)**
	- Values are **based on a snapshot** so **real-time values might differ**
	- Limit and usage data **takes up to 24 hours to reflect any changes**

