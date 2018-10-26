# GuardDuty CryptoCurrency Finding Types<a name="guardduty_crypto"></a>

This section covers the active CryptoCurrency threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [CryptoCurrency:EC2/BitcoinTool\.B\!DNS](#crypto3)

## CryptoCurrency:EC2/BitcoinTool\.B\!DNS<a name="crypto3"></a>

### Default severity: Medium<a name="crypto3_severity"></a>

### Finding description<a name="crypto3_description"></a>

**EC2 instance is querying a domain name that is associated with Bitcoin\-related activity\.**

This finding informs you that an EC2 instance in your AWS environment is querying a domain name that is associated with Bitcoin\-related activity\. Bitcoin is a worldwide cryptocurrency and digital payment system\. Besides being created as a reward for Bitcoin mining, bitcoin can be exchanged for other currencies, products, and services\. Unless you use this EC2 instance to mine or manage cryptocurrency or your EC2 instance is involved in blockchain activity, your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.