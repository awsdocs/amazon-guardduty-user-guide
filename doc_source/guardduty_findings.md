# Findings<a name="guardduty_findings"></a>

GuardDuty generates findings when it detects unexpected and potentially malicious activity in your AWS environment\. You can view and manage your GuardDuty findings on the **Findings** page in the GuardDuty console or by using the GuardDuty CLI or API operations\. You can also view your GuardDuty findings through Amazon CloudWatch events\. For more information, see [Monitoring GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

This topic describes the following information:

**Topics**
+ [Locating and Analyzing GuardDuty Findings](#guardduty_working-with-findings)
+ [Archiving, Downloading, and Providing Feedback on GuardDuty Findings](#guardduty_archive-findings)
+ [Filtering Findings](#guardduty_filter-findings)
+ [Suppression Rules](#guardduty_filter-suppression-rule)
+ [Severity Levels for GuardDuty Findings](#guardduty_findings-severity)
+ [Generating GuardDuty Sample Findings](#guardduty_sample-findings)
+ [Proof of Concept \- Automatically Generating Several Common GuardDuty Findings](#guardduty_findings-scripts)
+ [GuardDuty Finding Format](guardduty_finding-format.md)
+ [Active Finding Types](guardduty_finding-types-active.md)
+ [Retired Finding Types](guardduty_finding-types-retired.md)
+ [Remediating Security Issues Discovered by GuardDuty](guardduty_remediate.md)

## Locating and Analyzing GuardDuty Findings<a name="guardduty_working-with-findings"></a>

Use the following procedure to view and analyze your GuardDuty findings\.

****

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty), and then choose **Findings**\.

1. Choose a specific finding to view its details\.

   A details pane appears where you can view the following information:
   + A finding's summary section that includes the following information: 
     + **Finding type** – a concise yet readable description of the potential security issue\. For more information, see [GuardDuty Finding Format](guardduty_finding-format.md)\.
     + **Severity** – a finding's assigned severity level of either High, Medium, or Low\. For more information, see [Severity Levels for GuardDuty Findings](#guardduty_findings-severity)\.
     + **Region** – the AWS region in which the finding was generated\.
**Note**  
For more information about supported regions, see [Regions and Endpoints](guardduty_regions.md)
     + **Count** – the number of times GuardDuty generated the finding after you enabled GuardDuty in your AWS account\.
     + **Account ID** – the ID of the AWS account in which the activity took place that prompted GuardDuty to generate this finding\.
     + **Resource ID** – the ID of the AWS resource against which the activity took place that prompted GuardDuty to generate this finding\.
     + **Threat list name** \- the name of the threat list that includes the IP address or the domain name involved in the activity that prompted GuardDuty to generate the finding\. 
     + **Last seen** – the time at which the activity took place that prompted GuardDuty to generate this finding\.
**Note**  
Findings' time stamps in the GuardDuty console appear in your local time zone, while JSON exports and CLI outputs display timestamps in UTC\.
   + A finding's **Resource affected** section that includes the following information:
     + **Resource role** – a value that usually is set to **Target ** because the affected resource can be a potential target of an attack\.
     + **Resource type** – the type of the affected resource\. This value is either **AccessKey** or **Instance**\. Currently, supported finding types highlight potentially malicious activity against either EC2 instances or AWS credentials\. For more information, see [Remediating Security Issues Discovered by GuardDuty](guardduty_remediate.md)\.
     + **Instance ID** – the ID of the EC2 instance involved in the activity that prompted GuardDuty to generate the finding\. 
     + **Port** – the port number for the connection used during the activity that prompted GuardDuty to generate the finding\.
     + **Access key ID** – access key ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 
     + **Principal ID** – the principal ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 
     + **User type** – the type of user engaged in the activity that prompted GuardDuty to generate the finding\. For more information, see [CloudTrail userIdentity element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html#cloudtrail-event-reference-user-identity-fields)\.
     + **User name** – The name of the user engaged in the activity that prompted GuardDuty to generate the finding\.
   + A finding's **Action** section that can include the following information:
     + **Action type** – the finding activity type\. This value can be one of the following: NETWORK\_CONNECTION, AWS\_API\_CALL, PORT\_PROBE, or DNS\_REQUEST\. NETWORK\_CONNECTION indicates that network traffic was exchanged between the identified EC2 instance and the remote host\. AWS\_API\_CALL indicates that an AWS API was invoked\. DNS\_REQUEST indicates that the identified EC2 instance queried a domain name\. PORT\_PROBE indicates that a remote host probed the identified EC2 instance on multiple open ports\. 
     + **API** – the name of the API operation that was invoked and thus prompted GuardDuty to generate this finding\. 
**Note**  
These operations can also include non\-API events captured by CloudTrail\. For more information, see [Non\-API Events Captured by CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-non-api-events.html)\.
     + **Service name** – the name of the AWS service \(GuardDuty\) that generated the finding\. 
     + **Connection direction** – the network connection direction observed in the activity that prompted GuardDuty to generate the finding\. The values can be INBOUND, OUTBOUND, and UNKNOWN\. INBOUND indicates that a remote host initiated a connection to a local port on the identified EC2 instance in your account\. OUTBOUND indicates that the identified EC2 instance initiated a connection to a remote host\. UNKNOWN indicates that GuardDuty could not determine the direction of the connection\.
     + **Protocol** – the network connection protocol observed in the activity that prompted GuardDuty to generate the finding\. 
   + A finding's **Actor** section that can include the following information:
     + **Location** – location information of the IP address involved in the activity that prompted GuardDuty to generate the finding\.
     + **Organization** – ISP organization information of the IP address involved in the activity that prompted GuardDuty to generate the finding\. 
     + **IP address** – the IP address involved in the activity that prompted GuardDuty to generate the finding\.
     + **Port** – the port number involved in the activity that prompted GuardDuty to generate the finding\.
     + **Domain** – the domain involved in the activity that prompted GuardDuty to generate the finding\.
   + A finding's **Additional information** section that can include the following information:
     + **Threat list name** – the name of the threat list that includes the IP address or the domain name involved in the activity that prompted GuardDuty to generate the finding\.
     + **Sample** – indicates whether this is a sample finding\.
     + **Unusual** – activity details that were not observed historically\. These can include an unusual \(previously not observed\) user, or location, or time\. 
     + **Unusual protocol **– the network connection protocol involved in the activity that prompted GuardDuty to generate the finding\.

## Archiving, Downloading, and Providing Feedback on GuardDuty Findings<a name="guardduty_archive-findings"></a>

Use the following procedure to archive your findings or mark them as current and to provide feedback for your GuardDuty findings

****

1. To archive or download a finding, choose it from the list of your findings and then choose the **Actions** menu\. Then choose **Archive** or **Export**\. When you **Export** a finding, you can see its full JSON document\.
**Note**  
Currently in GuardDuty, users from GuardDuty member accounts can't archive findings\.
**Note**  
If, and only if, the confidence level of a GuardDuty finding is set to 0, the **Confidence** field is displayed in the full finding JSON\. The presence of the **Confidence** field set to 0 indicates that this GuardDuty finding is a false positive\.

1. To provide feedback by marking the finding useful or not useful, choose it from the list of your findings and then choose the thumbs up or thumbs down icons\. 

1. To view your archived or current findings, choose the filter icon above the list of findings and then check either the **Archived** or the **Current** checkbox\.

**Important**  
If you archive a finding manually using the procedure above, all subsequent occurrences of this finding \(generated after the archiving is complete\) are added to the list of your current findings\. To never see this finding in your current list, you can auto\-archive it\. For more information, see [Filtering Findings](#guardduty_filter-findings)\.

## Filtering Findings<a name="guardduty_filter-findings"></a>

Use the following procedure to create filters for your GuardDuty findings\.

**To filter findings**

1. Choose the **Add filter criteria** bar above the displayed list of your GuardDuty findings\.

1. In the expanded list of attributes, select the attributes that you want to specify as the criteria for your filter\. For example, **Account ID** and/or **Action type**\. You can specify one attribute or a maximum of 50 attributes as the criteria for a particular filter\. 

   For the complete list of attributes that you can specify as filter criteria, see the details of the [findingCriteria](docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html#API_CreateFilter_RequestSyntax) parameter of the `CreateFilter` operation\.

1. In the displayed text field, specify a value for each selected attribute and then select **Apply**\.
**Note**  
When you use the 'equal to' or 'not equal to' condition to filter on an attribute value, such as Account ID, you can specify a maximum of 50 values\. After you apply a filter, you can convert the filter to exclude findings that match the filter by choosing the black dot to the left side of the filter name\. This effectively creates a "not equals" filter for the selected attribute\.

1. To save the specified attributes and their values \(filter criteria\) as a filter, select **Save**\. Provide the filter name and description, and then choose **Done**\.

## Suppression Rules<a name="guardduty_filter-suppression-rule"></a>

A suppression rule is a filter used to automatically archive new findings\. After you create a suppression rule, new findings that match the criteria defined in the rule are automatically archived\. You can use an existing filter to create a suppression rule, or define a new filter for the supporession rule as you create it\.

**To create a suppression rule**

1. On the GuardDuty **Findings** page, choose **Suppress findings**\.

1. Do one of the following:
   + To use an existing filter for the rule, choose the filter from the **Saved rules** drop\-down list\.
   + Add filter criteria to create a filter for the suppression rule\. To save the filter for use later, choose **Save** at the end of the filter criteria field\.

1. Enter a name and a description for the suppression rule\.

1. Choose **Save**\.

### Common Use Cases and Best Practices for Suppression Rules<a name="guardduty_suppression-best-practices"></a>

One of the most important steps when setting up GuardDuty is to fine\-tune the service to your specific AWS environment\. You can achieve this by using GuardDuty finding suppression rules\. Suppression rules result in reduces noise levels of generated findings, letting you focus on findings that may indicate a security threat\. Noisy findings can represent either activity that is expected for your AWS environment or activity that is not a threat that you intend to act on\. When a finding matches a suppression rule, it is still be generated and stored in GuardDuty for 90\-days\. However, it is automatically marked as “archived”\. Accordingly, it does not appear in the “current findings” section of console, clearing away the noise and enabling you to focus on findings that are of higher security value and represent unexpected behavior for you AWS environment\.

You can still view suppressed findings in the archived section of the findings table\. Suppressed findings are not sent to AWS Security Hub, Amazon S3, CloudWatch Events\. This helps lower the noise level if you consume GuardDuty findings via Security Hub or a third\-party SIEM, alerting and ticketing applications\. As the findings are still generated, we recommend periodically viewing the archived findings to validate that the rules are configured properly to only match findings that you wish to suppress\. You can configure suppression rules to suppress entire finding types, or define more granular filter criteria to suppress only specific instances of a particular finding type\. Following are common use cases for applying suppression rules:

**UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration – Using a suppression rule to automatically archive findings generated when VPC networking is configured to route Internet traffic such that it egresses from an on\-premises gateway rather than from a VPC Internet Gateway**  
The instance credential exfiltration finding informs you of attempts to run AWS API operations from a host outside of EC2, using temporary AWS credentials that were created on an EC2 instance in your AWS account\. This finding may indicate that your EC2 instance is compromised, and the temporary credentials from this instance might have been exfiltrated to a remote host outside of AWS\. If this behavior is unexpected this can indicate a high severity security incident and should be addressed immediately\. However, this finding is generated if VPC networking is configured to route Internet traffic such that it egresses from an on\-premise gateway rather than from a VPC Internet Gateway \(IGW\)\. Common configurations that result in this include using AWS Direct Connect, AWS Outputs, or VPC VPN connections\. To suppress this expected behavior it is recommended that you create a suppression rule that consists of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of *UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration*\. The second filter criteria should use either the IP address or ASN of your on\-premises internet gateway\. For IP\-based filters, use the **API caller IPv4 address** attribute, and for ASN based filters use either the **API caller ASN name** attribute or the **API caller ASN ID** attribute\.

**Recon:EC2/Portscan – Using a suppression rule to automatically archive findings when using a vulnerability assessment application**  
The Portscan finding informs you that there is an EC2 instance in your AWS environment that is engaged in a possible port scan attack because it is trying to connect to multiple ports over a short period of time\. The purpose of a port scan attack is to locate open ports to discover which services that the machine is running and to identify its operating system\. This may indicate that your EC2 instance might be compromised\. However, this finding is often triggered when vulnerability assessment applications are deployed on EC2 Instances in your environment, as these applications conduct portscans to alert you about misconfigured open ports\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of *Recon:EC2/Portscan*\. The second filter criteria should match the instance or instances that host these vulnerability assessment tools\. You can use either the *Instance image ID* attribute or the *Tag value* attribute depending on what criteria is identifiable with the instances that host these tools\.

**UnauthorizedAccess:EC2/SSHBruteForce – Using a suppression rule to automatically archive findings when it is targeted to bastion instances**  
The SSH Brut Force finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to SSH services on Linux\-based systems\. This can indicate unauthorized access to your AWS resources\. However, if the target of the SSH bruteforce attempt is a bastion host, this may represent expected behavior for your AWS environment\. If this is the case, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of *UnauthorizedAccess:EC2/SSHBruteForce*\. The second filter criteria should match the instance or instances that serve as a bastion host\. You can use either the **Instance image ID** attribute or the **Tag value** attribute depending on what criteria is identifiable with the instances that host these tools\.

**Recon:EC2/PortProbeUnprotectedPort – Using a suppression rule to automatically archive findings when it is targeted to intentionally exposed instances**  
The Port Probe finding informs you that a port on an EC2 instance in your AWS environment is not blocked by a security group, access control list \(ACL\), or an on\-host firewall \(for example, Linux IPTables\), and known scanners on the internet are actively probing it\. However, there may be cases in which instances are intentionally exposed, for example if they are hosting web servers\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of *Recon:EC2/PortProbeUnprotectedPort*\. The second filter criteria should match the instance or instances that serve as a bastion host\. You can use either the **Instance image ID** attribute or the **Tag value** attribute depending on what criteria is identifiable with the instances that host these tools\.

## Severity Levels for GuardDuty Findings<a name="guardduty_findings-severity"></a>

Each GuardDuty finding has an assigned severity level and value that reduces the need to prioritize one finding over another and can help you determine your response to a potential security issue that is highlighted by a finding\. The value of the severity can fall anywhere within the 0\.1 to 8\.9 range\. 

**Note**  
Values 0 and 9\.0 to 10\.0 are currently reserved for future use\.

The following are the currently defined severity levels and values for the GuardDuty findings:
+ **High** \(the value of the **severity** parameter in the [GetFindings](get-findings.md) response falls within the 7\.0 to 8\.9 range\) – indicates that the resource in question \(an EC2 instance or a set of IAM user credentials\) is compromised and is actively being used for unauthorized purposes\. We recommend that you treat this security issue as a priority and take immediate remediation steps\. For example, clean up your EC2 instance or terminate it, or rotate the IAM credentials\.
+ **Medium** \(the value of the **severity** parameter in the [GetFindings](get-findings.md) response falls within the 4\.0 to 6\.9 range\) – indicates suspicious activity, for example, a large amount of traffic being returned to a remote host that is hiding behind the Tor network, or activity that deviates from normally observed behavior\. We recommend that you investigate the implicated resource at your earliest convenience\. Here are some of the possible remediation steps:
  + Check if an authorized user has installed new software that changed the behavior of a resource \(for example, allowed higher than normal traffic, or enabled communication on a new port\)\.
  + Check if an authorized user changed the control panel settings, for example, modified a security group setting
  + Run an anti\-virus scan on the implicated resource to detect unauthorized software\.
  + Verify the permissions that are attached to the implicated IAM role, user, group, or set of credentials\. These might have to be changed or rotated\.
+ **Low** \(the value of the **severity** parameter in the [GetFindings](get-findings.md) response falls within the 0\.1 to 3\.9 range\) \- indicates suspicious or malicious activity that was blocked before it compromised your resource\. There is no immediate recommended action, but it is worth making note of this information as something to address in the future\. 

## Generating GuardDuty Sample Findings<a name="guardduty_sample-findings"></a>

Sample findings can help you visualize and analyze the various finding types that GuardDuty generates\. When you generate sample findings, GuardDuty populates your current findings list with one sample finding for each supported finding type\. For more information about GuardDuty finding types, see [Active Finding Types](guardduty_finding-types-active.md)\.

Use the following procedure to generate sample findings\.

****

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\.

1. In the navigation pane, under **Settings**, choose **General**\.

1. On the **Settings** page, under **Sample findings**, choose **Generate sample findings**\.

1. In the navigation pane, under **Findings**, choose **Current**\. The sample findings are displayed on the **Current findings** page\. The title of sample findings always begins with **\[SAMPLE\]**\. Choose a specific sample finding to view its details\.

## Proof of Concept \- Automatically Generating Several Common GuardDuty Findings<a name="guardduty_findings-scripts"></a>

You can use the following [scripts](https://github.com/awslabs/amazon-guardduty-tester) to automatically generate several common GuardDuty findings\. **guardduty\-tester\.template** uses AWS CloudFormation to create an isolated environment with a bastion host, a tester EC2 instance that you can ssh into, and two target EC2 instances\. Then you can run **guardduty\_tester\.sh** that starts interaction between the tester EC2 instance and the target Windows EC2 instance and the target Linux EC2 instance to simulate five types of common attacks that GuardDuty is built to detect and notify you about with generated findings\.

1. As a prerequisite, you must enable GuardDuty in the same account and region where you want to run the **guardduty\-tester\.template** and **guardduty\_tester\.sh**\. For more information about enabling GuardDuty, see [Setting Up GuardDuty](guardduty_settingup.md)\.

   You must also generate a new or use an existing EC2 key pair in each region where you want to run these scripts\. This EC2 key pair is used as a parameter in the **guardduty\-tester\.template** script that you use to create a new CloudFormation stack\. For more information about generating EC2 key pairs, see [https://docs\.aws\.amazon\.com/AWSEC2/latest/UserGuide/ec2\-key\-pairs\.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)\.

1. Create a new CloudFormation stack using **guardduty\-tester\.template**\. For detailed instructions about creating a stack, see [https://docs\.aws\.amazon\.com/AWSCloudFormation/latest/UserGuide/cfn\-console\-create\-stack\.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html)\. Before you run **guardduty\-tester\.template**, modify it with values for the following parameters: Stack Name to identify your new stack, Availability Zone where you want to run the stack, and Key Pair that you can use to launch the EC2 instances\. Then you can use the corresponding private key to SSH into the EC2 instances\.

   **guardduty\-tester\.template** takes around 10 minutes to run and complete\. It creates your environment and copies **guardduty\_tester\.sh** onto your tester EC2 instance\.

1. In the AWS CloudFormation console, choose the checkbox next to your new running AWS CloudFormation stack\. In the displayed set of tabs, select the **Output** tab\. Note the IP addresses assigned to the bastion host and the tester EC2 instance\. You need both of these IP addresses in order to ssh into the tester EC2 instance\.

1. Create the following entry in your \~/\.ssh/config file to login to your instance through the bastion host:

   ```
   Host bastion
       HostName {Elastic IP Address of Bastion}
       User ec2-user
       IdentityFile ~/.ssh/{your-ssh-key.pem}
   Host tester
       ForwardAgent yes
       HostName {Local IP Address of RedTeam Instance}
       User ec2-user
       IdentityFile ~/.ssh/{your-ssh-key.pem}
       ProxyCommand ssh bastion nc %h %p
       ServerAliveInterval 240
   ```

   Now you can call $ ssh tester to login to your target EC2 instance\. For more information about configuring and connecting to EC2 instances through bastion hosts, see [https://aws\.amazon\.com/blogs/security/securely\-connect\-to\-linux\-instances\-running\-in\-a\-private\-amazon\-vpc/](https://aws.amazon.com/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/)\. 

1. Once connected to the tester EC2 instance, run **guardduty\_tester\.sh** to initiate interaction between your tester and target EC2 instances, simulate attacks, and generate GuardDuty Findings\.