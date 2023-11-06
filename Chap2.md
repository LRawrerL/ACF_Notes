## Section 1 Fundamentals of Pricing

### AWS Pricing Model
The **three Fundamental drivers** of **cost** with [[AWS]]:
1. **Compute**
2. **Storage** 
3. **Out Bound Data Transfer**
#### Compute 
- Charged per hour/second
- Varies by instance type
*Linux Only*
#### Storage
- Charge typically by **GB**
#### Data transfer
- Outbound is **aggregated** and **charged**
- **Inbound** and **between other AWS services** within the **same** region has no charge (with some exceptions)
- Charged typically per **GB**
### How do you pay for AWS?
[[AWS]] has a utility-style pricing model which includes:
- Pay for what you use
- Pay less when you reserve
- Pay less when you use more
- Pay even less as [[AWS]] grows

This is paid of **every month** and **no long term contracts** are required. You are able to **start and stop** using a product any time
#### Pay for what you use
All AWS services are **available** on demand, have no long-term contracts, and licensing dependencies. 

Some of the benefits of utilizing AWS in a pay for what you use model includes:
- Lower Variable Costs
- No need to dedicate valuable resources to building infrastructure
- No Software license
- No leasing facilities
#### Pay less when you reserve
For **certain services** you can **invest** in **reserved capacity**. This allows users to save up to **75%** over **equivalent** on demand capacity.

Three types of reserved instances are available:
1. All Upfront Reserved Instance (AURI)
2. Partial Upfront Reserved Instance (PURI)
3. No Upfront Payments Reserved Instance (NURI)
The more **Upfront payment** the more discount you will receive.
#### Pay less by using more
With [[AWS]] you can get **volume-based** discounts there are different types of discounts:
1. Tiered pricings, which mean you pay less per GB when you use more, data transfer *in* is always free. Example like (Amazon Simple Storage Service)
2. **Multiple Storage** services deliver **lower storage costs** based on needs
#### Pay even less as AWS Grows
[[AWS]] focuses on **reducing** **costs** as it is a **business**. It implements strategies like:
- **Optimizations and economics** of scale pass savings to customers
- Future **high performing resource** replace current ones with **no charge**

#### Custom Pricing
Different customers have different needs, if none works for a customer they can pick a custom pricing
- Allows [[AWS]] to meet varying needs
- Available for **high** volume projects with **unique** requirements

### AWS Free Tier
This helps new [[AWS]] customers to get started in [[Cloud Computing]]. 
- Offered for up to 1 year
- Only **gives access to certain** services and options

### Services with no Charge
[[AWS]] has options that have no additional charge, these are:
- Amazon Virtual Private Cloud
- AWS Identity and Acces Management
- Consolidated Billing
- AWS Elastic Beanstalk
- AWS CloudFormation
- Automatic Scaling
- AWS Opswork
**However** there might be **charges** associated with other [[AWS]] services that are used with them

### AWS Consolidated billing
One bill for >1 accts 
→ Tracks billing of each acct
→ Leads to volume-based discounts from combined usage of >1 accounts

## Section 2 Total Cost of Ownership
### On-Premise versus Cloud
There difference between these two is **how they are deployed**

For On-Premise:
- Long planning cycles
- Capital expenditure
- Managing infrastructure 

For AWS Cloud:
- Flexibility
- Agility
- Consumption based costs
### Total Cost of Ownership (TCO)
**TCO** is the financial estimate to help **identify** direct and indirect cost of a **system**

What it includes:
1. Cost of a service
2. All the other costs associated with owning the service

Why use TCO?
- To compare **operating** costs between on-site and cloud
- Done for **budgeting purposes** or for **optimal deployment solution**
#### TCO Consideration
Some of the costs associated with on-site include:
- **Server** costs
- **Storage** costs
- **Network** costs
- **IT labor** costs

Cloud technology is easy to determine costs:
- Transparent pricing models
- Pricing is frequently fixed per unit of time
- Most of the costs are upfront and readily calculated

On-premise technology difficult to determine costs:
- Direct costs are like power, space, and IT operations
- Indirect costs are like network and storage infrastructure 
#### On-premises versus all-in-cloud
For on-premise solutions:
- The solution is predicted
- The costs will continue to incur whether capacity is used

For all-in-cloud
- Solution can be commissioned and decommissioned when resources are no longer in use

#### Return on investment
A type of analysis used to determine value that is generated while considering spending and savings

### Additional benefits of AWS
Some additional hard benefits and soft benefits of AWS

Hard benefits
- Reduced spending on compute, storage, networking, security
- Reduction in hardware and software purchases
- Reductions in operational costs, backup, and disaster recovery
- Reduction in operations personnel

Soft Benefits
- Reuse of service and applications 
- Increased developer productivity
- Improved customer satisfaction
- Agile business process
- Increase global reach
### AWS Pricing Calculator
A [[AWS]] services used for estimating monthly AWS bills

Some of the benefits of using **AWS Pricing Calculator**
- Estimate Monthly Costs
- Identify Opportunities for cost reduction
- Model your solution before building them
- Explore price points and calculations behind your estimate
- Find available instance type and contract terms that meet your needs

**AWS Pricing Calculator** allows you to estimate, create, and name groups of services
- Groups are containers that you add to services in order to organize and build your estimate

#### Reading and Estimate
Estimates are broken into:
1. 12 month total, combines upfront and monthly estimates
2. Total Upfront
3. Total Monthly

![](https://i.imgur.com/R1aqQEm.png)
`Shows how to read an estimate`


## Section 3 AWS Organizations
### Introduction to AWS Organization
AWS organizations is a free account management service that helps centrally manage multiple accounts for an **organization**

Main benefits of AWS organizations:
- Centrally manage access policies across accounts
- Controlled access to AWS services
- Automated AWS account creation and management
- Consolidated billing across multiple AWS accounts

Key features and benefits:
- Create service control policies (SCPs) 
- Create groups of accounts and then attach policies to a group
- Simplify account management using **application programming interfaces** to automate new AWS accounts
- Consolidated billing
#### AWS Organizations terminology
![](https://i.imgur.com/LuQrcRJ.png)

Organizational Units (OU) are container for accounts within a root. OU can also contain other OUs
- Attaching policy to a OU affects all the others down the tree
- AWS accounts can only be attached to one OU 
- AWS accounts can have their own policies 

#### Security with AWS Organizations
AWS Org does not replace associating **AWS Identity and Access Management** (IAM) policies with user, groups, and roles within an AWS account

IAM policies:
- Used to allow or deny access to AWS services
- Applies to only IAM users, groups, or roles, and can never restrict AWS account root user

SCPS:
- Deny for individual AWS accounts or for groups under an OU
- Affects all IAM users, groups, and roles for an account including the AWS account root user

#### Organization Setup
```mermaid
flowchart LR
A[Step 1 Create Organization] --> B[Step 2 Create OUs]
B --> C[Create SCPS]
C --> D[Test restrictions]
```

#### Limits of AWS Organizations
![](https://i.imgur.com/vSHkUdQ.png)

#### Accessing AWS Organizations
Can be managed through different interfaces:
- AWS Management Console
- AWS CLI
- SDKs
- HTTPS query API

## Section 4 Billing and Cost Management
### Introduction
**AWS Billing and Cost Management** is the service which you use to pay AWS bills, monitor usage, and budget your costs
- Forecast and obtain a better of costs and usage in the future so you can plan ahead
- Set a custom time period 

**AWS Cost and Usage Report Tool**
- Identify opportunities for optimization through understanding cost and usage data trends

#### AWS Billing Dashboard
Allows you to view the status of your month-to-date AWS expenditure
- Allows you to understand at a high level how costs are trending

Spend Summary
- Located on the dashboard
- Shows you how much you spend last month
- Forecast for next month and month-to-date

Month-to-Date spend by service
- Shows top services you use the most 
- Shows a pie chart  

#### Tools
Used to estimate and plan AWS costs
- AWS Budgets
- AWS Cost and Usage Report
- AWS Cost Explorer
- AWS Bills

AWS Bills
- Lists cost incurred over the past month for each service
- Further broke down into AWS Region and linked accounts

AWS Cost Explorer 
- View charts of your costs
- View cost data for past 13 months
- Forecast next 3 months
- Discover patterns 
- Identify services you use the most
- View metrics 

AWS Budgets
- Shows status of your budgets and to provide forecasts of estimated costs
- Can have notifications when you exceed
- Can track monthly, quarterly, or yearly

AWS Cost and Usage Report
- Single location for accessing comprehensive information
- Can have AWS publish billing reports to S3 bucket

## Section 5 Technical Support
Provide Unique combination of tools and expertise
- AWS Support
- AWS Support Plans

Support provided for
- Experimenting with AWS
- Production use of AWS
- Business-critical use of AWS

Proactive guidance
- Technical Account Managers (TAMs)
- Prepares and informs on plan, deploy and optimize solution
- Primary contact for support needs

Best practices
- AWS Trusted Advisor
- Online resource
- Increase performance and fault tolerance
- Helps reduce monthly expenditures and increase productivity

Account Assistance
- AWS Support Concierge
- Provides quick and efficient analysis on billing and account issues

#### Support plans
The Basic Support Plan
- Customer service, documentation, whitepapers, and support forums
- Six core Trust Advisor checks
- Personal health dashboard

Developer Support Plan
- Guidance and technical support
- Quickly put AWS to work
- Use AWS for non-production workloads or applications

Business Support Plan
- Run one or more applications in production environment
- Multiple services activated or use key services extensively
- Business solutions to be available, scalable, and secure

Enterprise Support Plan
- Focus on increasing efficiency and availability 
- Build and operate to AWS best practices
- Need AWS expertise to help launches and migrations
- Want to use a TAM 

#### Case severity and response time
![](https://i.imgur.com/vGub0BZ.png)
Critical
- Business is at risk
- Business is significantly impacted
- Important functions are impaired or degraded
- Non-critical functions are not functioning or time-sensitive development question
- General development question or requesting a feature 