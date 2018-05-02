# Amazon GuardDuty Terminology and Concepts<a name="guardduty_concepts"></a>

As you get started with Amazon GuardDuty, you can benefit from learning about its key concepts\.

**Account**  
A standard Amazon Web Services \(AWS\) account that contains your AWS resources\. You can sign in to AWS with your account and enable GuardDuty\.  
You can also invite other accounts to enable GuardDuty and become associated with your AWS account in GuardDuty\. If your invitations are accepted, your account is designated as the **master** GuardDuty account, and the added accounts become your **member** accounts\. You can then view and manage those accounts' GuardDuty findings on their behalf\.  
Users of the master account can configure GuardDuty as well as view and manage GuardDuty findings for their own account and all of their member accounts\. You can have up to 1000 member accounts in GuardDuty\.  
Users of member accounts can configure GuardDuty as well as view and manage GuardDuty findings in their account \(either through the GuardDuty management console or GuardDuty API\)\. Users of member accounts can't view or manage findings in other members' accounts\.   
An AWS account can't be a GuardDuty master and member account at the same time\. An AWS account can accept only one membership invitation\. Accepting a membership invitation is optional\.  
For more information, see [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

**Data source**  
The origin or location of a set of data\. To detect unauthorized and unexpected activity in your AWS environment, GuardDuty analyzes and processes data from AWS CloudTrail event logs, VPC Flow Logs, and DNS logs\. For more information, see [How Amazon GuardDuty Uses Its Data Sources](guardduty_data-sources.md)\.

**Finding**  
A potential security issue discovered by GuardDuty\. For more information, see [Amazon GuardDuty Findings](guardduty_findings.md)\.  
Findings are displayed in the GuardDuty console and contain a detailed description of the security issue\. You can also retrieve your generated findings by calling the [GetFindings](get-findings.md) and [ListFindings](list-findings.md) HTTPS API operations\.  
You can also see your GuardDuty findings through Amazon CloudWatch events\. GuardDuty sends findings to Amazon CloudWatch via HTTPS protocol\. For more information, see [Monitoring Amazon GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

**Trusted IP list**  
A list of whitelisted IP addresses for highly secure communication with your AWS environment\. GuardDuty does not generate findings based on trusted IP lists\. For more information, see [Working with Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)\.

**Threat list**  
A list of known malicious IP addresses\. GuardDuty generates findings based on threat lists\. For more information, see [Working with Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)\.