# Monitoring Amazon GuardDuty Findings with Amazon CloudWatch Events<a name="guardduty_findings_cloudwatch"></a>

Amazon GuardDuty sends notifications based on [Amazon CloudWatch Events](http://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) when any change in the findings takes place\. An event indicates a change in your AWS environment\. In the context of GuardDuty, such changes include newly generated findings and all subsequent occurrences of these existing findings\. All subsequent occurrences of an existing finding are always assigned a finding ID that is identical to the ID of the original finding\.

Every GuardDuty finding is assigned a finding ID\. GuardDuty creates a CloudWatch event for every finding with a unique finding ID\.

**Notifications for newly generated findings with a unique finding ID** \- GuardDuty sends a notification based on its CloudWatch event within 5 minutes of the finding\. This event \(and this notification\) also includes all subsequent occurrences of this finding that take place in the first 5 minutes since this finding with a unique ID is generated\.

**Notifications for subsequent finding occurrences** \- by default, for every finding with a unique finding ID, GuardDuty aggregates all subsequent occurrences of a particular finding that take place in six\-hour intervals into a single event\. GuardDuty then sends a notification about these subsequent occurrences based on this event\. In other words, by default, for the subsequent occurrences of the existing findings, GuardDuty sends notifications based on CloudWatch events every 6 hours\.

**Important**  
If you archive a finding manually, the initial and all subsequent occurrences of this finding \(generated after the archiving is complete\) are sent to CloudWatch events per frequency described above\.  
If a finding is auto\-archived, the initial and all subsequent occurrences of this finding \(generated after the archiving is complete\) are NOT sent to CloudWatch events\.

The CloudWatch [event](http://docs.aws.amazon.com/AmazonCloudWatch/latest/events/CloudWatchEventsandEventPatterns.html) for GuardDuty has the following format:

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

For the complete list of all the parameters included in the COMPLETE\_GUARDDUTY\_FINDING\_JSON, see [Response Syntax](get-findings.md#get-findings-response-syntax)\. The id parameter that appears in the COMPLETE\_GUARDDUTY\_FINDING\_JSON is the finding ID described above\.

## Creating a CloudWatch Events Rule and Target for GuardDuty<a name="guardduty_cloudwatch_example"></a>

The following procedure shows how to use AWS CLI commands to create a CloudWatch Events rule and target for GuardDuty\. Specifically, the procedure shows you how to create a rule that enables CloudWatch to send events for all findings that GuardDuty generates, and add an AWS Lambda function as a target for the rule\. 

**Note**  
In addition to Lambda functions, GuardDuty and CloudWatch support the following target types: Amazon EC2 instances, Amazon Kinesis streams, Amazon ECS tasks, AWS Step Functions state machines, the `run` command, and built\-in targets\.

You can also create a CloudWatch Events rule and target for GuardDuty through the CloudWatch Events console\. For more information and detailed steps, see [Creating a CloudWatch Events Rule That Triggers on an Event](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/Create-CloudWatch-Events-Rule.html)\. In the **Event Source** section, select **GuardDuty** for **Service name** and **GuardDuty Finding** for **Event Type**\. 

**To create a rule and target**

1. To create a rule that enables CloudWatch to send events for all findings that GuardDuty generates, run the following CloudWatch CLI command: 

   `aws events put-rule --name Test --event-pattern "{\"source\":[\"aws.guardduty\"]}"`
**Important**  
You can further customize your rule so that it instructs CloudWatch to send events only for a subset of the GuardDuty\-generated findings\. This subset is based on the finding attribute\(s\) that are specified in the rule\. For example, use the following CLI command to create a rule that enables CloudWatch to only send events for the GuardDuty findings with the severity of either 5 or 8:   
`aws events put-rule --name Test --event-pattern "{\"source\":[\"aws.guardduty\"],\"detail-type\":[\"GuardDuty Finding\"],\"detail\":{\"severity\":[5,8]}}"`  
For this purpose, you can use any of the GuardDuty attributes that are supported for sorting findings\. For more information, see [GetFindings](get-findings.md)\.

1. To attach a Lambda function as a target for the rule that you created in step 1, run the following CloudWatch CLI command:

   `aws events put-targets --rule Test --targets Id=1,Arn=arn:aws:lambda:us-east-1:111122223333:function:<your_function>`
**Note**  
Make sure to replace <your\_function> in the command above with your actual Lambda function for the GuardDuty events\.

1. To add the permissions required to invoke the target, run the following Lambda CLI command:

   `aws lambda add-permission --function-name <your_function> --statement-id 1 --action 'lambda:InvokeFunction' --principal events.amazonaws.com`
**Note**  
Make sure to replace <your\_function> in the command above with your actual Lambda function for the GuardDuty events\.
**Note**  
In the procedure above, we're using a Lambda function as the target for the rule that triggers CloudWatch events\. You can also configure other AWS resources as targets to trigger CloudWatch Events\. For more information, see [PutTargets](https://docs.aws.amazon.com/AmazonCloudWatchEvents/latest/APIReference/API_PutTargets.html)\.