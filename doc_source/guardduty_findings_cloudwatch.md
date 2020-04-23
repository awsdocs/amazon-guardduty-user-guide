# Monitoring GuardDuty Findings with Amazon CloudWatch Events<a name="guardduty_findings_cloudwatch"></a>

GuardDuty can send notifications based on [Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) when any changes in the findings takes place\. These changes include newly generated findings or subsequent occurrences of existing findings\.

Every GuardDuty finding is assigned a finding ID\. GuardDuty creates a CloudWatch event for every finding with a unique finding ID\. All subsequent occurrences of an existing finding are always assigned a finding ID that is identical to the ID of the original finding\.

In order to receive notifications about GuardDuty findings based on CloudWatch Events, you must create a CloudWatch Events rule and a target for GuardDuty\. This rule enables CloudWatch to send events for all findings that GuardDuty generates to the target that is specified in the rule\. For more information, see [Creating a CloudWatch Events Rule and Target for GuardDuty](#guardduty_cloudwatch_example)\.

**Topics**
+ [CloudWatch Events Notification Frequency for GuardDuty](#guardduty_findings_cloudwatch_notification_frequency)
+ [Monitoring Archived GuardDuty Findings with CloudWatch Events](#guardduty_findings_cloudwatch_archived)
+ [CloudWatch Event Format for GuardDuty](#guardduty_findings_cloudwatch_format)
+ [Creating a CloudWatch Events Rule and Target for GuardDuty](#guardduty_cloudwatch_example)

## CloudWatch Events Notification Frequency for GuardDuty<a name="guardduty_findings_cloudwatch_notification_frequency"></a>

**Notifications for newly generated findings with a unique finding ID** – GuardDuty sends a notification based on its CloudWatch event within 5 minutes of the finding\. This event \(and this notification\) also includes all subsequent occurrences of this finding that take place in the first 5 minutes since this finding with a unique ID is generated\.

**Important**  
You CANNOT customize the default frequency \(5 minutes\) of notifications sent about the newly generated findings\.

**Notifications for subsequent finding occurrences** – By default, for every finding with a unique finding ID, GuardDuty aggregates all subsequent occurrences of a particular finding that take place in 6\-hour intervals into a single event\. GuardDuty then sends a notification about these subsequent occurrences based on this event\. In other words, by default, for the subsequent occurrences of the existing findings, GuardDuty sends notifications based on CloudWatch events every 6 hours\.

**Important**  
You can customize the default frequency of notifications sent about the subsequent finding occurrences\. Possible values are 15 minutes, 1 hour, or the default 6 hours\. You can update this value using the [CreateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) or the [UpdateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateDetector.html) API operations\. You can also update this value through the GuardDuty console \- choose **Settings** and then under **CloudWatch Events**, choose one of the available values from the **Updated findings** pull\-down menu\.  
Only users from a master account can customize the default frequency of notifications sent about the subsequent finding occurrences to CloudWatch Events\. Users from member accounts CANNOT customize this frequency value\. The frequency value set by the master account in its own account is imposed on GuardDuty functionality in all its member accounts\. In other words, if a user from a master account sets this frequency value to 1 hour, all member accounts will also have the 1 hour frequency of notifications about the subsequent finding occurrences sent to CloudWatch Events\. For more information, see [Managing Multiple Accounts in Amazon GuardDuty](guardduty_accounts.md)\. 

## Monitoring Archived GuardDuty Findings with CloudWatch Events<a name="guardduty_findings_cloudwatch_archived"></a>

For the manually archived findings, the initial and all subsequent occurrences of these finding \(generated after the archiving is complete\) are sent to CloudWatch Events per frequency described above\.

For the auto\-archived findings, the initial and all subsequent occurrences of these findings \(generated after the archiving is complete\) are *not* sent to CloudWatch Events\.

## CloudWatch Event Format for GuardDuty<a name="guardduty_findings_cloudwatch_format"></a>

The CloudWatch [event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/CloudWatchEventsandEventPatterns.html) for GuardDuty has the following format\.

```
        {
         "version": "0",
         "id": "cd2d702e-ab31-411b-9344-793ce56b1bc7",
         "detail-type": "GuardDuty Finding",
         "source": "aws.guardduty",
         "account": "111122223333",
         "time": "1970-01-01T00:00:00Z",
         "region": "us-east-1",
         "resources": [],
         "detail": {COMPLETE_GUARDDUTY_FINDING_JSON}
        }
```

For the complete list of all the parameters included in `COMPLETE_GUARDDUTY_FINDING_JSON`, see [GetFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFindings.html#API_GetFindings_ResponseSyntax)\. The `id` parameter that appears in `COMPLETE_GUARDDUTY_FINDING_JSON` is the finding ID previously described\.

## Creating a CloudWatch Events Rule and Target for GuardDuty<a name="guardduty_cloudwatch_example"></a>

The following procedure shows how to use AWS CLI commands to create a CloudWatch Events rule and target for GuardDuty\. Specifically, the procedure shows you how to create a rule that enables CloudWatch to send events for all findings that GuardDuty generates and add an AWS Lambda function as a target for the rule\. 

**Note**  
In addition to Lambda functions, GuardDuty and CloudWatch support the following target types: Amazon EC2 instances, Amazon Kinesis streams, Amazon ECS tasks, AWS Step Functions state machines, the `run` command, and built\-in targets\.

You can also create a CloudWatch Events rule and target for GuardDuty through the CloudWatch Events console\. For more information and detailed steps, see [Creating a CloudWatch Events Rule That Triggers on an Event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/Create-CloudWatch-Events-Rule.html)\. In the **Event Source** section, select **GuardDuty** for **Service name** and **GuardDuty Finding** for **Event Type**\. 

**To create a rule and target**

1. To create a rule that enables CloudWatch to send events for all findings that GuardDuty generates, run the following CloudWatch CLI command\.

   `aws events put-rule --name Test --event-pattern "{\"source\":[\"aws.guardduty\"]}"`
**Important**  
You can further customize your rule so that it instructs CloudWatch to send events only for a subset of the GuardDuty\-generated findings\. This subset is based on the finding attribute or attributes that are specified in the rule\. For example, use the following CLI command to create a rule that enables CloudWatch to only send events for the GuardDuty findings with the severity of either 5 or 8:   
`aws events put-rule --name Test --event-pattern "{\"source\":[\"aws.guardduty\"],\"detail-type\":[\"GuardDuty Finding\"],\"detail\":{\"severity\":[5,8]}}"`  
For this purpose, you can use any of the GuardDuty attributes that are supported for sorting findings\. For more information, see [GetFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFindings.html)\.

1. To attach a Lambda function as a target for the rule that you created in step 1, run the following CloudWatch CLI command\.

   `aws events put-targets --rule Test --targets Id=1,Arn=arn:aws:lambda:us-east-1:111122223333:function:<your_function>`
**Note**  
Make sure to replace <your\_function> in the command above with your actual Lambda function for the GuardDuty events\.

1. To add the permissions required to invoke the target, run the following Lambda CLI command\.

   `aws lambda add-permission --function-name <your_function> --statement-id 1 --action 'lambda:InvokeFunction' --principal events.amazonaws.com`
**Note**  
Make sure to replace <your\_function> in the command above with your actual Lambda function for the GuardDuty events\.
**Note**  
In the procedure above, we're using a Lambda function as the target for the rule that triggers CloudWatch Events\. You can also configure other AWS resources as targets to trigger CloudWatch Events\. For more information, see [PutTargets](https://docs.aws.amazon.com/AmazonCloudWatchEvents/latest/APIReference/API_PutTargets.html)\.