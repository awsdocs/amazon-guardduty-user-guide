# GuardDuty Unauthorized Finding Types<a name="guardduty_unauthorized"></a>

This section covers the active Unauthorized threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [UnauthorizedAccess:IAMUser/TorIPCaller](#unauthorized1)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](#unauthorized2)
+ [UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](#unauthorized4)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller](#unauthorized5)
+ [UnauthorizedAccess:IAMUser/UnusualASNCaller](#unauthorized6)
+ [UnauthorizedAccess:EC2/TorIPCaller](#unauthorized7)
+ [UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom](#unauthorized8)
+ [UnauthorizedAccess:EC2/SSHBruteForce](#unauthorized9)
+ [UnauthorizedAccess:EC2/RDPBruteForce](#unauthorized10)
+ [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](#unauthorized11)
+ [UnauthorizedAccess:IAMUser/ConsoleLogin](#unauthorized12)
+ [UnauthorizedAccess:EC2/TorClient](#unauthorized13)
+ [UnauthorizedAccess:EC2/TorRelay](#unauthorized14)

## UnauthorizedAccess:IAMUser/TorIPCaller<a name="unauthorized1"></a>

### Default severity: Medium<a name="unauthorized1_severity"></a>

### Finding description<a name="unauthorized1_description"></a>

**An API was invoked from a Tor exit node IP address\.**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, or modify your AWS privileges\) was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker’s true identity\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom<a name="unauthorized2"></a>

### Default severity: Medium<a name="unauthorized2_severity"></a>

### Finding description<a name="unauthorized2_description"></a>

**An API was invoked from an IP address on a custom threat list\.**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, and so on\) was invoked from an IP address that is included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker’s true identity\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B<a name="unauthorized4"></a>

### Default severity: Medium<a name="unauthorized4_severity"></a>

### Finding description<a name="unauthorized4_description"></a>

**Multiple worldwide successful console logins were observed\.**

This finding informs you that multiple successful console logins for the same IAM user were observed around the same time in various geographical locations\. Such anomalous and risky access location pattern indicates potential unauthorized access to your AWS resources\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

**Note**  
This finding is only triggered by the activity of the following IAM identities: root, IAM users, and federated users\. This finding is NOT triggered by the activity of an assumed role\. For more information about IAM identities, see [CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. 

## UnauthorizedAccess:IAMUser/MaliciousIPCaller<a name="unauthorized5"></a>

### Default severity: Medium<a name="unauthorized5_severity"></a>

### Finding description<a name="unauthorized5_description"></a>

**An API was invoked from a known malicious IP address\.**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, and so on\) was invoked from a known malicious IP address\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/UnusualASNCaller<a name="unauthorized6"></a>

### Default severity: High<a name="unauthorized6_severity"></a>

### Finding description<a name="unauthorized6_description"></a>

**An API was invoked from an IP address of an unusual network\.**

This finding informs you that certain activity was invoked from an IP address of an unusual network\. This network was never observed throughout the AWS usage history of the described user\. This activity can include a console login, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, etc\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:EC2/TorIPCaller<a name="unauthorized7"></a>

### Default severity: Medium<a name="unauthorized7_severity"></a>

### Finding description<a name="unauthorized7_description"></a>

**EC2 instance is receiving inbound connections from a Tor exit node\.**

This finding informs you that an EC2 instance in your AWS environment is receiving inbound connections from a Tor exit node\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker’s true identity\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom<a name="unauthorized8"></a>

### Default severity: Medium<a name="unauthorized8_severity"></a>

### Finding description<a name="unauthorized8_description"></a>

**EC2 instance is communicating outbound with a IP address on a custom threat list\.**

This finding informs you that an EC2 instance in your AWS environment is communicating outbound using the TCP protocol with an IP address included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/SSHBruteForce<a name="unauthorized9"></a>

### Default severity: Low<a name="unauthorized9_severity"></a>

### Finding description<a name="unauthorized9_description"></a>

**EC2 instance has been involved in SSH brute force attacks\.**

This finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to SSH services on Linux\-based systems\. This can indicate unauthorized access to your AWS resources\. 

**Note**  
This finding is generated only through GuardDuty monitoring traffic on port 22\. If your SSH services are configured to use other ports, this finding is not generated\.

For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/RDPBruteForce<a name="unauthorized10"></a>

### Default severity: Low<a name="unauthorized10_severity"></a>

### Finding description<a name="unauthorized10_description"></a>

**EC2 instance has been involved in RDP brute force attacks\.**

This finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to RDP services on Windows\-based systems\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration<a name="unauthorized11"></a>

### Default severity: High<a name="unauthorized11_severity"></a>

### Finding description<a name="unauthorized11_description"></a>

**Credentials that were created exclusively for an EC2 instance through an instance launch role are being used from an external IP address\.**

This finding informs you of attempts to run AWS API operations from a host outside of EC2, using temporary AWS credentials that were created on an EC2 instance in your AWS account\. Your EC2 instance might be compromised, and the temporary credentials from this instance might have been exfiltrated to a remote host outside of AWS\. AWS does not recommend redistributing temporary credentials outside of the entity that created them \(for example, AWS applications, EC2, or Lambda\)\. However, authorized users can export credentials from their EC2 instances to make legitimate API calls\. To rule out a potential attack and verify the legitimacy of the activity, contact the IAM user to whom these credentials are assigned\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

This finding is commonly triggered in AWS Direct Connect scenarios where all traffic from EC2 instances is routed into your on\-premises network and out your own firewall, thus appearing to originate from an IP address that is external to EC2\. If it's common practice in your AWS production environment to exfiltrate temporary AWS credentials created on EC2 instances, you can whitelist this finding by adding the IP address listed in the **service\.action\.awsApiCallAction\.remoteIpDetails\.ipAddressV4** field in the finding's JSON to your active trusted IP list\. \(You can view the finding's complete JSON, by selecting the finding in the console, and then choosing **Actions/Export**, or by running the [GetFindings](get-findings.md) API operation\)\. A GuardDuty trusted IP list consists of IP addresses that you have whitelisted for secure communication with your AWS infrastructure and applications\. GuardDuty does not generate findings for IP addresses on trusted IP lists\. For more information, see [Working with Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)

## UnauthorizedAccess:IAMUser/ConsoleLogin<a name="unauthorized12"></a>

### Default severity: Medium<a name="unauthorized12_severity"></a>

### Finding description<a name="unauthorized12_description"></a>

**An unusual console login by an IAM user in your AWS account was observed\. **

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of login activity using this client application from this specific location\. Your IAM user credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when a console login is detected under suspicious circumstances\. For example, if an IAM user with no prior history of doing so, invoked the ConsoleLogin API from a never\-before\-used client or an unusual location\. This could be an indication of stolen credentials being used to gain access to your AWS account, or a valid user accessing the account in an invalid or less secure manner \(for example, not over an approved VPN\)\.

## UnauthorizedAccess:EC2/TorClient<a name="unauthorized13"></a>

### Default severity: High<a name="unauthorized13_severity"></a>

### Finding description<a name="unauthorized13_description"></a>

**EC2 instance is making connections to a Tor Guard or an Authority node\.**

This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor Guard or an Authority node\. Tor is software for enabling anonymous communication\. Tor Guards and Authority nodes act as initial gateways into a Tor network\. This traffic can indicate that this EC2 instance is acting as a client on a Tor network\. A common use for a Tor client is to circumvent network monitoring and filter for access to unauthorized or illicit content\. Tor clients can also generate nefarious Internet traffic, including attacking SSH servers\. This activity can indicate that your EC2 instance is compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/TorRelay<a name="unauthorized14"></a>

### Default severity: High<a name="unauthorized14_severity"></a>

### Finding description<a name="unauthorized14_description"></a>

**EC2 instance is making connections to a Tor network as a Tor relay\. **

This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor network in a manner that suggests that it's acting as a Tor relay\. Tor is software for enabling anonymous communication\. Tor relays increase anonymity of the communication by forwarding the client’s possibly illicit traffic from one Tor relay to another\. If this activity is unexpected, your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.