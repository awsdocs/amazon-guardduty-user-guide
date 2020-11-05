# Concepts and terminology<a name="guardduty_concepts"></a>

As you get started with Amazon GuardDuty, you can benefit from learning about its key concepts\.

**Account**  
A standard Amazon Web Services \(AWS\) account that contains your AWS resources\. You can sign in to AWS with your account and enable GuardDuty\.  
You can also invite other accounts to enable GuardDuty and become associated with your AWS account in GuardDuty\. If your invitations are accepted, your account is designated as the **master** GuardDuty account, and the added accounts become your **member** accounts\. You can then view and manage those accounts' GuardDuty findings on their behalf\.  
Users of the master account can configure GuardDuty as well as view and manage GuardDuty findings for their own account and all of their member accounts\. You can have up to 1000 member accounts in GuardDuty\.  
Users of member accounts can configure GuardDuty as well as view and manage GuardDuty findings in their account \(either through the GuardDuty management console or GuardDuty API\)\. Users of member accounts can't view or manage findings in other members' accounts\.   
An AWS account can't be a GuardDuty master and member account at the same time\. An AWS account can accept only one membership invitation\. Accepting a membership invitation is optional\.  
For more information, see [Managing multiple accounts in Amazon GuardDuty](guardduty_accounts.md)\.

**Detector**  
All GuardDuty findings are associated with a detector, which is an object that represents the GuardDuty service\. The detector is a regional entity, and a unique detector is required in each region GuardDuty operates in\. When you enable GuardDuty in a region a new detector with a unique 32 alphanumeric detector ID is generated in that region\. The detector ID format looks like this:  

```
12abc34d567e8fa901bc2d34e56789f0
```
You can find your detector ID for your current region in the console from the **Settings** pane, or programmatically using the [ListDetectors](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFindings.html#API_ListDetectors) API\.  

In multiple account environments all findings for member accounts roll up to the master account's detector\.
Some GuardDuty functionality is configured through the detector, such as configuring CloudWatch Events notification frequency\.

**Data source**  
The origin or location of a set of data\. To detect unauthorized and unexpected activity in your AWS environment, GuardDuty analyzes and processes data from AWS CloudTrail event logs, VPC Flow Logs, and DNS logs\. For more information, see [How Amazon GuardDuty uses its data sources](guardduty_data-sources.md)\.

**Finding**  
A potential security issue discovered by GuardDuty\. For more information, see [Understanding Amazon GuardDuty findings](guardduty_findings.md)\.  
Findings are displayed in the GuardDuty console and contain a detailed description of the security issue\. You can also retrieve your generated findings by calling the [GetFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFindings.html) and [ListFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFindings.html) API operations\.  
You can also see your GuardDuty findings through Amazon CloudWatch events\. GuardDuty sends findings to Amazon CloudWatch via HTTPS protocol\. For more information, see [Creating custom responses to GuardDuty findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

**Suppression rule**  
Suppression rules allow you to create very specific combinations of attributes to suppress findings\. For example, you can define a rule through the GuardDuty filter to auto\-archive `Recon:EC2/Portscan` from only those instances in a specific VPC, running a specific AMI, or with a specific EC2 tag\. This rule would result in port scan findings being automatically archived from the instances that meet the criteria\. However, it still allows alerting if GuardDuty detects those instances conducting other malicious activity, such as crypto\-currency mining\.  
Suppression rules defined in the GuardDuty master account apply to the GuardDuty member accounts\. GuardDuty member accounts can't modify suppression rules\.  
With auto\-archive rules, GuardDuty still generates all findings\. Suppression rules provide suppression of findings while maintaining a complete and immutable history of all activity\.   
Typically suppression rules are used to hide findings that you have determined as false positives for your environment, and reduce the noise from low\-value findings so you can focus on larger threats\. For more information, see [Suppression rules](findings_suppression-rule.md)

**Trusted IP list**  
A list of trusted IP addresses for highly secure communication with your AWS environment\. GuardDuty does not generate findings based on trusted IP lists\. For more information, see [Working with trusted IP lists and threat lists](guardduty_upload-lists.md)\.

**Threat list**  
A list of known malicious IP addresses\. GuardDuty generates findings based on threat lists\. For more information, see [Working with trusted IP lists and threat lists](guardduty_upload-lists.md)\.
