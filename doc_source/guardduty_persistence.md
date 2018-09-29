# GuardDuty Persistence Finding Types<a name="guardduty_persistence"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\.

**Topics**
+ [Persistence:IAMUser/NetworkPermissions](#persistence1)
+ [Persistence:IAMUser/ResourcePermissions](#persistence2)
+ [Persistence:IAMUser/UserPermissions](#persistence3)

## Persistence:IAMUser/NetworkPermissions<a name="persistence1"></a>

### Finding description<a name="persistence1_description"></a>

**An IAM user invoked an API commonly used to change the network access permissions for security groups, routes, and ACLs in your AWS account\.**

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when network configuration settings are changed under suspicious circumstances\. For example, if an IAM user in your AWS environment with no prior history of doing so, invoked the CreateSecurityGroup API\. Attackers often attempt to change security groups, allowing certain inbound traffic on various ports in order to improve their ability to access the bot they might have planted on your EC2 instance\. 

## Persistence:IAMUser/ResourcePermissions<a name="persistence2"></a>

### Finding description<a name="persistence2_description"></a>

**An IAM user invoked an API commonly used to change the security access policies of various resources in your AWS account\.**

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when a change is detected to policies or permissions attached to AWS resources\. For example, if an IAM user in your AWS environment with no prior history of doing so, invoked the PutBucketPolicy API\. Some services, for example, Amazon S3, support resource\-attached permissions that grant one or more IAM principals access to the resource\. With stolen credentials, attackers can change the policies attached to a resource, granting themselves future access to that resource\.

## Persistence:IAMUser/UserPermissions<a name="persistence3"></a>

### Finding description<a name="persistence3_description"></a>

**An IAM user invoked an API commonly used to add, modify, or delete IAM users, groups or policies in your AWS account\.**

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered by suspicious changes to the user\-related permissions in your AWS environment\. For example, if an IAM user in your AWS environment with no prior history of doing so, invoked the AttachUserPolicy API\. In an effort to maximize their ability to access the account even after they have been discovered, attackers can use stolen credentials to create new users, add access policies to existing users, create access keys, etc\. The owner of the account might notice that a particular IAM user or password was stolen and delete it from the account, but might not delete other users that were created by the fraudulently created admin IAM user, leaving their AWS account still accessible to the attacker\. 