# Retired finding types<a name="guardduty_finding-types-retired"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document history for Amazon GuardDuty](doc-history.md)\.

In the current release of GuardDuty, the following finding types are retired \(no longer generated\)\. You CANNOT reactivate retired GuardDuty findings types\. 

**Topics**
+ [Impact:S3/PermissionsModification\.Unusual](#impact-s3-permissionsmodificationunusual)
+ [Impact:S3/ObjectDelete\.Unusual](#impact-s3-objectdeleteunusual)
+ [Discovery:S3/BucketEnumeration\.Unusual](#discovery-s3-bucketenumerationunusual)
+ [Persistence:IAMUser/NetworkPermissions](#persistence-iam-networkpermissions)
+ [Persistence:IAMUser/ResourcePermissions](#persistence-iam-resourcepermissions)
+ [Persistence:IAMUser/UserPermissions](#persistence-iam-userpermissions)
+ [PrivilegeEscalation:IAMUser/AdministrativePermissions](#privilegeescalation-iam-administrativepermissions)
+ [Recon:IAMUser/NetworkPermissions](#recon-iam-networkpermissions)
+ [Recon:IAMUser/ResourcePermissions](#recon-iam-resourcepermissions)
+ [Recon:IAMUser/UserPermissions](#recon-iam-userpermissions)
+ [ResourceConsumption:IAMUser/ComputeResources](#resourceconsumption-iam-computeresources)
+ [Stealth:IAMUser/LoggingConfigurationModified](#stealth-iam-loggingconfigurationmodified)
+ [UnauthorizedAccess:IAMUser/ConsoleLogin](#unauthorizedaccess-iam-consolelogin)
+ [UnauthorizedAccess:EC2/TorIPCaller](#unauthorizedaccess-ec2-toripcaller)
+ [Backdoor:EC2/XORDDOS](#backdoor2)
+ [Behavior:IAMUser/InstanceLaunchUnusual](#behavior1)
+ [CryptoCurrency:EC2/BitcoinTool\.A](#crypto1)
+ [UnauthorizedAccess:IAMUser/UnusualASNCaller](#unauthorized6)

## Impact:S3/PermissionsModification\.Unusual<a name="impact-s3-permissionsmodificationunusual"></a>

### An IAM entity invoked an API to modify permissions on one or more S3 resources\.<a name="impact-s3-permissionsmodificationunusual_description"></a>

#### <a name="impact-s3-permissionsmodificationunusual_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="impact-s3-permissionsmodificationunusual_full"></a>

This finding informs you that an IAM entity is making API calls designed to modify the permissions on one or more buckets or objects in your AWS environment\. This action may be performed by an attacker to allow information to be shared outside of the account\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="impact-s3-permissionsmodificationunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Impact:S3/ObjectDelete\.Unusual<a name="impact-s3-objectdeleteunusual"></a>

### An IAM entity invoked an API used to delete data in an S3 bucket\.<a name="impact-s3-objectdeleteunusual_description"></a>

#### <a name="impact-s3-objectdeleteunusual_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="impact-s3-objectdeleteunusual_full"></a>

This finding informs you that a specific IAM entity in your AWS environment is making API calls designed to delete data in the listed S3 bucket by deleting the bucket itself\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="impact-s3-objectdeleteunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Discovery:S3/BucketEnumeration\.Unusual<a name="discovery-s3-bucketenumerationunusual"></a>

### An IAM entity invoked an S3 API used to discover S3 buckets within your network\.<a name="discovery-s3-bucketenumerationunusual_description"></a>

#### <a name="discovery-s3-bucketenumerationunusual_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="discovery-s3-bucketenumerationunusual_full"></a>

This finding informs you that an IAM entity has invoked an S3 API to discover S3 buckets in your environment, such as `ListBuckets`\. This type of activity is associated with the discovery stage of an attack wherein an attacker is gathering information to determine if your AWS environment is susceptible to a broader attack\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="discovery-s3-bucketenumerationunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Persistence:IAMUser/NetworkPermissions<a name="persistence-iam-networkpermissions"></a>

### An IAM entity invoked an API commonly used to change the network access permissions for security groups, routes, and ACLs in your AWS account\.<a name="persistence-iam-networkpermissions_description"></a>

#### <a name="persistence-iam-networkpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="persistence-iam-networkpermissions_full"></a>

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
This finding's default severity is Medium\. However, if the API is invoked is using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="persistence-iam-resourcepermissions_full"></a>

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
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="persistence-iam-userpermissions_full"></a>

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. 

This finding is triggered by suspicious changes to the user\-related permissions in your AWS environment, such as when a principal in your AWS environment invokes the `AttachUserPolicy` API with no prior history of doing so\. Attackers may use stolen credentials to create new users, add access policies to existing users, or create access keys to maximize their access to an account, even if their original access point is closed\. For example, the owner of the account might notice that a particular IAM user or password was stolen and delete it from the account\. However, they might not delete other users that were created by a fraudulently created admin principal, leaving their AWS account accessible to the attacker\. 

#### <a name="persistence-iam-userpermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PrivilegeEscalation:IAMUser/AdministrativePermissions<a name="privilegeescalation-iam-administrativepermissions"></a>

### A principal has attempted to assign a highly permissive policy to themselves\.<a name="privilegeescalation-iam-administrativepermissions_description"></a>

#### <a name="privilegeescalation-iam-administrativepermissions_severity"></a>

**Default severity: Low\***

**Note**  
This finding's severity is Low if the attempt at privilege escalation was unsuccessful, and Medium if the attempt at privilege escalation was successful\.

#### <a name="privilegeescalation-iam-administrativepermissions_full"></a>

This finding indicates that a specific IAM entity in your AWS environment is exhibiting behavior that can be indicative of a privilege escalation attack\. This finding is triggered when an IAM user or role attempts to assign a highly permissive policy to themselves\. If the user or role in question is not meant to have administrative privileges, either the user's credentials may be compromised or the role's permissions may not be configured properly\. 

Attackers will use stolen credentials to create new users, add access policies to existing users, or create access keys to maximize their access to an account even if their original access point is closed\. For example, the owner of the account might notice that a particular IAM user or password was stolen and delete it from the account, but might not delete other users that were created by a fraudulently created admin principal, leaving their AWS account still accessible to the attacker\. 

#### <a name="privilegeescalation-iam-administrativepermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/NetworkPermissions<a name="recon-iam-networkpermissions"></a>

### A principal invoked an API commonly used to change the network access permissions for security groups, routes, and ACLs in your AWS account\.<a name="recon-iam-networkpermissions_description"></a>

#### <a name="recon-iam-networkpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="recon-iam-networkpermissions_full"></a>

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
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="recon-iam-resourcepermissions_full"></a>

This finding indicates that a specific principal \(AWS account root user, IAM role, or IAM user\) in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. 

 This finding is triggered when resource access permissions in your AWS account are probed under suspicious circumstances\. For example, if a principal invoked the `DescribeInstances` API with no prior history of doing so\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-resourcepermissions_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/UserPermissions<a name="recon-iam-userpermissions"></a>

### A principal invoked an API commonly used to add, modify, or delete IAM users, groups or policies in your AWS account\.<a name="recon-iam-userpermissions_description"></a>

#### <a name="recon-iam-userpermissions_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="recon-iam-userpermissions_full"></a>

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
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="resourceconsumption-iam-computeresources_full"></a>

This finding is triggered when EC2 instances in the listed account within your AWS environment are launched under suspicious circumstances\. This finding indicates that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline; for example, if a principal \(AWS account root user, IAM role, or IAM user\) invoked the `RunInstances` API with no prior history of doing so\. This might be an indication of an attacker using stolen credentials to steal compute time \(possibly for cryptocurrency mining or password cracking\)\. It can also be an indication of an attacker using an EC2 instance in your AWS environment and its credentials to maintain access to your account\.



#### <a name="resourceconsumption-iam-computeresources_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:IAMUser/LoggingConfigurationModified<a name="stealth-iam-loggingconfigurationmodified"></a>

### A principal invoked an API commonly used to stop CloudTrail Logging, delete existing logs, and otherwise eliminate traces of activity in your AWS account\.<a name="stealth-iam-loggingconfigurationmodified_description"></a>

#### <a name="stealth-iam-loggingconfigurationmodified_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="stealth-iam-loggingconfigurationmodified_full"></a>

This finding is triggered when the logging configuration in the listed AWS account within your environment is modified under suspicious circumstances\. This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline; for example, if a principal \(AWS account root user, IAM role, or IAM user\) invoked the `StopLogging` API with no prior history of doing so\. This can be an indication of an attacker trying to cover their tracks by eliminating any trace of their activity\.

#### <a name="stealth-iam-loggingconfigurationmodified_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/ConsoleLogin<a name="unauthorizedaccess-iam-consolelogin"></a>

### An unusual console login by a principal in your AWS account was observed\.<a name="unauthorizedaccess-iam-consolelogin_description"></a>

#### <a name="unauthorizedaccess-iam-consolelogin_severity"></a>

**Default severity: Medium\***

**Note**  
This finding's default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an instance, the finding's severity is High\.

#### <a name="unauthorizedaccess-iam-consolelogin_full"></a>

This finding is triggered when a console login is detected under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the ConsoleLogin API from a never\-before\-used client or an unusual location\. This could be an indication of stolen credentials being used to gain access to your AWS account, or a valid user accessing the account in an invalid or less secure manner \(for example, not over an approved VPN\)\.

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of login activity using this client application from this specific location\.

#### <a name="unauthorizedaccess-iam-consolelogin_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:EC2/TorIPCaller<a name="unauthorizedaccess-ec2-toripcaller"></a>

### Your EC2 instance is receiving inbound connections from a Tor exit node\.<a name="unauthorizedaccess-ec2-toripcaller_description"></a>

#### <a name="unauthorizedaccess-ec2-toripcaller_severity"></a>

**Default severity: Medium**

#### <a name="unauthorizedaccess-ec2-toripcaller_full"></a>

This finding informs you that an EC2 instance in your AWS environment is receiving inbound connections from a Tor exit node\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This finding can indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="unauthorizedaccess-ec2-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/XORDDOS<a name="backdoor2"></a>

### An EC2 instance is attempting to communicate with an IP address that is associated with XorDDos malware\.<a name="backdoor2_description"></a>

#### <a name="backdoor2_severity"></a>

**Default severity: High**

#### <a name="backdoor2_full"></a>

This finding informs you that an EC2 instance in your AWS environment is attempting to communicate with an IP address that is associated with XorDDos malware\. This EC2 instance might be compromised\. XOR DDoS is Trojan malware that hijacks Linux systems\. To gain access to the system, it launches a brute force attack in order to discover the password to Secure Shell \(SSH\) services on Linux\. After SSH credentials are acquired and the login is successful, it uses root privileges to run a script that downloads and installs XOR DDoS\. This malware is then used as part of a botnet to launch distributed denial of service \(DDoS\) attacks against other targets\.

#### <a name="backdoor2_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Behavior:IAMUser/InstanceLaunchUnusual<a name="behavior1"></a>

### An IAM user launched an EC2 instance of an unusual type\.<a name="behavior1_description"></a>

#### <a name="behavior1_severity"></a>

**Default severity: High**

#### <a name="behavior1_full"></a>

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of launching an EC2 instance of this type\. Your IAM user credentials might be compromised\.

#### <a name="backdoor2_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## CryptoCurrency:EC2/BitcoinTool\.A<a name="crypto1"></a>

### EC2 instance is communicating with Bitcoin mining pools\.<a name="crypto1_description"></a>

#### <a name="crypto1_severity"></a>

**Default severity: High**

This finding informs you that an EC2 instance in your AWS environment is communicating with Bitcoin mining pools\. In the field of cryptocurrency mining, a mining pool is the pooling of resources by miners who share their processing power over a network to split the reward according to the amount of work they contributed to solving a block\. Unless you use this EC2 instance for Bitcoin mining, your EC2 instance might be compromised\. 

#### <a name="crypto1_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:IAMUser/UnusualASNCaller<a name="unauthorized6"></a>

### An API was invoked from an IP address of an unusual network\.<a name="unauthorized6_description"></a>

#### <a name="unauthorized6_severity"></a>

**Default severity: High**

#### <a name="uanuthorized6_full"></a>

This finding informs you that certain activity was invoked from an IP address of an unusual network\. This network was never observed throughout the AWS usage history of the described user\. This activity can include a console login, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, etc\. This can indicate unauthorized access to your AWS resources\. 

#### <a name="unauthorized6_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.