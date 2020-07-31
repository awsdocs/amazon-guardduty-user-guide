# GuardDuty IAM finding types<a name="guardduty_finding-types-iam"></a>

The following findings are specific to IAM entities and access keys and always have a Resource Type of `AccessKey`\. The severity and details of the findings differ based on the finding type\.

For all IAM related findings, it is recommended that you examine the permissions on the entity in question and ensure that this entity follows the best practice of least privilege\. If the activity is unexpected, the credentials may be compromised\. See actions detailed in [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

**Topics**
+ [PenTest:IAMUser/KaliLinux](#pentest-iam-kalilinux)
+ [PenTest:IAMUser/ParrotLinux](#pentest-iam-parrotlinux)
+ [PenTest:IAMUser/PentooLinux](#pentest-iam-pentoolinux)
+ [Persistence:IAMUser/NetworkPermissions](#persistence-iam-networkpermissions)
+ [Persistence:IAMUser/ResourcePermissions](#persistence-iam-resourcepermissions)
+ [Persistence:IAMUser/UserPermissions](#persistence-iam-userpermissions)
+ [Policy:IAMUser/RootCredentialUsage](#policy-iam-rootcredentialusage)
+ [PrivilegeEscalation:IAMUser/AdministrativePermissions](#privilegeescalation-iam-administrativepermissions)
+ [Recon:IAMUser/MaliciousIPCaller](#recon-iam-maliciousipcaller)
+ [Recon:IAMUser/MaliciousIPCaller\.Custom](#recon-iam-maliciousipcallercustom)
+ [Recon:IAMUser/NetworkPermissions](#recon-iam-networkpermissions)
+ [Recon:IAMUser/ResourcePermissions](#recon-iam-resourcepermissions)
+ [Recon:IAMUser/TorIPCaller](#recon-iam-toripcaller)
+ [Recon:IAMUser/UserPermissions](#recon-iam-userpermissions)
+ [ResourceConsumption:IAMUser/ComputeResources](#resourceconsumption-iam-computeresources)
+ [Stealth:IAMUser/CloudTrailLoggingDisabled](#stealth-iam-cloudtrailloggingdisabled)
+ [Stealth:IAMUser/LoggingConfigurationModified](#stealth-iam-loggingconfigurationmodified)
+ [Stealth:IAMUser/PasswordPolicyChange](#stealth-iam-passwordpolicychange)
+ [UnauthorizedAccess:IAMUser/ConsoleLogin](#unauthorizedaccess-iam-consolelogin)
+ [UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](#unauthorizedaccess-iam-consoleloginsuccessb)
+ [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](#unauthorizedaccess-iam-instancecredentialexfiltration)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller](#unauthorizedaccess-iam-maliciousipcaller)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](#unauthorizedaccess-iam-maliciousipcallercustom)
+ [UnauthorizedAccess:IAMUser/TorIPCaller](#unauthorizedaccess-iam-toripcaller)

## PenTest:IAMUser/KaliLinux<a name="pentest-iam-kalilinux"></a>

### An API was invoked from a Kali Linux EC2 machine\.<a name="pentest-iam-kalilinux_description"></a>

#### <a name="pentest-iam-kalilinux_severity"></a>

**Default severity: Medium**

This finding informs you that a machine running Kali Linux is making API calls using credentials that belong to the listed AWS account in your environment\. Kali Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\. 

#### <a name="pentest-iam-kalilinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PenTest:IAMUser/ParrotLinux<a name="pentest-iam-parrotlinux"></a>

### An API was invoked from a Parrot Security Linux machine\.<a name="pentest-iam-parrotlinux_description"></a>

#### <a name="pentest-iam-parrotlinux_severity"></a>

**Default severity: Medium**

This finding informs you that a machine running Parrot Security Linux is making API calls using credentials that belong to the listed AWS account in your environment\. Parrot Security Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-iam-parrotlinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PenTest:IAMUser/PentooLinux<a name="pentest-iam-pentoolinux"></a>

### An API was invoked from a Pentoo Linux machine\.<a name="pentest-iam-pentoolinux_description"></a>

#### <a name="pentest-iam-pentoolinux_severity"></a>

**Default severity: Medium**

This finding informs you that a machine running Pentoo Linux is making API calls using credentials that belong to the listed AWS account in your environment\. Pentoo Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-iam-pentoolinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Persistence:IAMUser/NetworkPermissions<a name="persistence-iam-networkpermissions"></a>

### An IAM entity invoked an API commonly used to change the network access permissions for security groups, routes, and ACLs in your AWS account\.<a name="persistence-iam-networkpermissions_description"></a>

#### <a name="persistence-iam-networkpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\.

This finding is triggered when network configuration settings are changed under suspicious circumstances, such as when a principal invokes the `CreateSecurityGroup` API with no prior history of doing so\. Attackers often attempt to change security groups to allow certain inbound traffic on various ports to improve their ability to access an EC2 instance\.

#### <a name="persistence-iam-networkpermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Persistence:IAMUser/ResourcePermissions<a name="persistence-iam-resourcepermissions"></a>

### A principal invoked an API commonly used to change the security access policies of various resources in your AWS account\.<a name="persistence-iam-resourcepermissions_description"></a>

#### <a name="persistence-iam-resourcepermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked is using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. 

This finding is triggered when a change is detected to policies or permissions attached to AWS resources, such as when a principal in your AWS environment invokes the `PutBucketPolicy` API with no prior history of doing so\. Some services, such as Amazon S3, support resource\-attached permissions that grant one or more principals access to the resource\. With stolen credentials, attackers can change the policies attached to a resource in order to gain access to that resource\.

#### <a name="persistence-iam-resourcepermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Persistence:IAMUser/UserPermissions<a name="persistence-iam-userpermissions"></a>

### A principal invoked an API commonly used to add, modify, or delete IAM users, groups or policies in your AWS account\.<a name="persistence-iam-userpermissions_description"></a>

#### <a name="persistence-iam-userpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. 

This finding is triggered by suspicious changes to the user\-related permissions in your AWS environment, such as when a principal in your AWS environment invokes the `AttachUserPolicy` API with no prior history of doing so\. Attackers may use stolen credentials to create new users, add access policies to existing users, or create access keys to maximize their access to an account, even if their original access point is closed\. For example, the owner of the account might notice that a particular IAM user or password was stolen and delete it from the account\. However, they might not delete other users that were created by a fraudulently created admin principal, leaving their AWS account accessible to the attacker\. 

#### <a name="persistence-iam-userpermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Policy:IAMUser/RootCredentialUsage<a name="policy-iam-rootcredentialusage"></a>

### An API was invoked using root credentials\.<a name="policy-iam-rootcredentialusage_description"></a>

#### <a name="policy-iam-rootcredentialusage_severity"></a>

**Default severity: Low**

This finding informs you that the root credentials of the listed AWS account in your environment are being used to make requests to AWS services\. It is recommended that users never use root credentials to access AWS services\. Instead, AWS services should be accessed using least privilege temporary credentials from AWS Security Token Service \(STS\)\. For situations where STS is not supported, IAM user credentials are recommended\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

**Note**  
If S3 threat detection is enabled for the account this finding may be generated in response to attempts to run S3 data plane operations on S3 resources using the root credentials of the AWS account\. The API call used will be listed in the finding details\. If S3 threat detection is not enabled this finding can only be triggered by CloudTrail Event log API's\. For more information on S3 threat detection see [Amazon S3 protection in Amazon GuardDuty](s3_detection.md)\.

#### <a name="policy-iam-rootcredentialusage_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PrivilegeEscalation:IAMUser/AdministrativePermissions<a name="privilegeescalation-iam-administrativepermissions"></a>

### A principal has attempted to assign a highly permissive policy to themselves\.<a name="privilegeescalation-iam-administrativepermissions_description"></a>

#### <a name="privilegeescalation-iam-administrativepermissions_severity"></a>

**Default severity: Low\***

**Note**  
This finding's severity is Low if the attempt at privilege escalation was unsuccessful, and Medium if the attempt at privilege escalation was successful\.

This finding indicates that a specific IAM entity in your AWS environment is exhibiting behavior that can be indicative of a privilege escalation attack\. This finding is triggered when an IAM user or role attempts to assign a highly permissive policy to themselves\. If the user or role in question is not meant to have administrative privileges, either the user's credentials may be compromised or the role's permissions may not be configured properly\. Attackers will use stolen credentials to create new users, add access policies to existing users, or create access keys to maximize their access to an account even if their original access point is closed\. For example, the owner of the account might notice that a particular IAM user or password was stolen and delete it from the account, but might not delete other users that were created by a fraudulently created admin principal, leaving their AWS account still accessible to the attacker\. 

#### <a name="privilegeescalation-iam-administrativepermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/MaliciousIPCaller<a name="recon-iam-maliciousipcaller"></a>

### An API was invoked from a known malicious IP address\.<a name="recon-iam-maliciousipcaller_description"></a>

#### <a name="recon-iam-maliciousipcaller_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation that can list or describe AWS resources in an account within your environment was invoked from an IP address that is included on an internal threat list\. GuardDuty generates findings based off of third\-party partner threat lists\. The threat list used to generate this finding will be listed in the finding's details\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-maliciousipcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/MaliciousIPCaller\.Custom<a name="recon-iam-maliciousipcallercustom"></a>

### An API was invoked from a known malicious IP address\.<a name="recon-iam-maliciousipcallercustom_description"></a>

#### <a name="recon-iam-maliciousipcallercustom_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation that can list or describe AWS resources in an account within your environment was invoked from an IP address that is included on a custom threat list\. The threat list used will be listed in the finding's details\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/NetworkPermissions<a name="recon-iam-networkpermissions"></a>

### A principal invoked an API commonly used to change the network access permissions for security groups, routes, and ACLs in your AWS account\.<a name="recon-iam-networkpermissions_description"></a>

#### <a name="recon-iam-networkpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. 

This finding is triggered when resource access permissions in your AWS account are probed under suspicious circumstances\. For example, if a principal invoked the `DescribeInstances` API with no prior history of doing so\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-networkpermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/ResourcePermissions<a name="recon-iam-resourcepermissions"></a>

### A principal invoked an API commonly used to change the security access policies of various resources in your AWS account\.<a name="recon-iam-resourcepermissions_description"></a>

#### <a name="recon-iam-resourcepermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. 

 This finding is triggered when resource access permissions in your AWS account are probed under suspicious circumstances\. For example, if a principal invoked the `DescribeInstances` API with no prior history of doing so\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-resourcepermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/TorIPCaller<a name="recon-iam-toripcaller"></a>

### An API was invoked from a Tor exit node IP address\.<a name="recon-iam-toripcaller_description"></a>

#### <a name="recon-iam-toripcaller_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation that can list or describe AWS resources in an account within your environment was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. An attacker would use Tor to mask their true identity\.

#### <a name="recon-iam-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/UserPermissions<a name="recon-iam-userpermissions"></a>

### A principal invoked an API commonly used to add, modify, or delete IAM users, groups or policies in your AWS account\.<a name="recon-iam-userpermissions_description"></a>

#### <a name="recon-iam-userpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding is triggered when user permissions in your AWS environment are probed under suspicious circumstances\. For example, if a principal \(AWS account root user, IAM role, or IAM user\) invoked the `ListInstanceProfilesForRole` API with no prior history of doing so\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

This finding indicates that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API in this way\.

#### <a name="recon-iam-userpermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## ResourceConsumption:IAMUser/ComputeResources<a name="resourceconsumption-iam-computeresources"></a>

### A principal invoked an API commonly used to launch Compute resources like EC2 Instances\.<a name="resourceconsumption-iam-computeresources_description"></a>

#### <a name="resourceconsumption-iam-computeresources_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding is triggered when EC2 instances in the listed account within your AWS environment are launched under suspicious circumstances\. This finding indicates that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline; for example, if a principal \(AWS account root user, IAM role, or IAM user\) invoked the `RunInstances` API with no prior history of doing so\. This might be an indication of an attacker using stolen credentials to steal compute time \(possibly for cryptocurrency mining or password cracking\)\. It can also be an indication of an attacker using an EC2 instance in your AWS environment and its credentials to maintain access to your account\.

#### <a name="resourceconsumption-iam-computeresources_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:IAMUser/CloudTrailLoggingDisabled<a name="stealth-iam-cloudtrailloggingdisabled"></a>

### AWS CloudTrail trail was disabled\.<a name="stealth-iam-cloudtrailloggingdisabled_description"></a>

#### <a name="stealth-iam-cloudtrailloggingdisabled_severity"></a>

**Default severity: Low**

This finding informs you that a CloudTrail trail within your AWS environment was disabled\. This can be an attacker's attempt to disable logging to cover their tracks by eliminating any trace of their activity while gaining access to your AWS resources for malicious purposes\. This finding can be triggered by a successful deletion or update of a trail\. This finding can also be triggered by a successful deletion of an S3 bucket that stores the logs from a trail that is associated with GuardDuty\.

#### <a name="stealth-iam-cloudtrailloggingdisabled_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:IAMUser/LoggingConfigurationModified<a name="stealth-iam-loggingconfigurationmodified"></a>

### A principal invoked an API commonly used to stop CloudTrail Logging, delete existing logs, and otherwise eliminate traces of activity in your AWS account\.<a name="stealth-iam-loggingconfigurationmodified_description"></a>

#### <a name="stealth-iam-loggingconfigurationmodified_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding is triggered when the logging configuration in the listed AWS account within your environment is modified under suspicious circumstances\. This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline; for example, if a principal \(AWS account root user, IAM role, or IAM user\) invoked the `StopLogging` API with no prior history of doing so\. This can be an indication of an attacker trying to cover their tracks by eliminating any trace of their activity\.

#### <a name="stealth-iam-loggingconfigurationmodified_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:IAMUser/PasswordPolicyChange<a name="stealth-iam-passwordpolicychange"></a>

### Account password policy was weakened\.<a name="stealth-iam-passwordpolicychange_description"></a>

#### <a name="stealth-iam-passwordpolicychange_severity"></a>

**Default severity: Low**

The AWS account password policy was weakened on the listed account within your AWS environment\. For example, it was deleted or updated to require fewer characters, not require symbols and numbers, or required to extend the password expiration period\. This finding can also be triggered by an attempt to update or delete your AWS account password policy\. The AWS account password policy defines the rules that govern what kinds of passwords can be set for your IAM users\. A weaker password policy permits the creation of passwords that are easy to remember and potentially easier to guess, thereby creating a security risk\.

#### <a name="stealth-iam-passwordpolicychange_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/ConsoleLogin<a name="unauthorizedaccess-iam-consolelogin"></a>

### An unusual console login by a principal in your AWS account was observed\.<a name="unauthorizedaccess-iam-consolelogin_description"></a>

#### <a name="unauthorizedaccess-iam-consolelogin_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding's severity is High\.

This finding is triggered when a console login is detected under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the ConsoleLogin API from a never\-before\-used client or an unusual location\. This could be an indication of stolen credentials being used to gain access to your AWS account, or a valid user accessing the account in an invalid or less secure manner \(for example, not over an approved VPN\)\.

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of login activity using this client application from this specific location\.

#### <a name="unauthorizedaccess-iam-consolelogin_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B<a name="unauthorizedaccess-iam-consoleloginsuccessb"></a>

### Multiple worldwide successful console logins were observed\.<a name="unauthorizedaccess-iam-consoleloginsuccessb_description"></a>

#### <a name="unauthorizedaccess-iam-consoleloginsuccessb_severity"></a>

**Default severity: Medium**

This finding informs you that multiple successful console logins for the same IAM user were observed around the same time in various geographical locations\. Such anomalous and risky access location patterns indicate potential unauthorized access to your AWS resources\. 

#### <a name="unauthorizedaccess-iam-consoleloginsuccessb_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration<a name="unauthorizedaccess-iam-instancecredentialexfiltration"></a>

### Credentials that were created exclusively for an EC2 instance through an Instance launch role are being used from an external IP address\.<a name="unauthorizedaccess-iam-instancecredentialexfiltration_description"></a>

#### <a name="unauthorizedaccess-iam-instancecredentialexfiltration_severity"></a>

**Default severity: High**

This finding informs you of attempts to run AWS API operations from a host outside of EC2, using temporary AWS credentials that were created on an EC2 instance in your AWS environment\. The listed EC2 instance might be compromised, and the temporary credentials from this instance might have been exfiltrated to a remote host outside of AWS\. AWS does not recommend redistributing temporary credentials outside of the entity that created them \(for example, AWS applications, EC2, or Lambda\)\. However, authorized users can export credentials from their EC2 instances to make legitimate API calls\. To rule out a potential attack and verify the legitimacy of the activity, contact the IAM user to whom these credentials are assigned\.

**Note**  
If S3 threat detection is enabled for the account this finding may be generated in response to attempts to run S3 data plane operations on the S3 resources using EC2 credentials\. The API call used will be listed in the finding details\. If S3 threat detection is not enabled this finding can only be triggered by CloudTrail Event log API's\. For more information on S3 threat detection see [Amazon S3 protection in Amazon GuardDuty](s3_detection.md)\.

#### <a name="unauthorizedaccess-iam-instancecredentialexfiltration_remediation"></a>

**Remediation recommendations:**

This finding is generated when Amazon VPC networking is configured to route internet traffic such that it egresses from an on\-premises gateway rather than from a VPC Internet Gateway \(IGW\)\. Common configurations, such as using AWS Direct Connect, [AWS Outposts](https://docs.aws.amazon.com/outposts/latest/userguide/), or VPC VPN connections, can result in traffic routed this way\. If this is expected behavior, it's recommended that you use suppression rules in GuardDuty and create a rule that consists of two filter criteria\. The first criteria is **finding type**, which should be `UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration`\. The second filter criteria is either the IP address or the ASN of your on\-premises internet gateway\. For IP\-based filters, use the **API caller IPv4 Address** criteria\. For ASN based filters, use either the **API caller ASN name** or **API caller ASN ID**\. To learn more about creating suppression rules see [Suppression rules](findings_suppression-rule.md)

## UnauthorizedAccess:IAMUser/MaliciousIPCaller<a name="unauthorizedaccess-iam-maliciousipcaller"></a>

### An API was invoked from a known malicious IP address\.<a name="unauthorizedaccess-iam-maliciousipcaller_description"></a>

#### <a name="unauthorizedaccess-iam-maliciousipcaller_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges\) was invoked from a known malicious IP address\. This can indicate unauthorized access to AWS resources within your environment\.

#### <a name="unauthorizedaccess-iam-maliciousipcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom<a name="unauthorizedaccess-iam-maliciousipcallercustom"></a>

### An API was invoked from an IP address on a custom threat list\.<a name="unauthorizedaccess-iam-maliciousipcallercustom_description"></a>

#### <a name="unauthorizedaccess-iam-maliciousipcallercustom_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify AWS privileges\) was invoked from an IP address that is included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can indicate unauthorized access to your AWS resources within your environment\.

#### <a name="unauthorizedaccess-iam-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/TorIPCaller<a name="unauthorizedaccess-iam-toripcaller"></a>

### An API was invoked from a Tor exit node IP address\.<a name="unauthorizedaccess-iam-toripcaller_description"></a>

#### <a name="unauthorizedaccess-iam-toripcaller_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, or modify your AWS privileges\) was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="unauthorizedaccess-iam-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.