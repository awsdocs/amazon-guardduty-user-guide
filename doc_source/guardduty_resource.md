# ResourceConsumption Finding Types<a name="guardduty_resource"></a>

This section covers the active ResourceConsumption threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [ResourceConsumption:IAMUser/ComputeResources](#resourceconsumption)

## ResourceConsumption:IAMUser/ComputeResources<a name="resourceconsumption"></a>

### Finding description<a name="resourceconsumption_description"></a>

**A principal invoked an API commonly used to launch compute resources like EC2 Instances\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when EC2 instances in your AWS environment are launched under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the RunInstances API\. This might be an indication of an attacker using stolen credentials to steal compute time \(possibly for cryptocurrency mining or password cracking\)\. It can also be an indication of an attacker using an EC2 instance in your AWS environment and its credentials to maintain access to your account\.

### Default severity: Medium<a name="resourceconsumption_severity"></a>

This finding’s default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding’s severity is High\.