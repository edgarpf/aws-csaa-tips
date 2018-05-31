# AWS Certified Solutions Architect – Associate(2018) Tips

## EBS (Elastic Block Store)

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

## RDS (Relational Database Service)

- 6TB is the maximum size of the DB instance.

- Is it not possible to scale the storage down, you can only scale it up.

- Every DB has a weekely maintenence window.

- If you take a snapshot the I/O operations will be suspended for a few minutes while the backup is in progress.

- BYOL and License Included are the type licenses avaliable on ORACLE DB Engine.

## S3 (Simple Storage Service)

- To encrypty data in S3 buckets you can use AWS S3 server side encryption or encrypty the data at source.

- AWS S3 multipart upload to upload large files.

- S3 will return a HTTP 200 code when an object upload ended successful (and MD5 checksum if SSE was requested).

- Add a random prefix name to optimize uploads.

- You can use Cloud Front to optmize your static site.

- You can enable bucket version. 

- Amazon S3 standard storage class provides 99.99% avaliability and 99.999999999% durability to S3 objects.

- Amazon S3 Infrequent Acess class provides 99.9% avaliability and 99.999999999% durability to S3 objects.

- Glacier provides 99.999999999% durability.

- Expedited, Standard and Bulk are the three archive retrieval method thah can be used to restore archives from Glacier.

- Glacier uses synchronous uploads and asynchronous retrieval.

- AWS S3 replicates your data to multiple facilites within the same region.

- You can use pre-signed URLs to avoid people using your S3 objects for free.
