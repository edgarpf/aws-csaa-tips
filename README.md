# AWS Certified Solutions Architect – Associate(2018) Tips
Tips and hints for anyone trying to take AWS Certified Solutions Architect – Associate(2018) exam. Great for review before the exam. Feel free to make a PR and improve the content.

## EBS (Elastic Block Store)

- To share an **unencrypted** volume you can mark it as public (this will make it widely avaiable) or mark it as private and then enter the aws accounts with which you want to share it.

- To share an **encrypted** volume you can mark it as private and then enter the AWS accounts with which you want to share it, and give these accounts permissions on the key used to encrypt the snapshot. AWS will not allow making encrypted snapshots public.

- Before you can create EBS volumes from a encrypted shared snapshot you must create a copy of it.

- If an 'A' account, source of an shared encrypted snapshot, revoked 'B' account's rights on CMK encryption key used to encrypted it, 'B' can not use the snapshot, not even a copy.  

- Instance store volumes can be added only while launching the instance, and can't be added after the EC2 instance is created.

## ELB (Elastic Load Balancing)

- You can configure ELB to send the X-forwarded for headers and the web EC2 instances (servers) to filter traffic based on ELB's "X-forwarded-for" headers.

- Access Logs, API calls logged by Cloud Trail and Cloud Watch monitoring ELB metrics can be monitored as part of the ELB monitoring.
