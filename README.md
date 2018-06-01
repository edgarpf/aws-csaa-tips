# AWS Certified Solutions Architect – Associate(2018) Tips

## General

- Tags enable you to categorize your AWS resources in different ways.

## VPC

- In the default VPC, AWS automatically sets up the following for you:

Create a VPC with a size /16 IPv4 CIDR block (172.31.0.0/16). This provides up to 65,536 private IPv4 addresses.

Create a size /20 default subnet in each Availability Zone. This provides up to 4,096 addresses per subnet, a few of which are reserved for our use.

Create an Internet Gateway and connect it to your default VPC.

Create a main route table for your default VPC with a rule that sends all IPv4 traffic destined for the Internet to the Internet gateway.

Create a default security group and associate it with your default VPC.

Create a default network access control list (ACL) and associate it with your default VPC.

Associate the default DHCP options set for your AWS account with your default VPC.

- Changes made in a Security Group is immediately implemented to all associated EC2 instances.

- The allowed block size is between a /28 netmask and /16 netmask.

- The CIDR block must not overlap with any existing CIDR block that's associated with the VPC.

- You cannot increase or decrease the size of an existing CIDR block.

- The first four IP addresses and the last IP address in each subnet CIDR block are not available for you to use, and cannot be assigned to an instance.

- In an ideal and secure VPC architecture, you launch the web servers or elastic load balancers in the public subnet and the database servers in the private subnet.

## EC2

- The instance retains its associated Elastic IP addresses if it is in the EC2-VPC platform and not on EC2-Classic.

- If you use PuTTY to connect to your instance via SSH and get either of the following errors, Error: Server refused our key or Error: No supported authentication methods available, verify that you are connecting with the appropriate user name for your AMI. You should also verify that your private key (.pem) file has been correctly converted to the format recognized by PuTTY (.ppk).

- By default, your instance is enabled for basic monitoring. Data is available automatically in 5-minute periods at no charge.

## EBS (Elastic Block Store)

- Amazon EBS-backed instances can be stopped and restarted unlike Amazon Instance Store-Backed instances which cannot be stopped.

- EBS volumes are resizable.

- You can change the size of the volume even when it is attached to an instance.

- To share an **unencrypted** volume you can mark it as public (this will make it widely avaliable) or mark it as private and then enter the aws accounts with which you want to share it.

- To share an **encrypted** volume you can mark it as private and then enter the AWS accounts with which you want to share it, and give these accounts permissions on the key used to encrypt the snapshot. AWS will not allow making encrypted snapshots public.

- Before you can create EBS volumes from a encrypted shared snapshot you must create a copy of it.

- If an 'A' account, source of an shared encrypted snapshot, revoked 'B' account's rights on CMK encryption key used to encrypted it, 'B' can not use the snapshot, not even a copy already done.  

- Instance store volumes can be added only while launching the instance, and can't be added after the EC2 instance is created.

## ELB (Elastic Load Balancing)

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

## AS (Auto Scaling)

- AS will always try to rebalance EC2 instances between the AZ's.

- Cyclic or schedule-based scaling is the one that can increase (scale out) at certain date/time and scale in again based on certain date/time.

- For Rebalancing, a new instance is launched then the one(s) causing the imbalance get terminated.

- For unhealthy instances, Auto Scaling has to terminate the unhealthy first then launch a new one.

- The ELB and AS must be in the same region.

- AS group schedule policy events must be unique in time.

- Basic monitoring is the default if you created AS launch configuration using AWS console. But if you use AWS CLI the default will be detailed monitoring.

- When you delete an AS Group, its parameters minimum, maximum, and desired capacity are all set to Zero (it shows under AWS Console view as well), hence, it terminates all its EC2 instances.

## RDS (Relational Database Service) and DynamoDB

- When you create or modify your DB instance to run as a Multi-AZ deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone.

- 6TB is the maximum size of the DB instance.

- Is it not possible to scale the storage down, you can only scale it up.

- Every DB has a weekely maintenence window.

- If you take a snapshot the I/O operations will be suspended for a few minutes while the backup is in progress.

- BYOL and License Included are the type licenses avaliable on ORACLE DB Engine.

- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache that can reduce Amazon DynamoDB response times from milliseconds to microseconds, even at millions of requests per second.

## S3 (Simple Storage Service)

- Transferring data from an EC2 instance to Amazon S3, Amazon Glacier, Amazon DynamoDB, Amazon SES, Amazon SQS, or Amazon SimpleDB in the same AWS Region has no cost at all.

- By using Versioning and enabling MFA (Multi-Factor Authentication) Delete, you can secure and recover your S3 objects from accidental deletion or overwrite.  

- To encrypty data in S3 buckets you can use AWS S3 server side encryption or encrypty the data at source.

- AWS S3 multipart upload to upload large files.

- S3 will return a HTTP 200 code when an object upload ended successful (and MD5 checksum if SSE was requested).

- Add a random prefix name to optimize uploads.

- You can use Cloud Front to optmize your static site.

- You can enable bucket version. 

- Amazon S3 standard storage class provides 99.99% avaliability and 99.999999999% durability to S3 objects.

- Amazon S3 Infrequent Acess class provides 99.9% avaliability and 99.999999999% durability to S3 objects.

- Reduced Redundancy Storage (RRS) provides 99.99% durability and 99.99% availability to S3 objects.

- Glacier provides 99.999999999% durability.

- Expedited, Standard and Bulk are the three archive retrieval method thah can be used to restore archives from Glacier.

- Glacier uses synchronous uploads and asynchronous retrieval.

- AWS S3 replicates your data to multiple facilites within the same region.

- You can use pre-signed URLs to avoid people using your S3 objects for free.

## AWS CloudTrail

- CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. 

## AWS Budgets

- AWS Budgets gives you the ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed) your budgeted amount.

## AWS CloudFormation

- There is no additional charge for AWS CloudFormation. You only pay for the AWS resources that are created.

## Amazon EMR

- Amazon EMR is a web service that enables businesses, researchers, data analysts, and developers to easily and cost-effectively process vast amounts of data.

## CloudWatch 

- CloudWatch has available Amazon EC2 Metrics for you to use for monitoring CPU utilization, Network utilization, Disk performance and Disk Reads/Writes. In case that you need to monitor the below items, you need to prepare a custom metric using a Perl or other shell script, as there are no ready to use metrics for these:

Memory utilization
disk swap utilization
disk space utilization
page file utilization
log collection

## IAM

- There are 2 types of policies in IAM: Identity-Based Policies and Resource-Based Policies.

- If a company is using Microsoft Active Directory which implements Security Assertion Markup Language (SAML),  you can set up a SAML-Based Federation for API Access to your AWS cloud. In this way, you can easily connect to AWS using the login credentials of your on-premise network.

## Amazon Kinesis Data Firehos

- Amazon Kinesis Data Firehose is the easiest way to load streaming data into data stores and analytics tools. It can capture, transform, and load streaming data into Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and Splunk.

## Amazon SNS 

- Amazon SNS supports notifications over multiple transport protocols in order for customers to have broad flexibility of delivery mechanisms.Customers can select one the following transports as part of the subscription requests:HTTP, HTTPS, Email, Email-JSON, SQS and SMS.
