# How Amazon GuardDuty Uses Its Data Sources<a name="guardduty_data-sources"></a>

To detect unauthorized and unexpected activity in your AWS environment, GuardDuty analyzes and processes data from AWS CloudTrail event logs, VPC Flow Logs, and DNS logs\. While in transit from these data sources to GuardDuty, all of the log data is encrypted\. GuardDuty extracts various fields from these logs for profiling and anomaly detection, and then discards the logs\.

The following sections describe the details of how GuardDuty uses each supported data source\.

**Topics**
+ [AWS CloudTrail event logs](#guardduty_cloudtrail)
+ [VPC Flow Logs](#guardduty_vpc)
+ [DNS logs](#guardduty_dns)

## AWS CloudTrail event logs<a name="guardduty_cloudtrail"></a>

AWS CloudTrail provides you with a history of AWS API calls for your account, including API calls made using the AWS Management Console, the AWS SDKs, the command line tools, and higher\-level AWS services\. CloudTrail also allows you to identify which users and accounts called AWS APIs for services that support CloudTrail, the source IP address that the calls were made from, and when the calls occurred\. For more information, see the [AWS CloudTrail User Guide](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

You can configure CloudTrail trails to log management events and/or data events\. Management events provide insight into management operations that are performed on resources in your AWS account\. For example, configuring security \(IAM AttachRolePolicy API operations\), registering devices \(Amazon EC2 CreateDefaultVpc API operations\), configuring rules for routing data \(Amazon EC2 CreateSubnet API operations\), or setting up logging \(AWS CloudTrail CreateTrail API operations\)\. Data events provide insight into the resource operations performed on or within a resource\. For example, Amazon S3 object\-level API activity \(GetObject, DeleteObject, and PutObject API operations\) or AWS Lambda function execution activity \(the Invoke API\)\. For more information, see [Logging Data and Management Events for Trails](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-management-and-data-events-with-cloudtrail.html)\.

Currently, GuardDuty only analyzes CloudTrail management events\. If you have CloudTrail configured to log data events, there will be a difference between GuardDuty analysis based on CloudTrail data and the logs that CloudTrail itself is delivering\.

Another important detail about GuardDuty's usage of CloudTrail as a data source is the handling and processing of CloudTrail's global events\. For most services, events are recorded in the Region where the action occurred\. For global services such as AWS IAM, AWS STS, Amazon CloudFront, and Route 53, events are delivered to any trail that includes global services, and are logged as occurring in the US East \(N\. Virginia\) Region\. For more information, see [About Global Service Events](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-concepts.html#cloudtrail-concepts-global-service-events)\.

GuardDuty processes all events that come into a Region, including global events that CloudTrail sends to all Regions\. This allows GuardDuty to maintain user and role profiles in each Region and enables it to accurately detect credentials that are being maliciously used across Regions\.

We highly recommend that you enable GuardDuty in all supported AWS Regions\. This enables GuardDuty to generate findings about unauthorized or unusual activity even in Regions that you are not actively using\. This also enables GuardDuty to monitor AWS CloudTrail events for global AWS services\. If GuardDuty is not enabled in all supported Regions, its ability to detect activity that involves global services is reduced\.

## VPC Flow Logs<a name="guardduty_vpc"></a>

VPC Flow Logs capture information about the IP traffic going to and from Amazon EC2 network interfaces in your VPC\. For more information, see [VPC Flow Logs](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html)\.

When you enable GuardDuty, it immediately starts analyzing your VPC Flow Logs data\. It consumes VPC Flow Log events directly from the VPC Flow Logs feature through an independent and duplicative stream of flow logs\. This process does not affect any existing flow log configurations that you might have\. 

GuardDuty doesn't manage your flow logs or make them accessible in your account\. To manage access and retention of your flow logs, you must configure the VPC Flow Logs feature\. 

There is no additional charge for GuardDuty access to flow logs\. However, enabling flow logs for retention or use in your account falls under existing pricing\. For more information, see [Working With Flow Logs](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html#working-with-flow-logs)\.

## DNS logs<a name="guardduty_dns"></a>

If you use AWS DNS resolvers for your EC2 instances \(the default setting\), then GuardDuty can access and process your request and response DNS logs through the internal AWS DNS resolvers\. If you are using a 3rd party DNS resolver, for example, OpenDNS or GoogleDNS, or if you set up your own DNS resolvers, then GuardDuty cannot access and process data from this data source\.