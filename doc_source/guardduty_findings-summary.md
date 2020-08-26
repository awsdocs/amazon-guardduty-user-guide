# Finding details<a name="guardduty_findings-summary"></a>

When viewed through the console an Amazon GuardDuty finding has a finding summary section that includes a number of finding details\. These details will vary based on finding type\.

There are two primary details that will determine what kinds of information are available for any finding\. The first is the Resource Type, which can be `AccessKey`, or `Instance`\. The second detail that determines finding information is **Resource Role**, this will be `Target` for Access keys, meaning the resource was the target of suspicious activity, but for Instance type findings this can also be `Actor`, which means your resource was the actor carrying out suspicious activity\. The information on this page attempts to describes some of the commonly available details for findings\. 
+ A finding's summary section that includes the following information: 
  + **Finding type** – A formatted string representing the type of activity that triggered the finding\. For more information, see [GuardDuty finding format](guardduty_finding-format.md)\.
  + **Finding ID** – A unique Finding ID for this finding type and set of parameters\. New occurrences of activity matching this pattern will be aggregated to the same ID\.
  + **Severity** – a finding's assigned severity level of either High, Medium, or Low\. For more information, see [Severity levels for GuardDuty findings](guardduty_findings.md#guardduty_findings-severity)\.
  + **Region** – the AWS Region in which the finding was generated\. For more information about supported Regions, see [Regions and endpoints](guardduty_regions.md)
  + **Count** – The number of times GuardDuty has aggregated an activity matching this pattern to this finding ID\.
  + **Account ID** – the ID of the AWS account in which the activity took place that prompted GuardDuty to generate this finding\.
  + **Resource ID** – the ID of the AWS resource against which the activity took place that prompted GuardDuty to generate this finding\.
  + **Created at** – the time and date this finding was first created at\. If this value differs from **Updated at** it indicates the activity has occurred multiple times and is an ongoing issue\.
**Note**  
Findings' time stamps in the GuardDuty console appear in your local time zone, while JSON exports and CLI outputs display timestamps in UTC\.
  + **Updated at** – The last time this finding was updated with new activity matching the pattern that prompted GuardDuty to generate this finding\.
**Note**  
Findings' time stamps in the GuardDuty console appear in your local time zone, while JSON exports and CLI outputs display timestamps in UTC\.
+ The **Resource affected** gives details on the AWS resource that was targeted by the trigger activity\. The information available will vary based on resource type and action type\.
  + **Resource role** – The role of the AWS resource that triggered the finding\. This value can be **TARGET** or **ACTOR**, and represents whether your resource was the target of the suspicious activity or the actor that preformed the suspicious activity respectively\.
  + **Resource type** – the type of the affected resource\. This value is either **AccessKey**, **S3 bucket** or **Instance**\. Depending on the Resource type different finding details will be available\. 
    + Instance details:
      + **Instance ID** – the ID of the EC2 instance involved in the activity that prompted GuardDuty to generate the finding\. 
      + **Instance Type** – the type of the EC2 instance involved in the finding\. 
      + **Launch Time** – the time and date the assistance was launched\. 
      + **Outpost ARN** – The Amazon Resource Name \(ARN\) of the AWS Outpost\. Only applicable to AWS Outposts instances\. For more information, see [What is AWS Outposts?](https://docs.aws.amazon.com/outposts/latest/userguide/what-is-outposts.html)
      + **Security Group Name** – The name of the Security Group attached to the involved instance\.
      + **Security Group ID** – The ID of the Security Group attached to the involved instance\.
      + **Instance state** – The current state of the targeted instance\.
      + **Availability Zone** – The current state of the targeted instance\.
      + **Image ID** – The ID of the Amazon Machine Image used to build the instance involved in the activity\.
      + **Image Description** – A description of the ID of the Amazon Machine Image used to build the instance involved in the activity\.
      + **Tags** – A list of Tags attached to this resource, listed in the format of `key`:`value`\.
    + Access Key details:
      + **Access key ID** – access key ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 
      + **Principal ID** – the principal ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 
      + **User type** – the type of user engaged in the activity that prompted GuardDuty to generate the finding\. For more information, see [CloudTrail userIdentity element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html#cloudtrail-event-reference-user-identity-fields)\.
      + **User name** – The name of the user engaged in the activity that prompted GuardDuty to generate the finding\.
    + S3 bucket details
      + **Name** – The name of the bucket involved in the finding\.
      + **ARN** – The ARN of the bucket involved in the finding\.
      + **Owner** – The canonical user ID of the user that owns the bucket involved in the finding\. For more information on canonical user ID's see [AWS account identifiers](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html)\.
      + **Type** – The type of bucket finding, can be either **Destination** or **Source**\.
      + ** Default server side encryption** – encryption details for the bucket\.
      + **Bucket Tags** – A list of Tags attached to this resource, listed in the format of `key`:`value`\.
      + **Effective Permissions** – An evaluation of all effective permissions and policies on the bucket that indicates whether the involved bucket is publicly exposed, values can be PUBLIC or NOT PUBLIC\.
+ A finding's **Action** gives details on the type of activity that triggered the finding\. The information available will vary based on action type\.
  + **Action type** – The finding activity type\. This value can be one of the following: 
    + **NETWORK\_CONNECTION** – indicates that network traffic was exchanged between the identified EC2 instance and the remote host\.
    + **PORT\_PROBE** – indicates that a remote host probed the identified EC2 instance on multiple open ports\.
    + **DNS\_REQUEST** – indicates that the identified EC2 instance queried a domain name\.
    + **AWS\_API\_CALL** – indicates that an AWS API was invoked\.
  + **Connection direction** – The network connection direction observed in the activity that prompted GuardDuty to generate the finding\. The values can be one of the following:
    + **INBOUND** – indicates that a remote host initiated a connection to a local port on the identified EC2 instance in your account\.
    + **OUTBOUND** – indicates that the identified EC2 instance initiated a connection to a remote host\.
    + **UNKNOWN** – indicates that GuardDuty could not determine the direction of the connection\.
  + **Protocol** – the network connection protocol observed in the activity that prompted GuardDuty to generate the finding\. 
  + **Local IP** – The original source IP of the traffic that triggered the finding\. This info can be used to distinguish between the IP address of an intermediate layer through which traffic flows, and the original source IP address of the traffic that triggered the finding\. For example the IP address of an EKS pod as opposed to the IP address of the instance on which the EKS pod is running\. 
  + **API** – the name of the API operation that was invoked and thus prompted GuardDuty to generate this finding\. 
**Note**  
These operations can also include non\-API events captured by CloudTrail\. For more information, see [Non\-API events captured by CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-non-api-events.html)\.
  + **Service name** – the DNS name of the AWS service that attempted to make the API call that triggered the finding\. 
+ A finding will have an **Actor** section if the **Resource role** was `TARGET`\. This indicates your resource was targeted by suspicious activity, and the **Actor** section will contain details on the entity that targeted your resource\.

  A finding will have a **Target** section if the **Resource role** was `ACTOR`\. This indicates your resource was involved in suspicious activity against a remote host, and this section will contain information on the IP and/or domain that your resource targeted\.

  The information available in an **Actor** or **Target** section can include the following:
  + **IP address** – the IP address involved in the activity that prompted GuardDuty to generate the finding\.
  + **Location** – location information of the IP address involved in the activity that prompted GuardDuty to generate the finding\.
  + **Organization** – ISP organization information of the IP address involved in the activity that prompted GuardDuty to generate the finding\. 
  + **Port** – the port number involved in the activity that prompted GuardDuty to generate the finding\.
  + **Domain** – the domain involved in the activity that prompted GuardDuty to generate the finding\.
+ A finding's **Additional information** section that can include the following information:
  + **Threat list name** \- the name of the threat list that includes the IP address or the domain name involved in the activity that prompted GuardDuty to generate the finding\. 
  + **Sample** – a true or false value that indicates whether this is a sample finding\.
  + **Archived** – a true or false value that indicates whether this is finding has been archived\.
  + **Unusual** – activity details that were not observed historically\. These can include an unusual \(previously not observed\) user, or location, or time\. 
  + **Unusual protocol**– the network connection protocol involved in the activity that prompted GuardDuty to generate the finding\.