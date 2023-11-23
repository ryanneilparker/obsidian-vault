# AWS Certified Developer - Associate
## AWS Regions & Availability Zones
### AWS Regions
- An AWS region is a geographical area where Amazon Web Services (AWS) has built and operates multiple data centers.
- Regions are named according to their geographical location e.g. `us-east-1` or `af-south-1`.
- Consider the following when choosing a region:
	- Compliance with data governance and legal requirements (data can never leave a region by itself).
	- Proximity to end users (closer proximity reduces latency).
	- Availability of services (newer services aren't always available in all regions).
	- Pricing (pricing can vary from region to region).
### AWS Availability Zones (AZs)
-  Availability zones are groups of one or more independent data centers within a region.
- Each region has a minimum of 3 and maximum of 6 availability zones.
- Availability zones are linked together by high-bandwidth, ultra-low-latency networking to form a region.
- Availability zones are identified by letters at the end of the region name e.g. `us-east-1a` or `as-south-1b`.
## AWS IAM (Identity and Access Management)
- IAM is a global service (meaning it is not scoped to a specific region).
- IAM users are people within an organization that can be grouped together.
- Groups can only contain users and not other groups.
- Users can belong to multiple groups.
- Users or groups can be assigned JSON documents called policies that specify their AWS permissions.
- Users inherit the permissions policies of the groups they belong to.
- Inline policies can also be applied directly to a user.
- Always apply the principle of least privilege.
### IAM policy structure:
- Version - policy language version (required, usually 2012-10-17).
- ID - an identifier for the policy (optional).
- Statement - one or more statements (required)
	- Sid - an identifier for the statement (optional)
	- Effect - whether the statement allows or denies access (Allow or Deny).
	- Principal - account/user/role to which the policy is applied.
	- Action - list of actions this policy allows or denies (API calls).
	- Resource - list of resources to which the actions are applied.
	- Condition - conditions under which this statement is in effect. (optional)
```json
{
	"Version": "2012-10-17",
	"Id": "S3-Account-Permissions",
	"Statement": [
		{
			"Sid": "1",
			"Effect": "Allow",
			"Principal": {
				"AWS": ["arn:aws:iam::1234566789012:root"]
			},
			"Action": [
				"s3:GetObject",
				"s3:PutObject"
			],
			"Resource": ["arn:aws:s3:::mybucket/*"]
		}
	]
}
```
### IAM Password Policy
- Set minimum password length.
- Require specific characters e.g. uppercase letters, numbers, non-alphanumeric.
- Require at least one number.
- Allow/deny password resets.
- Require password expiration.
- Prevent password re-use.
- Multi-Factor-Authentication (hacker needs password and physical device).
	- Virtual MFA device (Google Authenticator, Microsoft Authenticator, Authy, etc.).
	- Universal 2nd Factor (U2F) security key (USB that generates a token) (FIDO).
	- Hardware Key Fob MFA device (garage remote that generates a token) (TOTP).
## AWS Access Keys, CLI, & SDK
There are 3 ways to access AWS:
1. AWS Management Console (protected by password + MFA).
2. AWS Command Line Interface (CLI) (for direct access to public AWS APIs, protected by access keys).
3. AWS Software Developer Kit (SDK) (for when you want to call AWS APIs from code, protected by access keys).
- Access keys are generated via the management console.
- Users manage their own access keys.
- Do not share access key IDs or secrets.
## AWS CLI / AWS CloudShell
`msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi` - install the AWS CLI.
`aws --version` - check which version of the AWS CLI is installed.
`aws configure` - configure AWS access key.
`aws iam list-users` - list all users on AWS account.
`aws iam list-users --region eu-west-1` - list all users on AWS account for a specific region.
- Files created in the CloudShell persist between sessions.
### IAM Roles for Services
- Some AWS services will need to perform actions on your behalf.
- We can assign permissions to AWS services with IAM Roles.
### IAM Security Tools
- IAM Credentials Report (account-level) - a report that lists the users and their status on your account.
- IAM Access Advisor (user-level) - shows the service permissions granted to a user and when they were last used. This info is helpful for revising policies.
### IAM Best Practices
- Don't use the root account except for setting up the AWS account.
- Assign users to groups and manage policies at the group level.
- Create a strong password policy.
- Use and enforce the use of MFA.
- Create and use Roles for giving permissions to AWS services.
- Use access keys for programmatic access to AWS (CLI/SDK).
- Audit your account policies by using the Credentials Report and Access Advisor.
- Never share IAM users and access keys.
### IAM Shared Responsibility Model
AWS is responsible for:
- Infrastructure (global network security).
- Configuration and vulnerability analysis.
- Compliance validation.
You are responsible for:
- Users, groups, roles, policies and the management and monitoring thereof.
- Enabling and enforcing MFA.
- Rotating all your keys often.
- Using IAM tools to apply appropriate policies.
- Analyzing access patterns and reviewing policies.
### IAM Summary
- Users: map physical users to IAM users with passwords to access the AWS console.
- Groups: contain users only.
- Policies: JSON document that outlines the permissions for users, groups, or roles.
- Roles: grant permissions for EC2 instances or other AWS services.
- Security: MFA + Password Policy.
- AWS CLI: manage AWS services via the command line.
- AWS SDK: manage AWS services programmatically.
- Access Keys: needed for accessing AWS via the CLI or SDK.
- Audit: IAM Credential Reports + IAM Access Advisor.
## Amazon EC2 (Elastic Compute Cloud)
- EC2 is an Infrastructure as a Service (IaaS) offering from AWS.
- EC2 is not limited to compute there are other offerings such as:
	- Renting virtual machines (EC2).
	- Storing data on virtual drives (EBS).
	- Distributing load across machines (ELB).
	- Scaling the services using auto-scaling group (ASG).
- Knowing how EC2 works is fundamental to understanding the cloud.
### EC2 Sizing & Configuration
- Operating System (OS) - Linux, Windows, Mac OS
- How much compute power and cores (CPU).
- How much random-access memory (RAM).
- How much storage space:
	- Network-Attached (EBS & EFS).
	- Hardware-Attached (EC2 Instance Store).
- Network card (speed, public IP address).
- Firewall rules (Security Group).
- Bootstrap script (configure at first launch) (EC2 User Data)
### EC2 User Data
- We use this to bootstrap our instances using an EC2 User Data script.
- The script runs only once when the virtual machine first starts.
- It can be used to automate tasks such as:
	- Installing updates.
	- Installing software.
	- Downloading files from the internet.
	- Anything else.
- This script runs with root user permissions (sudo).
### EC2 Instance Types
- There are different instance types optimized for different use cases, see https://aws.amazon.com/ec2/instance-types/.
	- General purpose (class M/T).
		- General purpose instances provide a balance of compute, memory and networking resources, and can be used for a variety of diverse workloads. These instances are ideal for applications that use these resources in equal proportions such as web servers and code repositories. 
	- Compute Optimized (class C).
		- Compute Optimized instances are ideal for compute bound applications that benefit from high performance processors. Instances belonging to this category are well suited for batch processing workloads, media transcoding, high performance web servers, high performance computing (HPC), scientific modeling, dedicated gaming servers and ad server engines, machine learning inference and other compute intensive applications.
	- Memory Optimized (class R/X/z).
		- Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.
	- Accelerated Computing (class P/Inf/G/F/VT).
		- Accelerated computing instances use hardware accelerators, or co-processors, to perform functions, such as floating point number calculations, graphics processing, or data pattern matching, more efficiently than is possible in software running on CPUs.
	- Storage Optimized (I/D/H-class).
		- Storage optimized instances are designed for workloads that require high, sequential read and write access to very large data sets on local storage. They are optimized to deliver tens of thousands of low-latency, random I/O operations per second (IOPS) to applications.
	- HPC Optimized (class Hpc).
		- High performance computing (HPC) instances are purpose built to offer the best price performance for running HPC workloads at scale on AWS. HPC instances are ideal for applications that benefit from high-performance processors such as large, complex simulations and deep learning workloads.
- EC2 instance naming convention:
	- (instance class)(instance generation).(instance size)
	- e.g. m5.2xlarge
- To compare EC2 instances see: https://ec2instances.info
### EC2 Security Groups
- Security groups are fundamental to network security in AWS.
- They control what traffic is allowed into or out of our EC2 instances.
- Security groups only contain allow rules.
- The inbound/outbound rules can reference by IP or by security group.
- Security groups are a firewall on our EC2 instances.
- They regulate:
	- Access to ports.
	- Authorized IP ranges (both IPv4 and IPv6).
	- Control inbound network traffic.
	- Control outbound network traffic.
- Security groups can be attached to multiple instances.
- Locked down to a region / VPC combination.
- Exists outside of the EC2 instance (blocked traffic is never seen by the EC2 instance).
- It is good practice to have a separate security group just for SSH access.
- All inbound traffic is blocked by default and all outbound traffic is authorized by default.
### Common EC2 Ports
- 22 - SSH (Secure Shell) - used to log into a Linux instance.
- 21 - FTP (File Transfer Protocol) - upload files into a file share.
- 22 - SFTP (Secure File Transfer Protocol) -  upload files using SSH.
- 80 - HTTP - access unsecured websites.
- 443 - HTTPS - access secured websites.
- 3389 - RDP (Remote Desktop Protocol) - used to log into a Windows instance.
### SSH into EC2 Instances
- Allows us to control a remote machine using the command line.
- For is to to work we need the SSH Port 22 security group on the instance.
- `chmod 0400 EC2Tutorial.pem`
- `ssh -i EC2Tutorial.pem`
- `ssh ec2-user@<public IPv4>`
- Alternatively you can use EC2 Instance Connect.
### EC2 Purchasing Options
1. **On-Demand Instances**
    - Suitable for short workloads with a flexible payment model.
    - Billed per second for Linux/Windows (after the first minute), and Mac OS is billed per hour.
    - Highest cost option with no upfront payment or long-term commitment.
    - Recommended for short-term, uninterrupted and unpredictable workloads.
    - Think of it as staying in a resort where you pay the full price for the time you stay.
2. **Reserved Instances**
    - Designed for long workloads with significant cost savings (1 & 3 years commitment).
    - Offers approximately a 72% discount compared to On-Demand.
    - Allows reservations for specific instance types, regions, tenancy, OS, or zones.
    - Longer reservation periods result in higher discounts.
    - Upfront payment or partial upfront payment further reduces costs.
    - Resale option available on a marketplace.
    - Convertible version allows attribute changes, such as instance type, region, OS, or zone, with a smaller discount of approximately 66%.
    - Recommended for steady-state usage, such as databases.
    - It's like reserving a room in the resort when you know you'll be staying for an extended period.
3. **Savings Plan**
    - Suited for long workloads with a fixed commitment to a specific usage amount (e.g., $10/hour for 1 year or 3 years).
    - Offers the same discount as Reserved Instances but with a cost commitment.
    - Usage beyond the commitment is billed at the On-Demand rate.
    - Allows access to any available resources including other AWS services like Lambda or Fargate.
    - Think of it as purchasing a pass to access any room in the resort for a specified period.
4. **Spot Instances**
    - Ideal for cost-effective, short workloads with some unpredictability.
    - Offers approximately a 90% discount compared to On-Demand.
    - You set a maximum price, and if it's below the current spot price, you may lose the instance to a higher bidder.
    - Most cost-effective instance type in AWS.
    - Recommended for tasks like batch processing, data analysis, or image processing.
    - Not suitable for critical or time-sensitive workloads.
    - Think of it as bidding on available rooms in the resort, but someone may outbid you and take the room.
5. **Dedicated Hosts**
    - The most expensive option, designed for specific use cases.
    - Recommended for software with complex licensing models (e.g., bring your own license) or organizations with stringent regulatory or compliance requirements.
    - Allows full control over instance placement.
    - Allows you to reserve and control the entire resort for your needs.
6. **Dedicated Instances**
    - Similar to dedicated hosts but without hardware access.
    - You do not share resources with other AWS customers.
1. **Capacity Reservations**
    - Reserve capacity in a specific Availability Zone (AZ) for any duration.
    - Charged at the On-Demand rate, regardless of whether you run instances.
    - Recommended for short-term, uninterrupted workloads that require a specific AZ.
    - Think of it as booking a room and paying the full price, even if you're unsure whether you'll use it.