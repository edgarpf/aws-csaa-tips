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

## Auto Scaling
