# What is Amazon GuardDuty?<a name="what-is-guardduty"></a>

Amazon GuardDuty is a continuous security monitoring service that analyzes and processes the following [Data sources](guardduty_data-sources.md#guardduty_data-sources.title): VPC Flow Logs, AWS CloudTrail management event logs, Cloudtrail S3 data event logs, and DNS logs\. It uses threat intelligence feeds, such as lists of malicious IP addresses and domains, and machine learning to identify unexpected and potentially unauthorized and malicious activity within your AWS environment\. This can include issues like escalations of privileges, uses of exposed credentials, or communication with malicious IP addresses, URLs, or domains\. For example, GuardDuty can detect compromised EC2 instances serving malware or mining bitcoin\. It also monitors AWS account access behavior for signs of compromise, such as unauthorized infrastructure deployments, like instances deployed in a Region that has never been used, or unusual API calls, like a password policy change to reduce password strength\.

GuardDuty informs you of the status of your AWS environment by producing security [findings](guardduty_findings.md) that you can view in the GuardDuty console or through [Amazon CloudWatch events](guardduty_findings_cloudwatch.md)\. 

## Pricing for GuardDuty<a name="guardduty_pricing"></a>

For information about GuardDuty pricing, see [Amazon GuardDuty Pricing](http://aws.amazon.com/guardduty/pricing/)\. 

## Accessing GuardDuty<a name="guardduty_access"></a>

You can work with GuardDuty in any of the following ways: 

**GuardDuty Console**  
[https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)  
The console is a browser\-based interface to access and use GuardDuty\.

**AWS SDKs**  
AWS provides software development kits \(SDKs\) that consist of libraries and sample code for various programming languages and platforms \(Java, Python, Ruby, \.NET, iOS, Android, and more\)\. The SDKs provide a convenient way to create programmatic access to GuardDuty\. For information about the AWS SDKs, including how to download and install them, see [Tools for Amazon Web Services](https://aws.amazon.com/tools/)\.

**GuardDuty HTTPS API**  
You can access GuardDuty and AWS programmatically by using the GuardDuty HTTPS API, which lets you issue HTTPS requests directly to the service\. For more information, see the [GuardDuty API reference](https://docs.aws.amazon.com/guardduty/latest/APIReference/)\. 