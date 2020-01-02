# Regions and Endpoints<a name="guardduty_regions"></a>

To view the Regions that Amazon GuardDuty is available in, see [Amazon GuardDuty Service Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#guardduty_region)\.

**Important**  
It is highly recommended that you enable GuardDuty in all supported AWS regions\. This allows GuardDuty to generate findings about unauthorized or unusual activity even in regions that you are not actively using\. This also allows GuardDuty to monitor AWS CloudTrail events for global AWS services such as IAM\.   
If GuardDuty is not enabled in all supported regions, its ability to detect activity that involves global services is reduced\. 

If you are using GuardDuty in the AWS GovCloud \(US\), be aware of the following differences between the AWS GovCloud \(US\) Region and standard AWS regions:
+ There is no support for using AWS CloudFormation to set up GuardDuty resources in AWS GovCloud \(US\)\.
+ You cannot use the Enable GuardDuty StackSet feature to enable GuardDuty in multiple accounts at the same time due to the lack of AWS CloudFormation support\. To bypass this limitation, use the Python scripts described in [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.
+ Cross\-region data transfer is not supported\.

  For more information, see the [Amazon GuardDuty topic](https://docs.aws.amazon.com/govcloud-us/latest/UserGuide/govcloud-guardduty.html) in the AWS Gov Cloud \(US\) User Guide\.