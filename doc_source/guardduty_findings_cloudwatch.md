# Creating custom responses to GuardDuty findings with Amazon CloudWatch Events<a name="guardduty_findings_cloudwatch"></a>

GuardDuty can send notifications based on [Amazon CloudWatch Events](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) when any change in findings takes place\. Finding changes that will create a CloudWatch event include newly generated findings or newly aggregated findings\.

Every GuardDuty finding is assigned a finding ID\. GuardDuty creates a CloudWatch event for every finding with a unique finding ID\. All subsequent occurrences of an existing finding are aggregated to the original finding\. 

By using CloudWatch events with GuardDuty you can automate tasks to help you respond to security issues revealed by GuardDuty findings\.

In order to receive notifications about GuardDuty findings based on CloudWatch Events, you must create a CloudWatch Events rule and a target for GuardDuty\. This rule enables CloudWatch to send notifications for findings that GuardDuty generates to the target that is specified in the rule\. For more information, see [Creating a CloudWatch Events rule and target for GuardDuty \(CLI\)](#guardduty_cloudwatch_example)\.

**Topics**
+ [CloudWatch Events notification frequency for GuardDuty](#guardduty_findings_cloudwatch_notification_frequency)
+ [Monitoring archived GuardDuty findings with CloudWatch Events](#guardduty_findings_cloudwatch_archived)
+ [CloudWatch event format for GuardDuty](#guardduty_findings_cloudwatch_format)
+ [Creating a CloudWatch Events rule to notify you of GuardDuty findings \(console\)](#guardduty_cloudwatch_severity_notification)
+ [Creating a CloudWatch Events rule and target for GuardDuty \(CLI\)](#guardduty_cloudwatch_example)

## CloudWatch Events notification frequency for GuardDuty<a name="guardduty_findings_cloudwatch_notification_frequency"></a>

**Notifications for newly generated findings with a unique finding ID** – GuardDuty sends a notification based on its CloudWatch event within 5 minutes of the finding\. This event \(and this notification\) also includes all subsequent occurrences of this finding that take place in the first 5 minutes since this finding with a unique ID is generated\.

**Important**  
You CANNOT customize the default frequency \(5 minutes\) of notifications sent about the newly generated findings\.

**Notifications for subsequent finding occurrences** – By default, for every finding with a unique finding ID, GuardDuty aggregates all subsequent occurrences of a particular finding that take place in 6\-hour intervals into a single event\. GuardDuty then sends a notification about these subsequent occurrences based on this event\. In other words, by default, for the subsequent occurrences of the existing findings, GuardDuty sends notifications based on CloudWatch events every 6 hours\.

**Important**  
You can customize the default frequency of notifications sent about the subsequent finding occurrences\. Possible values are 15 minutes, 1 hour, or the default 6 hours\. You can update this value using the [CreateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) or the [UpdateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateDetector.html) API operations\. You can also update this value through the GuardDuty console \- choose **Settings** and then under **CloudWatch Events**, choose one of the available values from the **Updated findings** pull\-down menu\.  
Only users from a master account can customize the default frequency of notifications sent about the subsequent finding occurrences to CloudWatch Events\. Users from member accounts CANNOT customize this frequency value\. The frequency value set by the master account in its own account is imposed on GuardDuty functionality in all its member accounts\. In other words, if a user from a master account sets this frequency value to 1 hour, all member accounts will also have the 1 hour frequency of notifications about the subsequent finding occurrences sent to CloudWatch Events\. For more information, see [Managing multiple accounts in Amazon GuardDuty](guardduty_accounts.md)\. 

## Monitoring archived GuardDuty findings with CloudWatch Events<a name="guardduty_findings_cloudwatch_archived"></a>

For the manually archived findings, the initial and all subsequent occurrences of these finding \(generated after the archiving is complete\) are sent to CloudWatch Events per frequency described above\.

For the auto\-archived findings, the initial and all subsequent occurrences of these findings \(generated after the archiving is complete\) are *not* sent to CloudWatch Events\.

## CloudWatch event format for GuardDuty<a name="guardduty_findings_cloudwatch_format"></a>

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
         "detail": {GUARDDUTY_FINDING_JSON_OBJECT}
        }
```

**Note**  
The detail value returns the JSON details of a single finding as an object, as opposed to returning the "findings" value which can support multiple findings within an array\.

For the complete list of all the parameters included in `GUARDDUTY_FINDING_JSON_OBJECT`, see [GetFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFindings.html#API_GetFindings_ResponseSyntax)\. The `id` parameter that appears in `GUARDDUTY_FINDING_JSON_OBJECT` is the finding ID previously described\.

## Creating a CloudWatch Events rule to notify you of GuardDuty findings \(console\)<a name="guardduty_cloudwatch_severity_notification"></a>

 The following procedure can be used to set up automatic email notifications for Medium to High Severity findings to the email address of your choice\. 

### Setup an Amazon SNS topic and endpoint<a name="SNS_setup"></a>

To begin, you must first set up a topic in Amazon Simple Notification Service and add an email address as an endpoint\. For more information refer to the [SNS guide](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)\.

1. Sign in to the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Select **Topics** from the navigation pane and then **Create Topic**\.

1. In the Create topic section, enter a Topic name, for example **GuardDuty**\. Other details are optional\.

1. Choose **Create Topic**\. The Topic details for your new topic will open\.

1. In the Subscriptions section select **Create Subscription**

1. 

   1. From the **Protocol** menu, select **Email**\.

   1. In the **Endpoint** field add the email address you would like to receive notifications at\.
**Note**  
You will be required to confirm your subscription through your email client after creating it\.

   1. Choose **Create Subscription**

1. Check for a subscription message in your inbox and choose **Confirm Subscription**

### Setup a CloudWatch event for GuardDuty findings<a name="setup_cloudwatch_event"></a>

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Select **Rules** from the navigation pane and then **Create Rule**\.

1. From the **Service Name** menu, choose **GuardDuty**\.

1. From the **Event Type** menu, choose **GuardDuty Finding**\.

1. In **Event Pattern Preview** choose **Edit**\.

1. Paste the below JSON code into **Event Pattern Preview** and choose **Save**

   ```
   {
     "source": [
       "aws.guardduty"
     ],
     "detail-type": [
       "GuardDuty Finding"
     ],
     "detail": {
       "severity": [
         4,
         4.0,
         4.1,
         4.2,
         4.3,
         4.4,
         4.5,
         4.6,
         4.7,
         4.8,
         4.9,
         5,
         5.0,
         5.1,
         5.2,
         5.3,
         5.4,
         5.5,
         5.6,
         5.7,
         5.8,
         5.9,
         6,
         6.0,
         6.1,
         6.2,
         6.3,
         6.4,
         6.5,
         6.6,
         6.7,
         6.8,
         6.9,
         7,
         7.0,
         7.1,
         7.2,
         7.3,
         7.4,
         7.5,
         7.6,
         7.7,
         7.8,
         7.9,
         8,
         8.0,
         8.1,
         8.2,
         8.3,
         8.4,
         8.5,
         8.6,
         8.7,
         8.8,
         8.9
       ]
     }
   }
   ```
**Note**  
The above code will alert for any Medium to High finding\.

1. In the **Targets** section click **Add Target**\.

1. From the **Select Targets** menu, choose **SNS Topic**\.

1. For **Select Topic** select the name of the SNS Topic you created in Step 1\.

1. Expand **Configure input** and then choose **Input Transformer**\.

1. Copy the following code and paste it into the **Input Path** field\.

   ```
   {
       "severity": "$.detail.severity",
       "Finding_ID": "$.detail.id",
       "Finding_Type": "$.detail.type",
       "region": "$.region",
       "Finding_description": "$.detail.description"
   }
   ```

1. Copy the following code and paste it into the **Input Template** field to format the email\.

   ```
   "You have a severity <severity> GuardDuty finding type <Finding_Type> in the <region> region."
   "Finding Description:"
   "<Finding_description>. "
   "For more details open the GuardDuty console at https://console.aws.amazon.com/guardduty/home?region=<region>#/findings?search=id%3D<Finding_ID>"
   ```

1. Click **Configure Details**\.

1. In the **Configure rule details** page, enter a **Name** and **Description** for the rule, and then choose **Create Rule**\.

## Creating a CloudWatch Events rule and target for GuardDuty \(CLI\)<a name="guardduty_cloudwatch_example"></a>

The following procedure shows how to use AWS CLI commands to create a CloudWatch Events rule and target for GuardDuty\. Specifically, the procedure shows you how to create a rule that enables CloudWatch to send events for all findings that GuardDuty generates and add an AWS Lambda function as a target for the rule\. 

**Note**  
In addition to Lambda functions, GuardDuty and CloudWatch support the following target types: Amazon EC2 instances, Amazon Kinesis streams, Amazon ECS tasks, AWS Step Functions state machines, the `run` command, and built\-in targets\.

You can also create a CloudWatch Events rule and target for GuardDuty through the CloudWatch Events console\. For more information and detailed steps, see [Creating a CloudWatch Events rule that triggers on an event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/Create-CloudWatch-Events-Rule.html)\. In the **Event Source** section, select **GuardDuty** for **Service name** and **GuardDuty Finding** for **Event Type**\. 

**To create a rule and target**

1. To create a rule that enables CloudWatch to send events for all findings that GuardDuty generates, run the following CloudWatch CLI command\.

   `aws events put-rule --name Test --event-pattern "{\"source\":[\"aws.guardduty\"]}"`
**Important**  
You can further customize your rule so that it instructs CloudWatch to send events only for a subset of the GuardDuty\-generated findings\. This subset is based on the finding attribute or attributes that are specified in the rule\. For example, use the following CLI command to create a rule that enables CloudWatch to only send events for the GuardDuty findings with the severity of either 5 or 8:   
`aws events put-rule --name Test --event-pattern "{\"source\":[\"aws.guardduty\"],\"detail-type\":[\"GuardDuty Finding\"],\"detail\":{\"severity\":[5,8]}}"`  
For this purpose, you can use any of the property values that are available in the JSON for GuardDuty findings\. 

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