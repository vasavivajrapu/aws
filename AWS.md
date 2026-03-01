# AWS
------------------------------------------------------------------------------------------------------------------------------------------------
## Introduction to AWS
* Why companies are moving to public cloud
* What are the advantages of moving to cloud.
* Introduction to the basics of AWS, including the core services and their significance in DevOps practices.
* How to set up an AWS account and navigate the AWS Management Console.

------------------------------------------------------------------------------------------------------------------------------------------------
* Global infrastructure
* Organizations & multi-account strategy
* VPC networking
* Compute & database
* Security layer
* High availability & scaling

### AWS Global Infrastructure (Base Layer)
* Region
   * Physical geographic location
   * Example: Asia Pacific (Mumbai) -> Code: ap-south-1
* Availability Zone (AZ)
  * One region lo multiple data centers
  * Example: ap-south-1a, ap-south-1b
* Edge Locations
  * Used by CloudFront (CDN)
### Organization & Account Architecture
#### organization Purpose
* Multi-account management
* Central billing
* SCP control
##### SCP (Service Control Policy)
* SCP = Maximum permission boundary
* It does NOT grant permissions
* It only restricts permissions
* Default SCP, When Org creates : FullAWSAccess
* SCPs can attach to : Root, OU, Account
* Explicit Deny overrides everything
* Final permission = IAM ∩ SCP
##### Organization Structure
```
Organization (Org ID: o-xxxx)
│
├── Management Account (Billing)
│      Account ID: 111111111111 (unique)
│
├── Dev Account
│      Account ID: 222222222222
│
├── Test Account
│      Account ID: 333333333333
│
└── Prod Account
       Account ID: 444444444444
```
#### Organizational Unit
OU = Logical folder/group of accounts
* Environment based grouping
* Centralized governance
* can apply same SCPs
```
Organization Root
│
├── Workloads OU
│     ├── Dev Account
│     └── Prod Account
│
└── Security OU
      └── Log Account
```
#### Account properties
* Unique Account ID
* Separate Root User - Full permissions and cannot be restricted by IAM, applys SCP.
* Separate IAM
* Separate Resources
* OrganizationAccountAccessRole
##### Switch Role Flow
no need to use root login
```
Login → Management Account
        ↓
Switch Role
        ↓
Enter Member Account ID
        ↓
Role Name:
OrganizationAccountAccessRole
        ↓
Access Granted
```
### Inside One AWS Account (Network Layer)
```
Region
  │
  └── VPC
        ├── Public Subnet
        │      ├── EC2 (Web Server)
        │
        ├── Private Subnet
        │      ├── EC2 (App Server)
        │      └── RDS (Database)
        │
        ├── Internet Gateway
        └── NAT Gateway
```
### Enterprise Architecture Flow
```
AWS Global Infra
     ↓
Organization
     ↓
Accounts (Dev / Test / Prod / Security)
     ↓
Region
     ↓
VPC
     ↓
Subnets
     ↓
EC2 / RDS / S3 / ALB
     ↓
Security + Monitoring
```

------------------------------------------------------------------------------------------------------------------------------------------------
## SetUp
Main pieces:
* AWS CLI
* IAM (Users / Roles)
* STS (Temporary credentials)
* Target service (EC2, S3, etc.)
```
You type command
     ↓
CLI signs request using Access Key
     ↓
Request goes to AWS API endpoint
     ↓
IAM evaluates permissions
     ↓
If allowed → EC2 returns data
     ↓
CLI prints output
```
#### Configure 
* First install AWS CLI. Then configure:
```
aws configure
```
------------------------------------------------------------------------------------------------------------------------------------------------
## IAM (Identity and Access Management)
* Explore IAM
  * Who are you?
  * What can you do?
  * On which resource?
  * Under what conditions?
* How to create IAM users, groups, and roles, and how to apply permissions and security best practices to ensure proper access control.
* Policy structure (JSON) : 
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::mybucket/*"
    }
  ]
}
* Allow vs Explicit Deny
  AWS evaluates like this:
    * Default = Deny
    * If Explicit Deny → ALWAYS Deny
    * If Allow → Allowed
    * If no allow → Deny
Permission Boundaries
SCP (Service Control Policies)
IAM Best Practices

#### commands
* aws sts get-caller-identity
* aws sts assume-role --role-arn xxx --role-session-name test

------------------------------------------------------------------------------------------------------------------------------------------------
## EC2 Instances
* EC2 - which provides virtual servers in the cloud.
* How to launch EC2 instances, connect to them using SSH, and understand key concepts such as instance types, security groups, and key pairs.
* EC2 lifecycle (Start/Stop/Terminate)
* Instance types & pricing
  * 
* Security Groups
* Key pairs & SSH
* Elastic IP
* Placement groups

#### practice
AWS Project: Deploy a simple web application(such as jenkins) on the ec2 instance and access the application from outside AWS.

#### commands

------------------------------------------------------------------------------------------------------------------------------------------------

