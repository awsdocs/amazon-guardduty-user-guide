# Subscribing to GuardDuty announcements SNS topic<a name="guardduty_sns"></a>

This section provides information on subscribing to the GuardDuty Announcements SNS topic to receive notifications about newly released finding types, updates to the existing finding types, and other functionality changes\. Notifications are available in all formats that Amazon SNS supports\. 

**Note**  
Your user account must have sns::subscribe IAM permissions to subscribe to an SNS topic\.

You can subscribe an Amazon SQS queue to this notification topic, but you must use a topic ARN that is in the same Region\. For more information, see [Tutorial: Subscribing an Amazon SQS queue to an Amazon SNS topic](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-subscribe-queue-sns-topic.html) in the Amazon Simple Queue Service Developer Guide\.

You can also use an AWS Lambda function to trigger events when notifications are received\. For more information, see [Invoking Lambda functions using Amazon SNS notifications](https://docs.aws.amazon.com/sns/latest/dg/sns-lambda-as-subscriber.html) in the Amazon Simple Notification Service Developer Guide\.

The Amazon SNS topic ARNs for each Region are shown below\.


| AWS Region | Amazon SNS topic ARN | 
| --- | --- | 
| us\-east\-1 | arn:aws:sns:us\-east\-1:242987662583:GuardDutyAnnouncements | 
| us\-east\-2 | arn:aws:sns:us\-east\-2:118283430703:GuardDutyAnnouncements | 
| us\-west\-1 | arn:aws:sns:us\-west\-1:144182107116:GuardDutyAnnouncements | 
| us\-west\-2 | arn:aws:sns:us\-west\-2:934957504740:GuardDutyAnnouncements | 
| ca\-central\-1 | arn:aws:sns:ca\-central\-1:107430051933:GuardDutyAnnouncements | 
| eu\-north\-1 | arn:aws:sns:eu\-north\-1:973841112453:GuardDutyAnnouncements | 
| eu\-west\-1 | arn:aws:sns:eu\-west\-1:965013871422:GuardDutyAnnouncements | 
| eu\-west\-2 | arn:aws:sns:eu\-west\-2:506403581195:GuardDutyAnnouncements | 
| eu\-west\-3 | arn:aws:sns:eu\-west\-3:436163563069:GuardDutyAnnouncements | 
| eu\-central\-1 | arn:aws:sns:eu\-central\-1:378365507264:GuardDutyAnnouncements | 
| ap\-east\-1 | arn:aws:sns:ap\-east\-1:646602203151:GuardDutyAnnouncements | 
| ap\-northeast\-1 | arn:aws:sns:ap\-northeast\-1:741172661024:GuardDutyAnnouncements | 
| ap\-northeast\-2 | arn:aws:sns:ap\-northeast\-2:464168911255:GuardDutyAnnouncements | 
| ap\-southeast\-1 | arn:aws:sns:ap\-southeast\-1:476419727788:GuardDutyAnnouncements | 
| ap\-southeast\-2 | arn:aws:sns:ap\-southeast\-2:457615622431:GuardDutyAnnouncements | 
| ap\-south\-1 | arn:aws:sns:ap\-south\-1:926826061926:GuardDutyAnnouncements | 
| sa\-east\-1 | arn:aws:sns:sa\-east\-1:955633302743:GuardDutyAnnouncements | 
| us\-gov\-west\-1 | arn:aws\-us\-gov:sns:us\-gov\-west\-1:430639793359:GuardDutyAnnouncements | 

**To subscribe to the GuardDuty update notification email in the AWS Management Console**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. In the Region list, choose the same Region as the topic ARN to which to subscribe\. This example uses the `us-west-2` Region\.

1. In the left navigation pane, choose **Subscriptions**, **Create subscription**\.

1. In the **Create Subscription** dialog box, for **Topic ARN**, paste the topic ARN: `arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements`\. 

1. For **Protocol**, choose **Email**\. For **Endpoint**, type an email address that you can use to receive the notification\.

1. Choose **Create subscription**\.

1. In your email application, open the message from AWS Notifications and open the link to confirm your subscription\.

   Your web browser displays a confirmation response from Amazon SNS\.

**To subscribe to the GuardDuty update notification email with the AWS CLI**

1. Run the following command with the AWS CLI:

   ```
   aws sns --region us-west-2 subscribe --topic-arn arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements --protocol email --notification-endpoint your_email@your_domain.com
   ```

1. In your email application, open the message from AWS Notifications and open the link to confirm your subscription\.

   Your web browser displays a confirmation response from Amazon SNS\.

## Amazon SNS message format<a name="guardduty_sns-notification-format"></a>

An example GuardDuty update notification message about new findings is shown below:

```
{
    "Type" : "Notification",
    "MessageId" : "9101dc6b-726f-4df0-8646-ec2f94e674bc",
    "TopicArn" : "arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements",
    "Message" : "{\"version\":\"1\",\"type\":\"NEW_FINDINGS\",\"findingDetails\":[{\"link\":\"https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_unauthorized.html\",\"findingType\":\"UnauthorizedAccess:EC2/TorClient\",\"findingDescription\":\"This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor Guard or an Authority node. Tor is software for enabling anonymous communication. Tor Guards and Authority nodes act as initial gateways into a Tor network. This traffic can indicate that this EC2 instance is acting as a client on a Tor network. A common use for a Tor client is to circumvent network monitoring and filter for access to unauthorized or illicit content. Tor clients can also generate nefarious Internet traffic, including attacking SSH servers. This activity can indicate that your EC2 instance is compromised.\"}]}",
    "Timestamp" : "2018-03-09T00:25:43.483Z",
    "SignatureVersion" : "1",
    "Signature" : "XWox8GDGLRiCgDOXlo/fG9Lu/88P8S0FL6M6oQYOmUFzkucuhoblsdea3BjqdCHcWR7qdhMPQnLpN7y9iBrWVUqdAGJrukAI8athvAS+4AQD/V/QjrhsEnlj+GaiW+ozAu006X6GopOzFGnCtPMROjCMrMonjz7Hpv/8KRuMZR3pyQYm5d4wWB7xBPYhUMuLoZ1V8YFs55FMtgQV/YLhSYuEu0BP1GMtLQauxDkscOtPP/vjhGQLFx1Q9LTadcQiRHtNIBxWL87PSI+BVvkin6AL7PhksvdQ7FAgHfXsit+6p8GyOvKCqaeBG7HZhR1AbpyVka7JSNRO/6ssyrlj1g==",
    "SigningCertURL" : "https://sns.us-west-2.amazonaws.com/SimpleNotificationService-433026a4050d206028891664da859041.pem",
    "UnsubscribeURL" : "https://sns.us-west-2.amazonaws.com/?Action=Unsubscribe&SubscriptionArn=arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements:9225ed2b-7228-4665-8a01-c8a5db6859f4"
}
```

The parsed Message value \(with escaped quotes removed\) is shown below:

```
{
    "version": "1",
    "type": "NEW_FINDINGS",
    "findingDetails": [{
        "link": "https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_unauthorized.html",
        "findingType": "UnauthorizedAccess:EC2/TorClient",
        "findingDescription": "This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor Guard or an Authority node. Tor is software for enabling anonymous communication. Tor Guards and Authority nodes act as initial gateways into a Tor network. This traffic can indicate that this EC2 instance is acting as a client on a Tor network. A common use for a Tor client is to circumvent network monitoring and filter for access to unauthorized or illicit content. Tor clients can also generate nefarious Internet traffic, including attacking SSH servers. This activity can indicate that your EC2 instance is compromised."
    }]
}
```

An example GuardDuty update notification message about GuardDuty functionality updates is shown below:

```
{
    "Type" : "Notification",
    "MessageId" : "9101dc6b-726f-4df0-8646-ec2f94e674bc",
    "TopicArn" : "arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements",
    "Message" : "{\"version\":\"1\",\"type\":\"NEW_FEATURES\",\"featureDetails\":[{\"featureDescription\":\"Customers with high-volumes of global CloudTrail events should see a net positive impact on their GuardDuty costs.\",\"featureLink\":\"https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html#guardduty_cloudtrail\"}]}",
    "Timestamp" : "2018-03-09T00:25:43.483Z",
    "SignatureVersion" : "1",
    "Signature" : "XWox8GDGLRiCgDOXlo/fG9Lu/88P8S0FL6M6oQYOmUFzkucuhoblsdea3BjqdCHcWR7qdhMPQnLpN7y9iBrWVUqdAGJrukAI8athvAS+4AQD/V/QjrhsEnlj+GaiW+ozAu006X6GopOzFGnCtPMROjCMrMonjz7Hpv/8KRuMZR3pyQYm5d4wWB7xBPYhUMuLoZ1V8YFs55FMtgQV/YLhSYuEu0BP1GMtLQauxDkscOtPP/vjhGQLFx1Q9LTadcQiRHtNIBxWL87PSI+BVvkin6AL7PhksvdQ7FAgHfXsit+6p8GyOvKCqaeBG7HZhR1AbpyVka7JSNRO/6ssyrlj1g==",
    "SigningCertURL" : "https://sns.us-west-2.amazonaws.com/SimpleNotificationService-433026a4050d206028891664da859041.pem",
    "UnsubscribeURL" : "https://sns.us-west-2.amazonaws.com/?Action=Unsubscribe&SubscriptionArn=arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements:9225ed2b-7228-4665-8a01-c8a5db6859f4"
}
```

The parsed Message value \(with escaped quotes removed\) is shown below:

```
{
    "version": "1",
    "type": "NEW_FEATURES",
    "featureDetails": [{
        "featureDescription": "Customers with high-volumes of global CloudTrail events should see a net positive impact on their GuardDuty costs.",
        "featureLink": "https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_data-sources.html#guardduty_cloudtrail"
    }]
}
```

An example GuardDuty update notification message about updated findings is shown below:

```
{
    "Type": "Notification",
    "MessageId": "9101dc6b-726f-4df0-8646-ec2f94e674bc",
    "TopicArn": "arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements",
    "Message": "{\"version\":\"1\",\"type\":\"UPDATED_FINDINGS\",\"findingDetails\":[{\"link\":\"https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_unauthorized.html\",\"findingType\":\"UnauthorizedAccess:EC2/TorClient\",\"description\":\"Increased severity value from 5 to 8.\"}]}",
    "Timestamp": "2018-03-09T00:25:43.483Z",
    "SignatureVersion": "1",
    "Signature": "XWox8GDGLRiCgDOXlo/fG9Lu/88P8S0FL6M6oQYOmUFzkucuhoblsdea3BjqdCHcWR7qdhMPQnLpN7y9iBrWVUqdAGJrukAI8athvAS+4AQD/V/QjrhsEnlj+GaiW+ozAu006X6GopOzFGnCtPMROjCMrMonjz7Hpv/8KRuMZR3pyQYm5d4wWB7xBPYhUMuLoZ1V8YFs55FMtgQV/YLhSYuEu0BP1GMtLQauxDkscOtPP/vjhGQLFx1Q9LTadcQiRHtNIBxWL87PSI+BVvkin6AL7PhksvdQ7FAgHfXsit+6p8GyOvKCqaeBG7HZhR1AbpyVka7JSNRO/6ssyrlj1g==",
    "SigningCertURL": "https://sns.us-west-2.amazonaws.com/SimpleNotificationService-433026a4050d206028891664da859041.pem",
    "UnsubscribeURL": "https://sns.us-west-2.amazonaws.com/?Action=Unsubscribe&SubscriptionArn=arn:aws:sns:us-west-2:934957504740:GuardDutyAnnouncements:9225ed2b-7228-4665-8a01-c8a5db6859f4"
}
```

The parsed Message value \(with escaped quotes removed\) is shown below:

```
{
    "version": "1",
    "type": "UPDATED_FINDINGS",
    "findingDetails": [{
        "link": "https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_unauthorized.html",
        "findingType": "UnauthorizedAccess:EC2/TorClient",
        "description": "Increased severity value from 5 to 8."
    }]
}
```