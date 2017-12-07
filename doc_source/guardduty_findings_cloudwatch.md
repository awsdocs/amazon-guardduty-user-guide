# Monitoring Amazon GuardDuty Findings with Amazon CloudWatch Events<a name="guardduty_findings_cloudwatch"></a>

Amazon GuardDuty sends notifications based on [Amazon CloudWatch Events](http://docs.aws.amazon.com/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html) when any change in the findings takes place\. This includes newly generated findings and updates to existing findings\. GuardDuty aggregates all changes to findings that take place in five\-minute intervals into a single event\.

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

## Creating a CloudWatch Events Rule and Target for GuardDuty<a name="guardduty_cloudwatch_example"></a>

Currently in GuardDuty, there's no user interface support for CloudWatch\. The following procedure shows how to use AWS CLI commands to create a CloudWatch Events rule and target for GuardDuty\. Specifically, the procedure shows you how to create a rule that enables CloudWatch to send events for all findings that GuardDuty generates, and add an AWS Lambda function as a target for the rule\. 

**Note**  
In addition to Lambda functions, GuardDuty and CloudWatch support the following target types: Amazon EC2 instances, Amazon Kinesis streams, Amazon ECS tasks, AWS Step Functions state machines, the `run` command, and built\-in targets\.

**To create a rule and target**

1. To create a rule that enables CloudWatch to send events for all findings that GuardDuty generates, run the following CloudWatch CLI command: 

   `aws events put-rule --name Test --event-pattern '{"source":["aws.guardduty"]}'`

1. To attach a Lambda function as a target for the rule that you created in step 1, run the following CloudWatch CLI command:

   `aws events put-targets --rule Test --targets Id=1,Arn=arn:aws:lambda:us-east-1:111122223333:function:<your_function>`
**Note**  
Make sure to replace <your\_function> in the command above with your actual Lambda function for the GuardDuty events\.

1. To add the permissions required to invoke the target, run the following Lambda CLI command:

   `aws lambda add-permission --function-name <your_function> --statement-id 1 --action 'lambda:InvokeFunction' --principal events.amazonaws.com`
**Note**  
Make sure to replace <your\_function> in the command above with your actual Lambda function for the GuardDuty events\.