# AWS Certified Solutions Architect – Associate(2018) Tips

## General

- Tags enable you to categorize your AWS resources in different ways.

- The term pilot light is often used to describe a DR scenario in which a minimal version of an environment is always running in the cloud. 

- Perfect Forward Secrecy is a feature that provides additional safeguards against the eavesdropping of encrypted data, through the use of a unique random session key. This prevents the decoding of captured data, even if the secret long-term key is compromised. Cloudfront and Elastic Load Balancing are the two AWS services that supports Perfect Forward Secrecy.

- Amazon Simple Queue Service (SQS) and Amazon Simple Workflow Service (SWF) are the services that you can use for creating a decoupled architecture in AWS.

## VPC, VPN

- In the default VPC, AWS automatically sets up the following for you:

   * Create a VPC with a size /16 IPv4 CIDR block (172.31.0.0/16). This provides up to 65,536 private IPv4 addresses.

   * Create a size /20 default subnet in each Availability Zone. This provides up to 4,096 addresses per subnet, a few of which are reserved for our use.

   * Create an Internet Gateway and connect it to your default VPC.

   * Create a main route table for your default VPC with a rule that sends all IPv4 traffic destined for the Internet to the Internet gateway.

   * Create a default security group and associate it with your default VPC.

   * Create a default network access control list (ACL) and associate it with your default VPC.

   * Associate the default DHCP options set for your AWS account with your default VPC.

- Changes made in a Security Group is immediately implemented to all associated EC2 instances.

- The allowed block size is between a /28 netmask and /16 netmask.

- The CIDR block must not overlap with any existing CIDR block that's associated with the VPC.

- Network ACL Rules are evaluated by rule number, from lowest to highest, and executed immediately when a matching allow/deny rule is found.

- You cannot increase or decrease the size of an existing CIDR block.

- The first four IP addresses and the last IP address in each subnet CIDR block are not available for you to use, and cannot be assigned to an instance.

- In an ideal and secure VPC architecture, you launch the web servers or elastic load balancers in the public subnet and the database servers in the private subnet.

- A bastion host is a special purpose computer on a network specifically designed and configured to withstand attacks.

- We have two types of rules in Security Group: Inbound and Outbound rules.

## EC2

- Instance metadata is data about your instance that you can use to configure or manage the running instance. You can get the instance id, public keys, public IP address and many other information from the instance metadata by firing a URL command in your instance to this URL: (http://169.254.169.254/latest/meta-data/).

- The instance retains its associated Elastic IP addresses if it is in the EC2-VPC platform and not on EC2-Classic.

- If you use PuTTY to connect to your instance via SSH and get either of the following errors, Error: Server refused our key or Error: No supported authentication methods available, verify that you are connecting with the appropriate user name for your AMI. You should also verify that your private key (.pem) file has been correctly converted to the format recognized by PuTTY (.ppk).

- Amazon EC2 has a soft limit of 20 instances per region, which can be easily resolved by completing the Amazon EC2 instance request form where your use case and your instance increase will be considered. Limit increases are tied to the region they were requested for.

- To log in to your instance, you must create a key pair.

- By default, your instance is enabled for basic monitoring. Data is available automatically in 5-minute periods at no charge.

- If your Spot instance is terminated or stopped by Amazon EC2 in the first instance hour, you will not be charged for that usage. However, if you terminate the instance yourself, you will be charged to the nearest second. If the Spot instance is terminated or stopped by Amazon EC2 in any subsequent hour, you will be charged for your usage to the nearest second. If you are running on Windows and you terminate the instance yourself, you will be charged for an entire hour.

- Snapshots occur asynchronously which means that the point-in-time snapshot is created immediately, but the status of the snapshot is pending until the snapshot is complete (when all of the modified blocks have been transferred to Amazon S3), which can take several hours for large initial snapshots or subsequent snapshots where many blocks have changed. While it is completing, an in-progress snapshot is not affected by ongoing reads and writes to the volume hence, you can still use the volume.

- The best way to implement a bastion host is to create a small EC2 instance which should only have a security group from a particular IP address for maximum security.

- You can launch EC2 instances in a placement group, which determines how instances are placed on underlying hardware. 

- In cases where your EC2 instance cannot access the Internet, you usually have to check two things:

  * Does it have an EIP or public IP address?
  * Is the route table properly configured?

- An elastic network interface (ENI) is a logical networking component in a VPC that represents a virtual network card. You can attach a network interface to an EC2 instance in the following ways:

  * When it's running (hot attach)
  * When it's stopped (warm attach)
  * When the instance is being launched (cold attach).
 

## EBS (Elastic Block Store)

- When you create an EBS volume in an Availability Zone, it is automatically replicated within that zone to prevent data loss due to failure of any single hardware component.

- EBS volumes support live configuration changes while in production which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions.

- In the AWS CLI, you can create a snapshot using this command: create-snapshot.

- Amazon EBS-backed instances can be stopped and restarted unlike Amazon Instance Store-Backed instances which cannot be stopped.

- EBS volumes are resizable.

- You can change the size of the volume even when it is attached to an instance.

- To share an **unencrypted** volume you can mark it as public (this will make it widely avaliable) or mark it as private and then enter the aws accounts with which you want to share it.

- To share an **encrypted** volume you can mark it as private and then enter the AWS accounts with which you want to share it, and give these accounts permissions on the key used to encrypt the snapshot. AWS will not allow making encrypted snapshots public.

- Before you can create EBS volumes from a encrypted shared snapshot you must create a copy of it.

- If an 'A' account, source of an shared encrypted snapshot, revoked 'B' account's rights on CMK encryption key used to encrypted it, 'B' can not use the snapshot, not even a copy already done.  

- Instance store volumes can be added only while launching the instance, and can't be added after the EC2 instance is created.

## ELB (Elastic Load Balancing)

- An Elastic Load Balancer distributes incoming application traffic across multiple EC2 instances, in multiple Availability Zones which increases the fault tolerance of your applications.

- The load balancer routes requests only to the healthy instances. When the load balancer determines that an instance is unhealthy, it stops routing requests to that instance. The load balancer resumes routing requests to the instance when it has been restored to a healthy state.

- You can configure ELB to send the X-forwarded for headers and the web EC2 instances (servers) to filter traffic based on ELB's "X-forwarded-for" headers. You can also filter traffic when you configure TCP listeners and enable proxy protocol. 

- Access Logs, API calls logged by Cloud Trail and Cloud Watch monitoring ELB metrics can be monitored as part of the ELB monitoring.

- Server Order Preference must be enable on ELB such that ELB will determine/select the cipher used for SSL connection during the SSL negotiation process between the ELB and the client.

- If you did not specify a SSL security policy by default the first cipher on the client's list that matches any of the ELB ciphers will be selected.

- Custom security policies and ELB predefined security Policies are the two types of security policies that are suported by ELB.

- If the end user is requesting behind a proxy server then the user should not enable a proxy protocol on ELB.

- If the backend instance to which a session was sticky, fails or becomes unhealthy, the ELB routes the new session/requests (that were stuck before) to a new, healthy, instance and the session is no longer a sticky one.

- ELB’s Cross zone load balancing feature will ensure even distribution of traffic among
the backed EC2 instances registered with the ELB across multiple availability zones.

- TLS 1.2 and SSL 3.0 security protocols are supported by the AWS ELB SSL security policies.

- ELB connection draining will allow the ELB to stop sending any new requests to a backend EC2 instance that is marked as unhealthy by the ELB, without terminating the in-flight sessions to that EC2 instance, while the ELB takes the unhealthy instance out of service.

- ELB and its backend EC2 instances must be in the same VPC.

- For multiple SSL certificates create multiple ELB instances.

- You can enable ELB Pre-Warm if you know your traffic will increase abruptly. You need to conctact AWS. 

-  To implement the stick session feature, you need to have 2 things:

   * An HTTP/HTTPS load balancer.
   * At least one healthy instance in each Availability Zone.

## AS (Auto Scaling)

- AS will always try to rebalance EC2 instances between the AZ's.

- Cyclic or schedule-based scaling is the one that can increase (scale out) at certain date/time and scale in again based on certain date/time.

- Remember that you can't modify a launch configuration after you've created it.

- The cooldown period is a configurable setting for your Auto Scaling group that helps to ensure that it doesn't launch or terminate additional instances before the previous scaling activity takes effect. Its period is 300 seconds by default.

- For Rebalancing, a new instance is launched then the one(s) causing the imbalance get terminated.

- For unhealthy instances, Auto Scaling has to terminate the unhealthy first then launch a new one.

- The ELB and AS must be in the same region.

- AS group schedule policy events must be unique in time.

- Basic monitoring is the default if you created AS launch configuration using AWS console. But if you use AWS CLI the default will be detailed monitoring.

- When you delete an AS Group, its parameters minimum, maximum, and desired capacity are all set to Zero (it shows under AWS Console view as well), hence, it terminates all its EC2 instances.

## RDS (Relational Database Service) and DynamoDB

- When you create or modify your DB instance to run as a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone.

-  The standby instance will not perform any read and write operations while the primary instance is running.

- 6TB is the maximum size of the DB instance.

- Is it not possible to scale the storage down, you can only scale it up.

- Every DB has a weekely maintenence window.

- Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. 

- If you take a snapshot the I/O operations will be suspended for a few minutes while the backup is in progress.

- BYOL and License Included are the type licenses avaliable on ORACLE DB Engine.

- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache that can reduce Amazon DynamoDB response times from milliseconds to microseconds, even at millions of requests per second.

- You can store session state data on both DynamoDB and ElastiCache.

- In Amazon RDS, failover is automatically handled so that you can resume database operations as quickly as possible without administrative intervention in the event that your primary database instance went down. When failing over, Amazon RDS simply flips the canonical name record (CNAME) for your DB instance to point at the standby, which is in turn promoted to become the new primary. 

- Amazon RDS automatically performs a failover in the event of any of the following:

   * Loss of availability in primary Availability Zone 
   * Loss of network connectivity to primary
   * Compute unit failure on primary
   * Storage failure on primary

## S3 (Simple Storage Service)

- Transferring data from an EC2 instance to Amazon S3, Amazon Glacier, Amazon DynamoDB, Amazon SES, Amazon SQS, or Amazon SimpleDB in the same AWS Region has no cost at all.

- By using Versioning and enabling MFA (Multi-Factor Authentication) Delete, you can secure and recover your S3 objects from accidental deletion or overwrite.  

- To encrypty data in S3 buckets you can use AWS S3 server side encryption or encrypty the data at source.

- AWS S3 multipart upload to upload large files.

- S3 will return a HTTP 200 code when an object upload ended successful (and MD5 checksum if SSE was requested).

- Add a random prefix name to optimize uploads.

- You can use Cloud Front to optmize your static site.

- Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and your Amazon S3 bucket.

- You can enable bucket version. 

- Amazon S3 standard storage class provides 99.99% avaliability and 99.999999999% durability to S3 objects.

- Amazon S3 Infrequent Acess class provides 99.9% avaliability and 99.999999999% durability to S3 objects.

- Reduced Redundancy Storage (RRS) provides 99.99% durability and 99.99% availability to S3 objects.

- Glacier provides 99.999999999% durability.

- Expedited, Standard and Bulk are the three archive retrieval method thah can be used to restore archives from Glacier.

- Glacier uses synchronous uploads and asynchronous retrieval.

- AWS S3 replicates your data to multiple facilites within the same region.

- You can use pre-signed URLs to avoid people using your S3 objects for free.

- Here are the prerequisites for routing traffic to a website that is hosted in an Amazon S3 Bucket:

  * An S3 bucket that is configured to host a static website. The bucket must have the same name as your domain or subdomain. For example, if you want to use the subdomain acme.example.com, the name of the bucket must be acme.example.com.
  * A registered domain name. You can use Route53 as your domain registrar, or you can use a different registrar.
  * Route53 as the DNS service for the domain. If you register your domain name by using Route53, we automatically configure Route53 as the DNS service for the domain.

- Amazon S3 supports the following destinations where it can publish events:

   * Amazon Simple Notification Service (Amazon SNS) topic
   * Amazon Simple Queue Service (Amazon SQS) queue
   * AWS Lambda

## CloudTrail

- CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. 

## Budgets

- AWS Budgets gives you the ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed) your budgeted amount.

## CloudFormation

- AWS CloudFormation provides a common language for you to describe and provision all the infrastructure resources in your cloud environment. 

- There is no additional charge for AWS CloudFormation. You only pay for the AWS resources that are created.

## EMR

- Amazon EMR is a web service that enables businesses, researchers, data analysts, and developers to easily and cost-effectively process vast amounts of data.

## CloudWatch 

- CloudWatch has available Amazon EC2 Metrics for you to use for monitoring CPU utilization, Network utilization, Disk performance and Disk Reads/Writes. In case that you need to monitor the below items, you need to prepare a custom metric using a Perl or other shell script, as there are no ready to use metrics for these:

   * Memory utilization
   
   * disk swap utilization
   
   * disk space utilization
   
   * page file utilization
   
   * log collection

## IAM

- There are 2 types of policies in IAM: Identity-Based Policies and Resource-Based Policies.

- One of the best practices in Amazon IAM is to grant least privilege.

- IAM users are created with no permissions by default.

- If a company is using Microsoft Active Directory which implements Security Assertion Markup Language (SAML),  you can set up a SAML-Based Federation for API Access to your AWS cloud. In this way, you can easily connect to AWS using the login credentials of your on-premise network.

- The best practice in handling API Credentials is to create a new role in the Identity Access Management (IAM) service and then assign it to a specific EC2 instance. 

- AWS Security Token Service (AWS STS) is the service that you can use to create and provide trusted users with temporary security credentials that can control access to your AWS resources.

## Kinesis

- A Kinesis data stream stores records from 24 hours by default to a maximum of 168 hours.

## Kinesis Data Firehose

- Amazon Kinesis Data Firehose is the easiest way to load streaming data into data stores and analytics tools. It can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk.

## SNS 

- Amazon SNS supports notifications over multiple transport protocols in order for customers to have broad flexibility of delivery mechanisms.Customers can select one the following transports as part of the subscription requests:HTTP, HTTPS, Email, Email-JSON, SQS and SMS.

## Lambda

- AWS Lambda lets you run code without provisioning or managing servers.

- The AWS Lambda resource limit for ephemeral disk capacity (/tmp space) per invocation is 512 MB.

- AWS Lambda supports Java, Node.js, C#, and Python with support for other languages coming in the future.

- AWS provides a set of fully managed services such as Lambda, API Gateway, DynamoDB and many others that you can use to build and run serverless applications. 

## SQS

- Remember that the messages in the SQS queue will continue to exist even after the EC2 instance has processed it, until you delete that message.

- SQS helps to facilitate horizontal scaling of encoding tasks.

- The maximum message retention in SQS is 14 days.

- It is a durable key-based object store service

- Only FIFO queues can preserve the order of messages and not standard queues.

## SWF

- SWF decision task tells the decider the state of the workflow execution.

## Cloud Front

- Amazon CloudFront is a global content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to your viewers with low latency and high transfer speeds.

## ElastiCache

- Amazon ElastiCache is a web service that makes it easy to deploy, operate, and scale an in-memory data store or cache in the cloud. The service improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory data stores, instead of relying entirely on slower disk-based databases.

## API Gateway

- Amazon API Gateway provides throttling at multiple levels including global and by a service call. Throttling limits can be set for standard rates and bursts. 

## Snowball

- AWS Snowball is a service that accelerates the transfer of large amounts of data into and out of AWS using physical storage appliances, bypassing the Internet.

## Amazon Redshift 

- Amazon Redshift is a fast, fully managed data warehouse that makes it simple and cost-effective to analyze all your data using standard SQL and your existing Business Intelligence (BI) tools. It allows you to run complex analytic queries against petabytes of structured data using sophisticated query optimization, columnar storage on high-performance local disks, and massively parallel query execution.

## AWS IoT Core

- AWS IoT Core is a managed cloud platform that lets connected devices easily and securely interact with cloud applications and other devices. 

## Route53

- To route the traffic from your domain name to an Elastic Load Balancer, you have to use an alias with a type "A" record set.

-  You can create a policy in Route53, such as a Weighted routing policy, to evenly distribute the traffic to 2 or more EC2 instances.

## OpsWorks

- AWS OpsWorks is a configuration management service that provides managed instances of Chef and Puppet. Chef and Puppet are automation platforms that allow you to use code to automate the configurations of your servers. OpsWorks lets you use Chef and Puppet to automate how servers are configured, deployed, and managed across your Amazon EC2 instances or on-premises compute environments. OpsWorks has three offerings - AWS Opsworks for Chef Automate, AWS OpsWorks for Puppet Enterprise, and AWS OpsWorks Stacks.

## Storage Gateway

- The AWS Storage Gateway service helps customers seamlessly integrate existing on-premises applications, infrastructure, and data with the AWS Cloud.
