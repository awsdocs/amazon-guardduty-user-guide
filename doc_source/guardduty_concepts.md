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
The origin or location of a set of data\. To detect unauthorized and unexpected activity in your AWS environment, GuardDuty analyzes and processes data from the following data sources\. The logs from these data sources are stored in the Amazon S3 buckets\. GuardDuty accesses them there using the HTTPS protocol\. While in transit from these data sources to GuardDuty, all of the log data is encrypted\. GuardDuty extracts various fields from these logs for profiling and anomaly detection, and then discards the logs\.   

+ AWS CloudTrail event logs

  AWS CloudTrail provides you with a history of AWS API calls for your account, including API calls made using the AWS Management Console, the AWS SDKs, the command line tools, and higher\-level AWS services\. AWS CloudTrail also allows you to identify which users and accounts called AWS APIs for services that support CloudTrail, the source IP address that the calls were made from, and when the calls occurred\. For more information, see [What is AWS CloudTrail?](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html)
**Important**  
It is highly recommended that you enable GuardDuty in all supported AWS regions\. This allows GuardDuty to generate findings about unauthorized or unusual activity even in regions that you are not actively using\. This also allows GuardDuty to monitor AWS CloudTrail events for global AWS services such as IAM\.   
If GuardDuty is not enabled in all supported regions, its ability to detect activity that involves global services is reduced\.   
There is little to no additional cost for GuardDuty to monitor a region where you do not have active workloads deployed\.

+ VPC Flow Logs

  VPC Flow Logs capture information about the IP traffic going to and from Amazon EC2 network interfaces in your VPC\. For more information, see [VPC Flow Logs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html)\.
**Important**  
When you enable GuardDuty, it immediately starts analyzing your VPC Flow Logs data\. It consumes VPC Flow Log events directly from the VPC Flow Logs feature through an independent and duplicative stream of flow logs\. This process does not affect any existing flow log configurations that you might have\.   
GuardDuty doesn't manage your flow logs or make them accessible in your account\. To manage access and retention of your flow logs, you must configure the VPC Flow Logs feature\.   
There is no additional charge for GuardDuty access to flow logs\. However, enabling flow logs for retention or use in your account falls under existing pricing\. For more information, see [Working With Flow Logs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html#working-with-flow-logs)\.

+ DNS logs

  If you use AWS DNS resolvers for your EC2 instances \(the default setting\), then GuardDuty can access and process your request and response DNS logs through the internal AWS DNS resolvers\. If you are using a 3rd party DNS resolver, for example, OpenDNS or GoogleDNS, or if you set up your own DNS resolvers, then GuardDuty cannot access and process data from this data source\.

**Finding**  
A potential security issue discovered by GuardDuty\. For more information, see [Amazon GuardDuty Findings](guardduty_findings.md)\.  
Findings are displayed in the GuardDuty console and contain a detailed description of the security issue\. You can also retrieve your generated findings by calling the [GetFindings](get-findings.md) and [ListFindings](list-findings.md) HTTPS API operations\.  
You can also see your GuardDuty findings through Amazon CloudWatch events\. GuardDuty sends findings to Amazon CloudWatch via HTTPS protocol\. For more information, see [Monitoring Amazon GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

**Trusted IP list**  
A list of whitelisted IP addresses for highly secure communication with your AWS environment\. GuardDuty does not generate findings based on trusted IP lists\. For more information, see [Uploading Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)\.

**Threat list**  
A list of known malicious IP addresses\. GuardDuty generates findings based on threat lists\. For more information, see [Uploading Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)\.