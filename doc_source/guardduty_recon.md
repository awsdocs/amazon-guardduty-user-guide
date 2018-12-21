# GuardDuty Recon Finding Types<a name="guardduty_recon"></a>

This section covers the active Recon threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Recon:EC2/PortProbeUnprotectedPort](#recon6)
+ [Recon:IAMUser/TorIPCaller](#recon1)
+ [Recon:IAMUser/MaliciousIPCaller\.Custom](#recon2)
+ [Recon:IAMUser/MaliciousIPCaller](#recon3)
+ [Recon:EC2/Portscan](#recon5)
+ [Recon:IAMUser/NetworkPermissions](#recon7)
+ [Recon:IAMUser/ResourcePermissions](#recon8)
+ [Recon:IAMUser/UserPermissions](#recon9)

## Recon:EC2/PortProbeUnprotectedPort<a name="recon6"></a>

### Default severity: Low<a name="recon6_severity"></a>

### Finding description<a name="recon6_description"></a>

**EC2 instance has an unprotected port that is being probed by a known malicious host\. **

This finding informs you that a port on an EC2 instance in your AWS environment is not blocked by a security group, access control list \(ACL\), or an on\-host firewall \(for example, Linux IPChains\), and known scanners on the internet are actively probing it\. If the identified unprotected port is 22 or 3389 and you often connect to this EC2 instance by using SSH/RDP and therefore can't block access to either of these ports, you can still limit exposure by allowing access to these ports only to the IP addresses from your corporate network IP address space\. To restrict access to port 22 on Linux, see [http://docs\.aws\.amazon\.com/AWSEC2/latest/UserGuide/authorizing\-access\-to\-an\-instance\.html](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/authorizing-access-to-an-instance.html)\. To restrict access to port 3389 on Windows, see [http://docs\.aws\.amazon\.com/AWSEC2/latest/WindowsGuide/authorizing\-access\-to\-an\-instance\.html](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/authorizing-access-to-an-instance.html)\.

For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## Recon:IAMUser/TorIPCaller<a name="recon1"></a>

### Default severity: Medium<a name="recon1_severity"></a>

### Finding description<a name="recon1_description"></a>

**An API was invoked from a Tor exit node IP address\. **

This finding informs you that an API operation that can list or describe your AWS resources was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This can be a reconnaissance attack: an anonymous user trying to gather information or gain access to your AWS resources for malicious purposes\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

## Recon:IAMUser/MaliciousIPCaller\.Custom<a name="recon2"></a>

### Default severity: Medium<a name="recon2_severity"></a>

### Finding description<a name="recon2_description"></a>

**An API was invoked from an IP address on a custom threat list\.**

This finding informs you that an API operation that can list or describe your AWS resources was invoked from an IP address that is included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can be a reconnaissance attack: an anonymous user trying to gather information or gain access to your AWS resources for malicious purposes\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

## Recon:IAMUser/MaliciousIPCaller<a name="recon3"></a>

### Default severity: Medium<a name="recon3_severity"></a>

### Finding description<a name="recon3_description"></a>

**An API was invoked from a known malicious IP address\.**

This finding informs you that an API operation that can list or describe your AWS resources was invoked from an IP address that is included on a threat list\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on the custom or internal threat lists\. This can be a reconnaissance attack: an anonymous user trying to gather information or gain access to your AWS resources for malicious purposes\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:EC2/Portscan<a name="recon5"></a>

### Default severity: Medium<a name="recon5_severity"></a>

### Finding description<a name="recon5_description"></a>

**EC2 instance is performing outbound port scans to a remote host\.**

This finding informs you that there is an EC2 instance in your AWS environment that is engaged in a possible port scan attack because it is trying to connect to multiple ports over a short period of time\. The purpose of a port scan attack is to locate open ports to discover what services the machine is running and to identify its operating system\. Your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## Recon:IAMUser/NetworkPermissions<a name="recon7"></a>

### Default severity: Medium<a name="recon7_severity"></a>

### Finding description<a name="recon7_description"></a>

**A principal invoked an API commonly used to discover the network access permissions of existing security groups, ACLs, and routes in your AWS account\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when network configuration settings in your AWS environment are probed under suspicious circumstances\. For example, if a principal in your AWS environment with no prior history of doing so, invoked the DescribeSecurityGroups API\. An attacker might use stolen credentials to perform this reconnaissance of network configuration settings before executing the next stage of their attack by changing network permissions or making use of existing openings in the network configuration\.

## Recon:IAMUser/ResourcePermissions<a name="recon8"></a>

### Default severity: Medium<a name="recon8_severity"></a>

### Finding description<a name="recon8_description"></a>

**A principal invoked an API commonly used to discover the permissions associated with various resources in your AWS account\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when resource access permissions in your AWS account are probed under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the DescribeInstances API\. An attacker might use stolen credentials to perform this reconnaissance of your AWS resources in order to find valuable information or determine the capabilities of the credentials they already have\.

## Recon:IAMUser/UserPermissions<a name="recon9"></a>

### Default severity: Medium<a name="recon9_severity"></a>

### Finding description<a name="recon9_description"></a>

**A principal invoked an API commonly used to discover the users, groups, policies and permissions in your AWS account\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when user permissions in your AWS environment are probed under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the ListInstanceProfilesForRole API\. An attacker might use stolen credentials to perform this reconnaissance of your IAM users and roles in order to determine the capabilities of the credentials they already have or to find more permissive credentials that are vulnerable to lateral movement\.