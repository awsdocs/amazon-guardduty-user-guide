# Unauthorized Finding Types<a name="guardduty_unauthorized"></a>

This section covers the active Unauthorized threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [UnauthorizedAccess:EC2/MetadataDNSRebind](#ec2-metadatadnsrebind)
+ [UnauthorizedAccess:IAMUser/TorIPCaller](#unauthorized1)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](#unauthorized2)
+ [UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](#unauthorized4)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller](#unauthorized5)
+ [UnauthorizedAccess:EC2/TorIPCaller](#unauthorized7)
+ [UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom](#unauthorized8)
+ [UnauthorizedAccess:EC2/SSHBruteForce](#unauthorized9)
+ [UnauthorizedAccess:EC2/RDPBruteForce](#unauthorized10)
+ [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](#unauthorized11)
+ [UnauthorizedAccess:IAMUser/ConsoleLogin](#unauthorized12)
+ [UnauthorizedAccess:EC2/TorClient](#unauthorized13)
+ [UnauthorizedAccess:EC2/TorRelay](#unauthorized14)

## UnauthorizedAccess:EC2/MetadataDNSRebind<a name="ec2-metadatadnsrebind"></a>

### Finding description<a name="ec2-metadatadnsrebind-description"></a>

**An Amazon EC2 instance is performing DNS lookups that resolve to the instance metadata service\.**

This finding informs you that an EC2 instance in your AWS environment is querying a domain that resolves to the EC2 metadata IP address \(169\.254\.169\.254\)\. A DNS query of this kind may indicate that the instance is a target of a DNS Rebinding technique which can be used to obtain metadata from an EC2 instance, including the IAM credentials associated with the instance\.

DNS Rebinding involves tricking an application running on the EC2 instance to load a return data from a URL, where the domain name in the URL resolves to the EC2 metadata IP address \(169\.254\.169\.254\)\. This causes the application to access EC2 metadata and possibly make it available to the attacker\. 

It is possible to access EC2 metadata using DNS Rebinding only if the EC2 instance is running a vulnerable application that allows injection of URLs, or if a human user accesses the URL in a web browser running on the EC2 instance\.

In response to this finding, you should evaluate whether there is a vulnerable application running on the EC2 instance, or a human user used a browser to access the domain identified in the finding\. If the root cause is a vulnerable application, you should fix the vulnerability\. If it was due to a user browsing the identified domain, you should block the domain or prevent users from accessing it\. If you determine this was related to either case above you should [revoke the session associated with the EC2 instance](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_revoke-sessions.html)\.

Some AWS customers intentionally map the metadata IP address to a domain name on their authoritative DNS servers\. Such customers can implement an archive filter to auto\-archive all findings which have the type of UnauthorizedAccess:EC2/MetaDataDNSRebind and the service\.action\.dnsRequestAction\.domain field is same as the domain name they have mapped to the metadata IP address \(169\.254\.169\.254\)\. To learn more, see [CreateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html)\.

### Default severity: High<a name="ec2-metadatadnsrebind-severity"></a>

## UnauthorizedAccess:IAMUser/TorIPCaller<a name="unauthorized1"></a>

### Finding description<a name="unauthorized1_description"></a>

**An API was invoked from a Tor exit node IP address\.**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, or modify your AWS privileges\) was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker’s true identity\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

### Default severity: Medium<a name="unauthorized1_severity"></a>

## UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom<a name="unauthorized2"></a>

### Finding description<a name="unauthorized2_description"></a>

**An API was invoked from an IP address on a custom threat list\.**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, and so on\) was invoked from an IP address that is included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker’s true identity\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

### Default severity: Medium<a name="unauthorized2_severity"></a>

## UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B<a name="unauthorized4"></a>

### Finding description<a name="unauthorized4_description"></a>

**Multiple worldwide successful console logins were observed\.**

This finding informs you that multiple successful console logins for the same IAM user were observed around the same time in various geographical locations\. Such anomalous and risky access location pattern indicates potential unauthorized access to your AWS resources\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

**Note**  
This finding is only triggered by the activity of the following IAM identities: root, IAM users, and federated users\. This finding is NOT triggered by the activity of an assumed role\. For more information about IAM identities, see [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. 

### Default severity: Medium<a name="unauthorized4_severity"></a>

## UnauthorizedAccess:IAMUser/MaliciousIPCaller<a name="unauthorized5"></a>

### Finding description<a name="unauthorized5_description"></a>

**An API was invoked from a known malicious IP address\.**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, and so on\) was invoked from a known malicious IP address\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

### Default severity: Medium<a name="unauthorized5_severity"></a>

## UnauthorizedAccess:EC2/TorIPCaller<a name="unauthorized7"></a>

### Finding description<a name="unauthorized7_description"></a>

**EC2 instance is receiving inbound connections from a Tor exit node\.**

This finding informs you that an EC2 instance in your AWS environment is receiving inbound connections from a Tor exit node\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker’s true identity\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Medium<a name="unauthorized7_severity"></a>

## UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom<a name="unauthorized8"></a>

### Finding description<a name="unauthorized8_description"></a>

**EC2 instance is communicating outbound with an IP address on a custom threat list\.**

This finding informs you that an EC2 instance in your AWS environment is communicating outbound with an IP address included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Medium<a name="unauthorized8_severity"></a>

## UnauthorizedAccess:EC2/SSHBruteForce<a name="unauthorized9"></a>

### Finding description<a name="unauthorized9_description"></a>

**EC2 instance has been involved in SSH brute force attacks\.**

This finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to SSH services on Linux\-based systems\. This can indicate unauthorized access to your AWS resources\. 

This finding’s severity is low if a brute force attack is aimed at one of your EC2 instances\. This finding’s severity is high if your EC2 instance is being used to perform the brute force attack\. 

**Note**  
This finding is generated only through GuardDuty monitoring traffic on port 22\. If your SSH services are configured to use other ports, this finding is not generated\.

For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Low<a name="unauthorized9_severity"></a>

## UnauthorizedAccess:EC2/RDPBruteForce<a name="unauthorized10"></a>

### Finding description<a name="unauthorized10_description"></a>

**EC2 instance has been involved in RDP brute force attacks\.**

This finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to RDP services on Windows\-based systems\. This can indicate unauthorized access to your AWS resources\.

This finding’s severity is low if a brute force attack is aimed at one of your EC2 instances\. This finding’s severity is high if your EC2 instance is being used to perform the brute force attack\. 

For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Low<a name="unauthorized10_severity"></a>

## UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration<a name="unauthorized11"></a>

### Finding description<a name="unauthorized11_description"></a>

**Credentials that were created exclusively for an EC2 instance through an instance launch role are being used from an external IP address\.**

This finding informs you of attempts to run AWS API operations from a host outside of EC2, using temporary AWS credentials that were created on an EC2 instance in your AWS account\. Your EC2 instance might be compromised, and the temporary credentials from this instance might have been exfiltrated to a remote host outside of AWS\. AWS does not recommend redistributing temporary credentials outside of the entity that created them \(for example, AWS applications, EC2, or Lambda\)\. However, authorized users can export credentials from their EC2 instances to make legitimate API calls\. To rule out a potential attack and verify the legitimacy of the activity, contact the IAM user to whom these credentials are assigned\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is generated when Amazon VPC networking is configured to route Internet traffic such that it egresses from an on\-premise gateway rather than from a VPC Internet Gateway \(IGW\)\. Common configurations, such as using AWS Direct Connect, [AWS Outposts](https://docs.aws.amazon.com/outposts/latest/userguide/), or VPC VPN connections, can result in traffic routed this way\. To suppress this expected behavior, it's recommended that you use the auto\-archiving feature in GuardDuty and create a rule that consists of two filter criteria\. The first criteria is “finding type”, which should be UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration\. The second filter criteria is either the IP address or the ASN of your on\-premise internet gateway\. For IP\-based filters, use the “API caller IPv4 Address” criteria\. For ASN based filters, use either the “API caller ASN name” or “API caller ASN ID”\. GuardDuty still generates findings that match an auto\-archiving filter rule\. However, the rule causes these findings to go directly to the findings archive and not trigger an event for a CloudWatch Events rule or be sent to any other downstream integrations\. To learn more, see [Filtering Findings](guardduty_findings.md#guardduty_filter-findings)\.

### Default severity: High<a name="unauthorized11_severity"></a>

## UnauthorizedAccess:IAMUser/ConsoleLogin<a name="unauthorized12"></a>

### Finding description<a name="unauthorized12_description"></a>

**An unusual console login by a principal in your AWS account was observed\. **

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of login activity using this client application from this specific location\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when a console login is detected under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the ConsoleLogin API from a never\-before\-used client or an unusual location\. This could be an indication of stolen credentials being used to gain access to your AWS account, or a valid user accessing the account in an invalid or less secure manner \(for example, not over an approved VPN\)\.

**Note**  
Unlike UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B, this finding can be triggered by any user type\.

### Default severity: Medium<a name="unauthorized12_severity"></a>

This finding’s default severity is Medium\. However, if a principal logs in to the console using temporary AWS credentials that are created on an Amazon EC2 instance, the finding’s severity is High\.

## UnauthorizedAccess:EC2/TorClient<a name="unauthorized13"></a>

### Finding description<a name="unauthorized13_description"></a>

**EC2 instance is making connections to a Tor Guard or an Authority node\.**

This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor Guard or an Authority node\. Tor is software for enabling anonymous communication\. Tor Guards and Authority nodes act as initial gateways into a Tor network\. This traffic can indicate that this EC2 instance is acting as a client on a Tor network\. A common use for a Tor client is to circumvent network monitoring and filter for access to unauthorized or illicit content\. Tor clients can also generate nefarious Internet traffic, including attacking SSH servers\. This activity can indicate that your EC2 instance is compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="unauthorized13_severity"></a>

## UnauthorizedAccess:EC2/TorRelay<a name="unauthorized14"></a>

### Finding description<a name="unauthorized14_description"></a>

**EC2 instance is making connections to a Tor network as a Tor relay\. **

This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor network in a manner that suggests that it's acting as a Tor relay\. Tor is software for enabling anonymous communication\. Tor relays increase anonymity of the communication by forwarding the client’s possibly illicit traffic from one Tor relay to another\. If this activity is unexpected, your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="unauthorized14_severity"></a>