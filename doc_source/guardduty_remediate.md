# Remediating Security Issues Discovered by GuardDuty<a name="guardduty_remediate"></a>

Amazon GuardDuty generates [findings](guardduty_findings.md) that indicate potential security issues\. In this release of GuardDuty, the potential security issues indicate either a compromised EC2 instance or a set of compromised credentials in your AWS environment\. The following sections describe the recommended remediation steps for either scenario\.

**Topics**
+ [Remediating a Compromised EC2 Instance](#compromised-ec2)
+ [Remediating Compromised AWS Credentials](#compromised-creds)

## Remediating a Compromised EC2 Instance<a name="compromised-ec2"></a>

Follow these recommended steps to remediate a compromised EC2 instance in your AWS environment:
+ Investigate the potentially compromised instance for malware and remove any discovered malware\. You can also refer to the [AWS Marketplace](https://aws.amazon.com/marketplace) for partner products that might help to identify and remove malware\.
+ If you are unable to identify and stop unauthorized activity on your EC2 instance, we recommend that you terminate the compromised EC2 instance and replace it with a new instance as needed\. The following are additional resources for securing your EC2 instances:
  + "Security and Network" section in [Best Practices for Amazon EC2](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html)\.
  + [Amazon EC2 Security Groups for Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) and [Amazon EC2 Security Groups for Windows Instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-network-security.html)\.
  + [Tips for securing your EC2 instances \(Linux\)](https://aws.amazon.com/articles/tips-for-securing-your-ec2-instance/) and [Securing Windows EC2 Instances](https://aws.amazon.com/answers/security/aws-securing-windows-instances/)\.
  + [AWS Security Best Practices](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
+ Browse for further assistance on the AWS developer forums: [https://forums\.aws\.amazon\.com/index\.jspa](https://forums.aws.amazon.com/index.jspa) 
+ If you are a Premium Support package subscriber, you can request [one\-one\-one assistance](https://console.aws.amazon.com/support/home#/case/create?issueType=technical)\. 

## Remediating Compromised AWS Credentials<a name="compromised-creds"></a>

Follow these recommended steps to remediate compromised credentials in your AWS environment:
+ **Identify the owner of the credentials\.**

  If a GuardDuty finding informs you of a potential compromise to AWS credentials, you can locate the affected IAM user by their access keys or user name\.
**Note**  
Users need their own access keys to make programmatic calls to AWS from the AWS Command Line Interface \(AWS CLI\), Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the APIs for individual AWS services\. To fill this need, you can create, modify, view, or rotate access keys \(access key IDs and secret access keys\) for IAM users\. For more information, see [Managing Access Keys for IAM Users](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)\.

  To find the access key ID or user name that belongs to a potentially compromised IAM user, open the console and view the details pane of the finding that you're analyzing\. For more information, see [Locating and Analyzing GuardDuty Findings](guardduty_findings.md#guardduty_working-with-findings)\. After you have the access key ID or user name, open the IAM console, choose the **Users** tab, and locate the affected user by typing the access key ID or user name in the **Find users by username or access key** search field\. 
+ **Determine whether the credentials were used by the IAM user legitimately\.**

  Contact the IAM user that you've located, and verify whether the user legitimately used the access key and user name that is identified in the GuardDuty finding\. For example, find out if the user did the following:
  + Invoked the API operation that was listed in the GuardDuty finding
  + Invoked the API operation at the time that is listed in the GuardDuty finding
  + Invoked the API operation from the IP address that is listed in the GuardDuty finding

If you confirm that the activity is a legitimate use of the AWS credentials, you can ignore the GuardDuty finding\. If not, this activity is likely the result of a compromise to that particular access key, the IAM user's user ID and password, or possibly the entire AWS account\. You can then use the information in the [My AWS account may be compromised](https://aws.amazon.com/premiumsupport/knowledge-center/potential-account-compromise/) article to remediate the issue\.