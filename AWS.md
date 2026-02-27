# aws
------------------------------------------------------------------------------------------------------------------------------------------------
## Introduction to AWS
* Why companies are moving to public cloud
* What are the advantages of moving to cloud.
* Introduction to the basics of AWS, including the core services and their significance in DevOps practices.
* How to set up an AWS account and navigate the AWS Management Console.

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

