# Setting Up GuardDuty<a name="guardduty_settingup"></a>

You must have an AWS account in order to enable Amazon GuardDuty\. If you don't have an account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

**Topics**
+ [Enable Amazon GuardDuty](#guardduty_enable-gd)
+ [Amazon GuardDuty Free Trial](#guardduty_free-trial)
+ [Using Service\-Linked Roles for Amazon GuardDuty](using-service-linked-roles.md)

## Enable Amazon GuardDuty<a name="guardduty_enable-gd"></a>

To use GuardDuty, you must first enable it\. Use the following procedure to enable GuardDuty\.

1. The IAM identity \(user, role, group\) that you use to enable GuardDuty must have the required permissions\. To grant the permissions required to enable GuardDuty, attach the following policy to an IAM user, group, or role:
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

1. Use the credentials of the IAM identity from step 1 to sign in to the GuardDuty console\. When you open the GuardDuty console for the first time, choose **Get Started**, and then choose **Enable GuardDuty**\.

   Note the following about enabling GuardDuty:
   + GuardDuty is assigned a service\-linked role called `AWSServiceRoleForAmazonGuardDuty`\. This service\-linked role allows GuardDuty to retrieve metadata for the EC2 instances in your AWS environment that are involved in potentially suspicious activity\. It also allows GuardDuty to include the retrieved EC2 instance metadata in the findings that GuardDuty generates about potentially suspicious activity\. To view the details of `AWSServiceRoleForAmazonGuardDuty`, on the **Welcome to GuardDuty** page, choose **View service role permissions**\. For more information, see [Using a Service\-Linked Role to Delegate Permissions to GuardDuty](guardduty_managing_access.md#guardduty_service-access)\. For more information about service\-linked roles, see [Using Service\-Linked Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\.
   + After you enable GuardDuty, it immediately begins pulling and analyzing independent streams of data from AWS CloudTrail, VPC Flow Logs, and DNS logs to generate security findings\. Because GuardDuty only consumes this data for purposes of determining if there are any findings, GuardDuty doesn't manage AWS CloudTrail, VPC Flow Logs, and DNS logs for you or make their events and logs available to you\. If you have enabled these services independent of GuardDuty, you will continue to have the option to configure the settings of these data sources through their respective consoles or APIs\. For more information about the data sources that GuardDuty integrates with, see [What is AWS CloudTrail?](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html) and [Working With Flow Logs](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html#working-with-flow-logs)\.
**Important**  
It is highly recommended that you enable GuardDuty in all supported AWS regions\. This allows GuardDuty to generate findings about unauthorized or unusual activity even in regions that you are not actively using\. This also allows GuardDuty to monitor AWS CloudTrail events for global AWS services such as IAM\.   
If GuardDuty is not enabled in all supported regions, its ability to detect activity that involves global services is reduced\. 
   + You can disable GuardDuty at any time to stop it from processing and analyzing AWS CloudTrail events, VPC Flow Logs, and DNS logs\. For more information, see [Suspending or Disabling GuardDuty](guardduty_suspend-disable.md)\.

## Amazon GuardDuty Free Trial<a name="guardduty_free-trial"></a>

When you enable GuardDuty for the first time, your AWS account is automatically enrolled in a 30\-day GuardDuty free trial\. You can view the details of your GuardDuty free trial in the **Free trial** page of the GuardDuty console \(choose **Free trial** / **Details** in the navigation pane\)\. The details include your current position on the free trial timeline and the estimated daily cost for using GuardDuty after your free trial ends\. This estimate is based on the logs that GuardDuty processes and analyzes daily during the free trial\. 

**Important**  
This estimated daily cost does NOT project charges for using GuardDuty in all of the AWS accounts and regions where you enabled GuardDuty\. The daily cost estimate is based only on the GuardDuty usage in the AWS account and the AWS region to which you’re currently signed in\. 

You will not be charged for using GuardDuty until your free trial ends\. For more information about GuardDuty pricing, see [Amazon GuardDuty Pricing](https://aws.amazon.com/guardduty/pricing/)\. 