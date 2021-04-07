# Finding details<a name="guardduty_findings-summary"></a>

In the Amazon GuardDuty console, you can view finding details in a finding summary section\. Finding details vary based on finding type\.

There are two primary details that will determine what kinds of information are available for any finding\. The first is the resource type, which can be `AccessKey`, or `Instance`\. The second detail that determines finding information is **Resource Role**\. Resource role, can be `Target` for access keys, meaning the resource was the target of suspicious activity\. For instance type findings, resource role can also be `Actor`, which means that your resource was the actor carrying out suspicious activity\. This topic describes some of the commonly available details for findings\.

## Finding summary<a name="findings-summary-section"></a>

A finding's summary section contains the most basic identifying features of the finding, including the following information: 
+ **Finding type** – A formatted string representing the type of activity that triggered the finding\. For more information, see [GuardDuty finding format](guardduty_finding-format.md)\.
+ **Finding ID** – A unique Finding ID for this finding type and set of parameters\. New occurrences of activity matching this pattern will be aggregated to the same ID\.
+ **Severity** – a finding's assigned severity level of either High, Medium, or Low\. For more information, see [Severity levels for GuardDuty findings](guardduty_findings.md#guardduty_findings-severity)\.
+ **Region** – the AWS Region in which the finding was generated\. For more information about supported Regions, see [Regions and endpoints](guardduty_regions.md)
+ **Count** – The number of times GuardDuty has aggregated an activity matching this pattern to this finding ID\.
+ **Account ID** – the ID of the AWS account in which the activity took place that prompted GuardDuty to generate this finding\.
+ **Resource ID** – the ID of the AWS resource against which the activity took place that prompted GuardDuty to generate this finding\.
+ **Created at** – the time and date when this finding was first created\. If this value differs from **Updated at**, it indicates that the activity has occurred multiple times and is an ongoing issue\.
**Note**  
Timestamps for findings in the GuardDuty console appear in your local time zone, while JSON exports and CLI outputs display timestamps in UTC\.
+ **Updated at** – The last time this finding was updated with new activity matching the pattern that prompted GuardDuty to generate this finding\.
**Note**  
Timestamps for findings in the GuardDuty console appear in your local time zone, while JSON exports and CLI outputs display timestamps in UTC\.

## Resource<a name="findings-resource-affected"></a>

The **Resource affected** gives details on the AWS resource that was targeted by the trigger activity\. The information available varies based on resource type and action type\.

**Resource role** – The role of the AWS resource that triggered the finding\. This value can be **TARGET** or **ACTOR**, and represents whether your resource was the target of the suspicious activity or the actor that preformed the suspicious activity\.

**Resource type** – the type of the affected resource\. This value is either **AccessKey**, **S3 bucket** or **Instance**\. Depending on the resource type, different finding details are available\. Select a resource option tab to learn about the details available for that resource\.

------
#### [ Instance ]

**Instance details:**

**Note**  
Some instance details may be missing if the instance has already been terminated or if the underlying API invocation originated from an EC2 instance in a different Region when making a cross\-Region API call\.
+ **Instance ID** – the ID of the EC2 instance involved in the activity that prompted GuardDuty to generate the finding\.
+ **Instance Type** – the type of the EC2 instance involved in the finding\.
+ **Launch Time** – the time and date the instance was launched\.
+ **Outpost ARN** – The Amazon Resource Name \(ARN\) of the AWS Outpost\. Only applicable to AWS Outposts instances\. For more information, see [What is AWS Outposts?](https://docs.aws.amazon.com/outposts/latest/userguide/what-is-outposts.html)
+ **Security Group Name** – The name of the Security Group attached to the involved instance\.
+ **Security Group ID** – The ID of the Security Group attached to the involved instance\.
+ **Instance state** – The current state of the targeted instance\.
+ **Availability Zone** – The AWS Region Availability Zone in which the involved instance is located\.
+ **Image ID** – The ID of the Amazon Machine Image used to build the instance involved in the activity\.
+ **Image Description** – A description of the ID of the Amazon Machine Image used to build the instance involved in the activity\.
+ **Tags** – A list of tags attached to this resource, listed in the format of `key`:`value`\.

------
#### [ Access Key ]

**Access Key details:**
+ **Access key ID** – access key ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 
+ **Principal ID** – the principal ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 
+ **User type** – the type of user engaged in the activity that prompted GuardDuty to generate the finding\. For more information, see [CloudTrail userIdentity element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html#cloudtrail-event-reference-user-identity-fields)\.
+ **User name** – The name of the user engaged in the activity that prompted GuardDuty to generate the finding\.

------
#### [ S3 bucket ]

**S3 bucket details:**
+ **Name** – The name of the bucket involved in the finding\.
+ **ARN** – The ARN of the bucket involved in the finding\.
+ **Owner** – The canonical user ID of the user that owns the bucket involved in the finding\. For more information on canonical user IDs see [AWS account identifiers](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html)\.
+ **Type** – The type of bucket finding, can be either **Destination** or **Source**\.
+ ** Default server side encryption** – encryption details for the bucket\.
+ **Bucket Tags** – a list of tags attached to this resource, listed in the format of `key`:`value`\.
+ **Effective Permissions** – An evaluation of all effective permissions and policies on the bucket that indicates whether the involved bucket is publicly exposed\. Values can be PUBLIC or NOT PUBLIC\.

------

## Action<a name="finding-action-section"></a>

A finding's **Action** gives details on the type of activity that triggered the finding\. The information available varies based on action type\.
+ **Action type** – The finding activity type\. This value can be one of the following: 
  + **NETWORK\_CONNECTION** – indicates that network traffic was exchanged between the identified EC2 instance and the remote host\.
  + **PORT\_PROBE** – indicates that a remote host probed the identified EC2 instance on multiple open ports\.
  + **DNS\_REQUEST** – indicates that the identified EC2 instance queried a domain name\.
  + **AWS\_API\_CALL** – indicates that an AWS API was invoked\.
  + **ERROR CODE** – if the finding was triggered by a failed API call this displays the error code for that call\.
+ **Connection direction** – The network connection direction observed in the activity that prompted GuardDuty to generate the finding\. The values can be one of the following:
  + **INBOUND** – indicates that a remote host initiated a connection to a local port on the identified EC2 instance in your account\.
  + **OUTBOUND** – indicates that the identified EC2 instance initiated a connection to a remote host\.
  + **UNKNOWN** – indicates that GuardDuty could not determine the direction of the connection\.
+ **Protocol** – the network connection protocol observed in the activity that prompted GuardDuty to generate the finding\. 
+ **Local IP** – The original source IP of the traffic that triggered the finding\. This info can be used to distinguish between the IP address of an intermediate layer through which traffic flows, and the original source IP address of the traffic that triggered the finding\. For example the IP address of an EKS pod as opposed to the IP address of the instance on which the EKS pod is running\. 
+ **API** – the name of the API operation that was invoked and thus prompted GuardDuty to generate this finding\. 
**Note**  
These operations can also include non\-API events captured by AWS CloudTrail\. For more information, see [Non\-API events captured by CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-non-api-events.html)\.
+ **Service name** – the DNS name of the AWS service that attempted to make the API call that triggered the finding\. 

## Actor or Target<a name="finding-actor-target"></a>

A finding has an **Actor** section if the **Resource role** was `TARGET`\. This indicates that your resource was targeted by suspicious activity, and the **Actor** section contains details on the entity that targeted your resource\.

A finding has a **Target** section if the **Resource role** was `ACTOR`\. This indicates that your resource was involved in suspicious activity against a remote host, and this section contains information on the IP or domain that your resource targeted\.

The information available in the **Actor** or **Target** section can include the following:
+ **IP address** – the IP address involved in the activity that prompted GuardDuty to generate the finding\.
+ **Location** – location information for the IP address involved in the activity that prompted GuardDuty to generate the finding\.
+ **Organization** – ISP organization information of the IP address involved in the activity that prompted GuardDuty to generate the finding\. 
+ **Port** – the port number involved in the activity that prompted GuardDuty to generate the finding\.
+ **Domain** – the domain involved in the activity that prompted GuardDuty to generate the finding\.

## Additional information<a name="finding-additional-info"></a>

All findings have an **Additional information** section that can include the following information:
+ **Threat list name** – the name of the threat list that includes the IP address or the domain name involved in the activity that prompted GuardDuty to generate the finding\. 
+ **Sample** – a true or false value that indicates whether this is a sample finding\.
+ **Archived** – a true or false value that indicates whether this is finding has been archived\.
+ **Unusual** – activity details that were not observed historically\. These can include an unusual \(previously not observed\) user, or location, or time\. 
+ **Unusual protocol**– the network connection protocol involved in the activity that prompted GuardDuty to generate the finding\.

## Anomalous behavior<a name="finding-anomalous"></a>

Findings types that end in **AnomalousBehavior** indicate that the finding was generated by the GuardDuty anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests to your account and identifies anomalous events that are associated with tactics used by adversaries\. The ML model tracks various factors of the API request, such as the user that made the request, the location the request was made from, and the specific API that was requested\. 

Details about which factors of the API request are unusual for the CloudTrail user identity that invoked the request can be found in the finding details\. The identities are defined by the [ CloudTrail userIdentity Element](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html), possible values are: `Root`, `IAMUser`, `AssumedRole`, `FederatedUser`, `AWSAccount` or `AWSService`\. 

In addition to the details available for all GuardDuty findings that are associated with API activity, **AnomalousBehavior** findings have additional details that are outlined in the following section\. These details can be viewed in the console and are also available in the finding's JSON\.
+ **Anomalous APIs** – a list of API requests that were invoked by the user identity in proximity to the primary API request associated with the finding\. This pane further breaks down the details of the API event in the following ways:
  + The first API listed is the primary API, which is the API request associated with the highest\-risk observed activity\. This is the API that triggered the finding and correlates to the attack stage of the finding type\. This is also the API that is detailed under the **Action** section in the console, and in the finding's JSON\.
  + Any other APIs listed are additional anomalous APIs from the listed user identity observed in proximity to the primary API\. If there is only one API on the list, the ML model did not identify any additional API requests from that user identity as anomalous\. 
  + The list of APIs is divided based on whether an API was **successfully called**, or if the API was unsuccessfully called, meaning an error response was received\. The type of error response received is listed above each unsuccessfully\-called API\. Possible error response types are: `access denied`, `access denied exception`, `auth failure`, `instance limit exceeded`, `invalid permission - duplicate`, `invalid permission - not found`, `operation not permitted`\.
  + APIs are categorized by their associated AWS service\. 
**Note**  
For more context, select **Usual APIs** to open a pane that gives details on the top APIs, to a maximum of 20, usually seen for both the user identity and all users within the account\. The APIs are marked **rare** \(less than once a month\), **infrequent** \(a few times a month\), or **frequent** \(daily to weekly\), depending on how often they are used within your account\.
+ **Unusual Behavior \(Account\)** – this section gives additional details on the profiled behavior for your account\. The information tracked in this panel includes:
  + **ASN Org** – The ASN Org the anomalous API call was made from\. 
  + **User Name** – The name of the user that made the anomalous API call\.
  + **User Agent**– the user agent used to make the anomalous API call\. The user agent is the method used to make the call such as `aws-cli` or `Botocore`\.
  + **User Type** – The type of user that made the anomalous API call\. Possible values are `AWS_SERVICE`, `ASSUMED_ROLE`, `IAM_USER`, or `ROLE`\.
+ **Unusual Behavior \(User Identity\)** – this section gives additional details on the profiled behavior for the user identity involved with the finding\. 
  + **ASN Org** – The ASN Org the anomalous API call was made from\. 
  + **User Agent**– the user agent used to make the anomalous API call\. The user agent is the method used to make the call such as `aws-cli` or `Botocore`\.
**Note**  
For more context on Unusual behaviors, select **Usual behaviors** in either the **Account** or **User ID** panel to open a pane that gives details on the expected behavior for you account for each of the following categories: **rare** \(less than once a month\), **infrequent** \(a few times a month\), or **frequent** \(daily to weekly\), depending on how often they are used within your account\.