## Learning Resources
- Udemy course - https://www.udemy.com/course/aws-certified-developer-associate-dva-c01/
- question dump 1 - https://www.examtopics.com/exams/amazon/aws-certified-developer-associate-dva-c02/
- question dump 2 - https://www.examtopics.com/exams/amazon/aws-certified-developer-associate/
- cheatsheet - https://digitalcloud.training/category/aws-cheat-sheets/aws-developer-associate/

## The plan
- Do the entire Udemy course.
- Read all of Amazons content.
- Go through the practice questions, make flashcards.
- Study the cheat sheet.

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
## EC2 Instance Storage
### EBS (Elastic Block Store) Volumes
- An EBS volume is a network drive (not a physical drive) that you can attach to EC2 instances whilst they run.
- It allows your instances to persist data, even after you terminate the EC2 instance.
- EBS can usually only be attached to one instance, however some have a multi-attach feature.
- You may attach multiple EBS volumes to a single EC2 instance.
- EBS volumes are bound to a specific availability zone (they can be moved by taking snapshots).
- Think of an EBS volume as a network USB stick.
- Since EBS volumes communicate with your instance via the network, there may be some latency.
- You can quickly detach and re-attach EBS volumes to different EC2 instances.
- You need to provision a fixed capacity to create an EBS, however you may increase this capacity over time.
- Remember to enable the delete on termination attribute for EBS volumes you want to destroy when the EC2 instance is terminated (only enabled for the root volume by default).
- Newley added volumes are not immediately usable by your instances as they need to be formatted first.
- You can take a snapshot (backup image) of your EBS volume at a specific point in time.
- It is not necessary to detach a volume before taking a snapshot, but it is recommended.
- Snapshots allow us to copy an EBS volume from one AZ to another.
- You have to option to save your snapshots to an archive tier which is about 75% cheaper, however it takes 24 to 72 hours to restore a snapshot from the archive.
- You can set up a recycle bin with a specified retention period (one day to one year) to recover accidently deleted volumes.
- It is possible to force a fast snapshot restore to fully initialize a snapshot with no latency, but this costs a lot of money.
### EBS Volume Types
- gp2/gp3 - general purpose SSD that balances price and performance.
	- Used as boot volumes, virtual desktops, development/test environments.
	- 1GB to 16TB
	- gp2: 3000 to 16000 IOPS and 3 IOPS per GB of storage (IOPS and throughput are dependent).
	- gp3: 3000 to 16000 IOPS and 125MB/s to 1000MB/s (IOPS and throughput can scale independently).
- io1/io2 (provisioned IOPS) - highest performance SSD for critical, low-latency, or high-throughput workloads.
	- Used for critical applications with sustained IOPS performance (>16000 IOPS) e.g. database workloads.
	- 4GB to 16TB 
	- Up to 32000 IOPS for standard EC2 instances and a max of 64000 IOPS for Nitro EC2 instances.
	- IOPS can be increased independently from storage size.
	- Today we always use io2 as it costs the same as io1 but offers more durability and IOPS per GB.
	- io2 block express (still in preview) can offer up to 64TB with sub-millisecond latency and 256000 IOPS.
	- Provisioned IOPS support EBS multi-attach. 
- st1 (throughput optimized) - low cost HDD designed for frequently accessed, high-throughput workloads.
	- Used for big data, data warehouses, log processing.
	- Max throughput of 500 MB/s with a max IOPS of 500.
- sc1 (cold HDD) - lowest cost HDD for less frequently accessed workloads.
	- Used where lowest cost is optimal.
	- Max throughput of 250MB/s with max IOPS of 250.
- Only gp2/gp3 and io1/io2 can be used as boot volumes (where the OS is installed).
- To compare EBS volume types see: [Amazon EBS volume types - Amazon Elastic Compute Cloud](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)
### EBS Multi-Attach
- Only available on io1/io2 volumes.
- Allows you to attach the same EBS volume to multiple EC2 instances within the same AZ.
- Each EC2 instance has full write/read permissions to the same volume.
- Allows for concurrent read/write operations facilitating higher application availability in clustered applications.
- Scoped to a specific AZ with a max of 16 EC2 instances attached.
### EC2 Instance Store
- EBS volumes are network drives with good but limited performance.
- If you need high-performance hardware, you can use an EC2 instance store.
- Instance stores are physically attached to your EC2 instances resulting in low latency.
- Instance stores are ephemeral, meaning that if you stop your instance you lose the data stored on the instance store.
- Instance stores are good for buffers, caches, temporary data but are not a long term data storage solution.
- There is a risk of data loss if hardware fails, therefore it is wise to backup and replicate any data stored on an instance store.
- Instance store have ultra-high-IOPS (input/output operations per second).
### Elastic File System (EFS)
- Managed NFS (network file system) that can be mounted to many EC2 instances.
- Can work with EC2 instances across multiple AZs.
- Highly available, scalable, and expensive (~3x the cost of gp2).
- Used for content management, web serving, data sharing, and WordPress.
- Uses NFSv4.1 protocol using a security group to control access to the EFS.
- EFS is only compatibly with Linux based AMIs.
- Can be encrypted at rest using KMS.
- Uses the standard file API with Linux POSIX file system.
- EFS is pay-per-use, this means there is no need to plan capacity in advance (scales automatically).
- EFS can handle 1000s of concurrent NFS clients and up to 10GB+/s throughput.
- EFS can grow to a Petabyte-scale network automatically.
- Performance modes: general purpose (default), max I/O.
- Throughput modes: bursting (50MB/s with 100MB/s bursts), provisioned (set a fixed throughput), elastic (automatically scaled throughput based on workload).
- EFS-IA offers a lower cost for storage of infrequently accessed files, in order to use this you must setup a lifecycle management policy (e.g. move files from EFS to EFS-IA after 60 days of not being accessed).
- EFS also comes in an AZ scoped option with ~90% cost savings (good for development environments).
### AMI (Amazon Machine Image)
- An AMI represents your customization of an EC2 instance.
- You can add your own software, configuration, operating system, monitoring, etc.
- Using an AMI results in faster boot and configuration times as all your software is already pre-packed in the image.
- AMI are scoped to a specific region but they can be copied across to other regions.
- You can use a publicly available AMI (e.g. AWS Linux AMI), browse community AMIs, or create your own custom AMI from scratch.
- You create custom AMIs by configuring an EC2 instance and then stopping it and creating an image of it's state.
- When you create an AMI from an EC2 instance snapshots of the attached EBS volumes are also created.
## ELB (Elastic Load Balancer) & ASG (Auto Scaling Groups)
- Scalability means that a system can adapt to greater or lessor loads.
- Vertical scaling means adding more resources to an instance.
- Vertical scaling is common for non-distributed systems e.g. databases.
- RDS and ElastiCache are AWS services that are often scaled vertically.
- Horizontal scaling means increasing the number of instances themselves.
- Horizontal scaling is common for distributed systems e.g. web applications.
- In AWS speak scaling out means adding more instances and scaling in means removing some.
- AWS makes horizontal scaling very easy.
- Scalability goes hand in hand with availability, they are distinct but closely related.
- High availability is when you have horizontally scaled instances across multiple AZs.
- The goal of high availability to be able to survive a data center blackout without disrupting users.
- To achieve horizontal scaling and high availability we can use ELBs and ASGs across many AZs.
### ELB (Elastic Load Balancer)
- Load balancers are servers that forward traffic to multiple downstream servers.
- Load balancers have many advantages such as:
	- Spreading load across multiple downstream servers.
	- Exposing a single entry point (DNS) to your application.
	- Seamlessly handling downstream failures by performing health checks.
	- Providing SSL termination (https) for your website.
	- Enforcing stickiness with cookies.
	- Enabling high availability across zones.
	- Separating public traffic from private traffic.
- ELB is managed load balancer from AWS with guaranteed availability.
- AWS takes on all the admin of maintaining, upgrading, etc.
- ELB is highly integrateable with other AWS services like EC2, ASG, ECS, and many more.
- Health checks allow an ELB instance to check the health of downstream servers.
- Checks are usually carried out via an http request to a specific port and endpoint of the downstream instance e.g. http://ec2.instance:443/health.
- AWS CLB (Classic LB) supports http, https, tcp, and ssl but is deprecated.
- AWS ALB (Application LB) supports http, https, and websockets.
- AWS NLB (Network LB) supports tcp, tls, and udp.
- AWS GWLB (Gateway LB) operates at the network layer of the IP protocol.
- Some LBs can be configured for private or public access only.
- Security groups are used to control access to the system.
- Users can access the LB from anywhere but the EC2 running the app can only receive traffic from the LB.
### ALB (Application Load Balancer)
- ALB is a layer 7 (http) LB.
- It can load balance across multiple machines called target groups.
- It can also load balance to multiple applications on the same machine e.g. containers.
- Supports http/2 and WebSockets.
- Supports redirects e.g. http to https at the LB level.
- Can use routing tables to route based on endpoint, hostname, or query strings.
- ALBs are great for micro-services & container-based applications.
- Supports mapping ports to redirect to a dynamic ECS port.
- Target groups include EC2 instances, ECS tasks, Lambda functions, or private IP addresses.
- Health checks are done at the target group level.
- Comes with a fixed host name e.g. xxx.region.elb.amazonaws.com.
- An EC2 instance only sees the LB IP, to see the client IP it must look in the X-Forwarded-For http header.