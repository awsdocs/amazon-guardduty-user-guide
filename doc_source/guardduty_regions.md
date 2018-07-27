# Amazon GuardDuty Supported Regions<a name="guardduty_regions"></a>

Currently, Amazon GuardDuty is supported in the following AWS regions:
+ Asia Pacific \(Mumbai\)
+ Asia Pacific \(Seoul\)
+ Asia Pacific \(Singapore\)
+ Asia Pacific \(Sydney\)
+ Asia Pacific \(Tokyo\)
+ Canada \(Central\)
+ EU \(Frankfurt\)
+ EU \(Ireland\)
+ EU \(London\)
+ EU \(Paris\)
+ US East \(N\. Virginia\)
+ US East \(Ohio\)
+ US West \(N\. California\)
+ US West \(Oregon\)
+ South America \(São Paulo\)
+ AWS GovCloud \(US\)
**Important**  
The following list details the differences for using GuardDuty in the AWS GovCloud \(US\) Region compared to other supported AWS regions\. For more informtion, see the [Amazon GuardDuty topic](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-guardduty.html) in the AWS Gov Cloud \(US\) User Guide\.  
There is no support for using AWS CloudFormation to set up GuardDuty resources in AWS GovCloud \(US\)\. 
You cannot use the Enable GuardDuty StackSet feature to enable GuardDuty in multiple accounts at the same time due to the lack of AWS CloudFormation support\. To bypass this limitation, use the Python scripts described in [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md)\.
Cross\-region data transfer is not supported\.
The following DNS\-related findings types will not be generated in AWS GovCloud \(US\)\.  
Trojan:EC2/BlackholeTraffic\!DNS 
Trojan:EC2/DriveBySourceTraffic\!DNS
Trojan:EC2/DropPoint\!DNS
Backdoor:EC2/C&CActivity\.B\!DNS
CryptoCurrency:EC2/BitcoinTool\.B\!DNS
Trojan:EC2/DGADomainRequest\.B
Trojan:EC2/DNSDataExfiltration
Trojan:EC2/DGADomainRequest\.C\!DNS
Trojan:EC2/PhishingDomainRequest\!DNS 

**Important**  
It is highly recommended that you enable GuardDuty in all supported AWS regions\. This allows GuardDuty to generate findings about unauthorized or unusual activity even in regions that you are not actively using\. This also allows GuardDuty to monitor AWS CloudTrail events for global AWS services such as IAM\.   
If GuardDuty is not enabled in all supported regions, its ability to detect activity that involves global services is reduced\.   
There is little to no additional cost for GuardDuty to monitor a region where you do not have active workloads deployed\.