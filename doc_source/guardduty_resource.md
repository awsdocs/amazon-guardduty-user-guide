# GuardDuty ResourceConsumption Finding Types<a name="guardduty_resource"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\.

**Topics**
+ [ResourceConsumption:IAMUser/ComputeResources](#resourceconsumption)

## ResourceConsumption:IAMUser/ComputeResources<a name="resourceconsumption"></a>

### Finding description<a name="resourceconsumption_description"></a>

**An IAM user invoked an API commonly used to launch compute resources like EC2 Instances\.**

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when EC2 instances in your AWS environment are launched under suspicious circumstances\. For example, if an IAM user with no prior history of doing so, invoked the RunInstances API\. This might be an indication of an attacker using stolen credentials to steal compute time \(possibly for cryptocurrency mining or password cracking\)\. It can also be an indication of an attacker using an EC2 instance in your AWS environment and its credentials to maintain access to your account\.