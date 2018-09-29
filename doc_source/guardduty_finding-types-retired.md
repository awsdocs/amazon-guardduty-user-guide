# GuardDuty Retired Finding Types<a name="guardduty_finding-types-retired"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\.

In the current release of GuardDuty, the following finding types are retired \(no longer generated\)\. You CANNOT reactivate retired GuardDuty findings types\. 

**Topics**
+ [Behavior:IAMUser/InstanceLaunchUnusual](#behavior1)
+ [CryptoCurrency:EC2/BitcoinTool\.A](#crypto1)

## Behavior:IAMUser/InstanceLaunchUnusual<a name="behavior1"></a>

### Finding description<a name="behavior1_description"></a>

**An IAM user launched an EC2 instance of an unusual type\.**

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of launching an EC2 instance of this type\. Your IAM user credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)

## CryptoCurrency:EC2/BitcoinTool\.A<a name="crypto1"></a>

### Finding description<a name="crypto1_description"></a>

**EC2 instance is communicating with Bitcoin mining pools\.**

This finding informs you that an EC2 instance in your AWS environment is communicating with Bitcoin mining pools\. In the field of cryptocurrency mining, a mining pool is the pooling of resources by miners who share their processing power over a network to split the reward according to the amount of work they contributed to solving a block\. Unless you use this EC2 instance for Bitcoin mining, your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.