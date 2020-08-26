# Setting up GuardDuty<a name="guardduty_settingup"></a>

You must have an AWS account in order to enable Amazon GuardDuty\. If you don't have an account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

**Topics**
+ [Enable Amazon GuardDuty](#guardduty_enable-gd)

## Enable Amazon GuardDuty<a name="guardduty_enable-gd"></a>

To use GuardDuty, you must first enable it\. When GuardDuty is enabled a GuardDuty detector is created in that region\. GuardDuty can be enabled in a region through the console or using the [createDetector]() API\.

**Note the following about enabling GuardDuty**:
+ GuardDuty is assigned a service\-linked role called `AWSServiceRoleForAmazonGuardDuty`\. This service\-linked role allows GuardDuty to retrieve metadata for the EC2 instances and S3 buckets in your AWS environment that are involved in potentially suspicious activity\. It also allows GuardDuty to include the retrieved EC2 instance and S3 bucket metadata in the findings that GuardDuty generates about potentially suspicious activity\. To view the details of `AWSServiceRoleForAmazonGuardDuty`, on the **Welcome to GuardDuty** page, choose **View service role permissions**\. For more information, see [Using a service\-linked role to delegate permissions to GuardDuty](guardduty_managing_access.md#guardduty_service-access)\. For more information about service\-linked roles, see [Using service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\.
+ After you enable GuardDuty, it immediately begins pulling and analyzing independent streams of data from AWS CloudTrail management andAmazon S3 data events, VPC flow logs, and DNS logs to generate security findings\. Because GuardDuty only consumes this data for purposes of determining if there are any findings, GuardDuty doesn't manage AWS CloudTrail, VPC Flow Logs, and DNS logs for you or make their events and logs available to you\. If you have enabled these services independent of GuardDuty, you will continue to have the option to configure the settings of these data sources through their respective consoles or APIs\. For more information about the data sources that GuardDuty integrates with, see [What is AWS CloudTrail?](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) and [Working with flow logs](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html#working-with-flow-logs)\.

  We highly recommend that you enable GuardDuty in all supported AWS Regions\. This enables GuardDuty to generate findings about unauthorized or unusual activity even in Regions that you are not actively using\. This also enables GuardDuty to monitor AWS CloudTrail events for global AWS services such as IAM\. If GuardDuty is not enabled in all supported Regions, its ability to detect activity that involves global services is reduced\. For a full list of regions in which GuardDuty is supported see [Regions and endpoints](guardduty_regions.md)\.
+ You can disable GuardDuty at any time to it from processing findings from AWS CloudTrail management events, VPC Flow Logs, and DNS logs\. For more information, see [Suspending or disabling GuardDuty](guardduty_suspend-disable.md)\. 
+ You can optionally disable the processing of CloudTrail S3 data events at any time, without interrupting GuardDuty's ability to process findings from AWS CloudTrail management events, VPC Flow Logs, and DNS logs\. For more information, see [Configuring S3 protection for an individual account](s3_detection.md#data-source-configure)\. 

### Enabling GuardDuty with an IAM user \(console\)<a name="guardduty-thru-policy_proc"></a>

Any user with administrator access can enable GuardDuty, however, following the security best practice of least privilege, it is recommended that you create an IAM user, role, or group to manage GuardDuty specifically\. 

The minimum permissions required for an IAM identity to enable and manage GuardDuty are outlined in the following procedure\. 

In this example we attach the policy to an IAM user and use that user to enable GuardDuty, however, it is also possible to connect this policy to an IAM group or role depending on the access needs of your environment\. For more information about the different IAM identities and how they can be used see [IAM: Identities \(users, groups, and roles\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html)\. 

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Select **Create policy** and then the **JSON** tab\. Replace the default JSON text with the following policy\.
**Note**  
Replace the sample account ID in the example below with your actual AWS account ID\.

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "guardduty:*"
               ],
               "Resource": "*"
           },
           {
               "Effect": "Allow",
               "Action": [
                   "iam:CreateServiceLinkedRole"
               ],
               "Resource": "arn:aws:iam::123456789123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty",
               "Condition": {
                   "StringLike": {
                       "iam:AWSServiceName": "guardduty.amazonaws.com"
                   }
               }
           }
   
       ]
   }
   ```

   Once you've added the policy JSON select **Review policy** and give your policy a name that is easy to identify, then select **Create policy**\.

1. After selecting an existing or newly created IAM user select **Add permissions** and then **Attach existing policies directly**\. Use the search bar to find the policy you created in step 2 and add it to the user\.

1. Use the credentials of the IAM user from step 3 to sign in to the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\. 

1. When you open the GuardDuty console for the first time, choose **Get Started**, and then choose **Enable GuardDuty**\.

### Amazon GuardDuty free trial<a name="guardduty_free-trial"></a>

When you enable GuardDuty for the first time, or enable a new data source for GuardDuty, your AWS account is automatically enrolled in a 30\-day GuardDuty free trial\. You can view the details of your GuardDuty free trial in the **Usage** page of the GuardDuty console \(choose **Usage** in the navigation pane\)\. The details include the time remaining on your free trial and the estimated monthly cost for using GuardDuty after your free trial ends\. This estimate is based on the logs that GuardDuty processes and analyzes daily during the free trial\. 

This estimated monthly cost does NOT project charges for using GuardDuty in all of the AWS accounts and Regions where you enabled GuardDuty\. The monthly cost estimate is based only on the GuardDuty usage in the AWS account and the AWS Region to which you’re currently signed in\. If you are operating as a GuardDuty master account in a multi\-account environment, then you will be able to see the usage and estimated costs for all of your member accounts\. You can also use the API to get cost estimates\. For more information see [Estimating GuardDuty costs in GuardDuty](monitoring_costs.md)\.

You will not be charged for using GuardDuty until your free trial ends\. For more information about GuardDuty pricing, see [Amazon GuardDuty Pricing](http://aws.amazon.com/guardduty/pricing/)\.