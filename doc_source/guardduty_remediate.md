# Remediating security issues discovered by GuardDuty<a name="guardduty_remediate"></a>

Amazon GuardDuty generates [findings](guardduty_findings.md) that indicate potential security issues\. In this release of GuardDuty, the potential security issues indicate either a compromised EC2 instance or a set of compromised credentials in your AWS environment\. The following sections describe the recommended remediation steps for these scenarios\. If there are alternative remediation scenarios they will be described in the entry for that specific finding type\. You can access the full information about a finding type by selecting it from the [Active findings types table](guardduty_finding-types-active.md)\.

**Topics**
+ [Remediating a compromised EC2 instance](#compromised-ec2)
+ [Remediating a Compromised S3 Bucket](#compromised-s3)
+ [Remediating compromised AWS credentials](#compromised-creds)

## Remediating a compromised EC2 instance<a name="compromised-ec2"></a>

Follow these recommended steps to remediate a compromised EC2 instance in your AWS environment:
+ Investigate the potentially compromised instance for malware and remove any discovered malware\. You can also refer to the [AWS Marketplace](https://aws.amazon.com/marketplace) for partner products that might help to identify and remove malware\.
+ If you are unable to identify and stop unauthorized activity on your EC2 instance, we recommend that you terminate the compromised EC2 instance and replace it with a new instance as needed\. The following are additional resources for securing your EC2 instances:
  + "Security and Network" section in [Best practices for amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-best-practices.html)\.
  + [Amazon EC2 security groups for Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html) and [Amazon EC2 security groups for Windows instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/using-network-security.html)\.
  + [Tips for securing your EC2 instances \(Linux\)](http://aws.amazon.com/articles/tips-for-securing-your-ec2-instance/)\.
  + [AWS security best practices](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
+ Browse for further assistance on the AWS developer forums: [https://forums\.aws\.amazon\.com/index\.jspa](https://forums.aws.amazon.com/index.jspa) 
+ If you are a Premium Support package subscriber, you can submit a [technical support](https://console.aws.amazon.com/support/home#/case/create?issueType=technical) request\. 

## Remediating a Compromised S3 Bucket<a name="compromised-s3"></a>

Follow these recommended steps to remediate a compromised S3 bucket in your AWS environment:

1. **Identify the affected S3 resource\.**

   A GuardDuty finding for S3 will list an S3 bucket, the bucket's Amazon Resource number \(ARN\) and a bucket owner in the finding details\.

1. **Identify the source of the suspicious activity and the API call used\.**

   The API call used will be listed as `API` in the finding details\. The source will be an IAM principal \(either an IAM user, role, or account\) and identifying details will be listed in the finding\. Depending on the source type, Remote IP or source domain info will be available and can help you evaluate whether the source was authorized\. If the finding involved credentials from an EC2 Instance the instance details will also be included\.

1. **Determine whether the call source was authorized to access the identified resource\. **

   For example consider the following:
   + If an IAM user was involved is it possible their credentials have been compromised? See the next section on Remediating Compromised AWS Credentials\.
   + If an API was invoked from a principal that has no prior history of invoking this type of API, does this source need access permissions for this operation? Can the bucket permissions be further restricted?
   +  If the access was seen from the **user name** `ANONYMOUS_PRINCIPAL` with **user type** of `AWSAccount` this indicates the bucket is public and was accessed\. Should this bucket be public? If not, review the security recommendations below for alternative solutions to sharing S3 resources\. 

If the access was authorized you can ignore the finding\. If you determine that your S3 data has been exposed or accessed by an unauthorized party review the following S3 security recommendations to tighten permissions and restrict access\. Appropriate remediation solutions will depend on the needs of your specific environment\. 

**These are some recommendations based on specific S3 access needs:**
+ For a centralized way to limit public access to your S3 data use S3 block public access\. Block public access settings can be enabled for access points, buckets, and AWS Accounts through four different settings to control granularity of access\. For more information see [S3 Block Public Access Settings](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html#access-control-block-public-access-options)\.
+ AWS Access policies can be used to control how IAM users can access your resources, or how your buckets can be accessed\. For more information see [Using Bucket Policies and User Policies](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-iam-policies.html)\.

  Additionally you can use Virtual Private Cloud \(VPC\) endpoints with S3 bucket policies to restrict access to specific VPC endpoints\. For more information see [Example Bucket Policies for VPC Endpoints for Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies-vpc-endpoint.html)
+ To temporarily allow access to your S3 objects to trusted entities outside your account you can create a Presigned URL through S3\. This access is created using your account credentials and depending on the credentials used can last 6 hours to 7 days\. For more information see [Generating presigned URLs with S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/ShareObjectPreSignedURL.html)\.
+ For use cases that require that sharing of S3 objects between different sources you can use S3 Access Points to create permission sets that restrict access to only those within your private network\. For more information see [Managing data access with Amazon S3 access points ](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-points.html)\.
+ To securely grant access to your S3 resources to other AWS Accounts you can use an access control list \(ACL\), for more information see [Managing S3 Access with ACLs](https://docs.aws.amazon.com/AmazonS3/latest/dev/S3_ACLs_UsingACLs.html)\.

For a full overview of S3 security options you see [S3 Security best practices](https://docs.aws.amazon.com/AmazonS3/latest/dev/security-best-practices.html)\.

## Remediating compromised AWS credentials<a name="compromised-creds"></a>

Follow these recommended steps to remediate compromised credentials in your AWS environment:

1. **Identify the affected IAM entity and the API call used\.** 

   The API call used will be listed as `API` in the finding details\. The IAM entity \(either an IAM user or role\) and it's identifying information will be listed in the **Resource** section of a finding's details\. The type of IAM entity involved can be determined by the **User Type** field, the name of the IAM entity will be in the **User name** field\. The type of IAM entity involved in the finding can also be determined by the **Access key ID** used\.  
For keys beginning with `AKIA`:  
This type of key is a long term customer\-managed credential associated with an IAM user or AWS account root user\. For information on managing access keys for IAM users see [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)\.  
For keys beginning with `ASIA`:  
This type of key is a short term temporary credential generated by AWS Security Token Service\. These keys exists for only a short time and cannot be viewed or managed in the AWS Management Console\. IAM roles will always use AWS STS credentials, but they can also be generated for IAM Users, for more information on AWS STS see [IAM: Temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html#sts-introduction)\.  
If a role was used the **User name** field will contain information about the name of the role used\. You can determine how the key was requested with AWS CloudTrail by examining the `sessionIssuer` element of the CloudTrail log entry, for more information see [IAM and AWS STS information in CloudTrail](https://docs.aws.amazon.com/IAM/latest/UserGuide/cloudtrail-integration.html#iam-info-in-cloudtrail)\.

1. **Review permissions for the IAM entity\.**

   Open the IAM console, depending on the type of entity used, choose the **Users** or **Roles** tab, and locate the affected entity by typing the identified name into the search field\. Use the **Permission** and **Access Advisor** tabs to review effective permissions for that entity\.

1. **Determine whether the IAM entity credentials were used legitimately\.**

   Contact the user of the credentials to determine if the activity was intentional\.

   For example, find out if the user did the following:
   + Invoked the API operation that was listed in the GuardDuty finding
   + Invoked the API operation at the time that is listed in the GuardDuty finding
   + Invoked the API operation from the IP address that is listed in the GuardDuty finding

If you confirm that the activity is a legitimate use of the AWS credentials, you can ignore the GuardDuty finding\. If not, this activity could be the result of a compromise to that particular access key, the IAM user's user ID and password, or possibly the entire AWS account\. If you suspect your credentials have been compromised, review the information in the [My AWS account may be compromised](https://aws.amazon.com/premiumsupport/knowledge-center/potential-account-compromise/) article to remediate the issue\.