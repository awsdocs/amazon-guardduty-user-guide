# Amazon GuardDuty Findings<a name="guardduty_findings"></a>

Amazon GuardDuty generates findings when it detects unexpected and potentially malicious activity in your AWS environment\. You can view and manage your GuardDuty findings on the **Findings** page in the GuardDuty console or by using the GuardDuty CLI or API operations\. You can also view your GuardDuty findings through Amazon CloudWatch events\. For more information, see [Monitoring Amazon GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

This topic describes the following information:


+ [Working with GuardDuty Findings](#guardduty_working-with-findings)
+ [Severity Levels for GuardDuty Findings](#guardduty_findings-severity)
+ [Generating GuardDuty Sample Findings](#guardduty_sample-findings)
+ [Proof of Concept \- Automatically Generating Several Common GuardDuty Findings](#guardduty_findings-scripts)
+ [Amazon GuardDuty Finding Types](guardduty_finding-types.md)
+ [Remediating Security Issues Discovered by Amazon GuardDuty](guardduty_remediate.md)

## Working with GuardDuty Findings<a name="guardduty_working-with-findings"></a>

Use the following procedure to view and manage your GuardDuty findings\.

**To locate, analyze, and manage GuardDuty findings \(console\)**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty), and then choose **Findings**\.

1. Choose a specific finding to view its details\.

   A details pane appears where you can view the following information:

   + A finding's summary section that includes the following information: 

     + **Finding type** – a concise yet readable description of the potential security issue\. For more information, see [Amazon GuardDuty Finding Types](guardduty_finding-types.md)\.

     + **Severity** – a finding's assigned severity level of either High, Medium, or Low\. For more information, see [Severity Levels for GuardDuty Findings](#guardduty_findings-severity)\.

     + **Region** – the AWS region in which the finding was generated\.
**Note**  
For more information about supported regions, see [Amazon GuardDuty Supported Regions](guardduty_regions.md)

     + **Count** – the number of times GuardDuty generated the finding after you enabled GuardDuty in your AWS account\.

     + **Account ID** – the ID of the AWS account in which the activity took place that prompted GuardDuty to generate this finding\.

     + **Resource ID** – the ID of the AWS resource against which the activity took place that prompted GuardDuty to generate this finding\.

     + **Threat list name** \- the name of the threat list that includes the IP address or the domain name involved in the activity that prompted GuardDuty to generate the finding\. 

     + **Last seen** – the time at which the activity took place that prompted GuardDuty to generate this finding\.

   + A finding's **Resource affected** section that includes the following information:

     + **Resource role** – a value that usually is set to **Target ** because the affected resource can be a potential target of an attack\.

     + **Resource type** – the type of the affected resource\. This value is either **AccessKey** or **Instance**\. Currently, supported finding types highlight potentially malicious activity against either EC2 instances or AWS credentials\. For more information, see [Remediating Security Issues Discovered by Amazon GuardDuty](guardduty_remediate.md)\.

     + **Instance ID** – the ID of the EC2 instance involved in the activity that prompted GuardDuty to generate the finding\. 

     + **Port** – the port number for the connection used during the activity that prompted GuardDuty to generate the finding\.

     + **Access key ID** – access key ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 

     + **Principal ID** – the principal ID of the user engaged in the activity that prompted GuardDuty to generate the finding\. 

     + **User type** – the type of user engaged in the activity that prompted GuardDuty to generate the finding\. For more information, see [CloudTrail userIdentity element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html#cloudtrail-event-reference-user-identity-fields)\.

     + **User name** – The name of the user engaged in the activity that prompted GuardDuty to generate the finding\.

   + A finding's **Action** section that can include the following information:

     + **Action type** – the finding activity type\. This value can be one of the following: NETWORK\_CONNECTION, AWS\_API\_CALL, PORT\_PROBE, or DNS\_REQUEST\. NETWORK\_CONNECTION indicates that network traffic was exchanged between the identified EC2 instance and the remote host\. AWS\_API\_CALL indicates that an AWS API was invoked\. DNS\_REQUEST indicates that the identified EC2 instance queried a domain name\. PORT\_PROBE indicates that a remote host probed the identified EC2 instance on multiple open ports\. 

     + **API** – the name of the API operation that was invoked and thus prompted GuardDuty to generate this finding\. 

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

1. To archive or export the finding that you're analyzing, choose the **Actions** menu, and then choose **Archive** or **Export**\. 
**Note**  
Currently in GuardDuty, users from GuardDuty member accounts CANNOT archive findings\.

1. To provide feedback by marking the finding useful or not useful, choose the thumbs up or thumbs down icons\. 

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

Sample findings can help you visualize and analyze the various finding types that GuardDuty generates\. When you generate sample findings, GuardDuty populates your current findings list with one sample finding for each supported finding type\. For more information about GuardDuty finding types, see [Amazon GuardDuty Finding Types](guardduty_finding-types.md)\.

Use the following procedure to generate sample findings\.

****

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\.

1. In the navigation pane, under **Settings**, choose **General**\.

1. On the **Settings** page, under **Sample findings**, choose **Generate sample findings**\.

1. In the navigation pane, under **Findings**, choose **Current**\. The sample findings are displayed on the **Current findings** page\. The title of sample findings always begins with **\[SAMPLE\]**\. Choose a specific sample finding to view its details\.

## Proof of Concept \- Automatically Generating Several Common GuardDuty Findings<a name="guardduty_findings-scripts"></a>

You can use the following [scripts](https://github.com/awslabs/amazon-guardduty-tester) to automatically generate several common Amazon GuardDuty findings\. **guardduty\-tester\.template** uses AWS CloudFormation to create an isolated environment with a bastion host, a tester EC2 instance that you can ssh into, and two target EC2 instances\. Then you can run **guardduty\_tester\.sh** that starts interaction between the tester EC2 instance and the target Windows EC2 instance and the target Linux EC2 instance to simulate five types of common attacks that GuardDuty is built to detect and notify you about with generated findings\.

1. As a prerequisite, you must enable GuardDuty in the same account and region where you want to run the **guardduty\-tester\.template** and **guardduty\_tester\.sh**\. For more information about enabling GuardDuty, see [Setting Up Amazon GuardDuty](guardduty_settingup.md)\.

   You must also generate a new or use an existing EC2 key pair in each region where you want to run these scripts\. This EC2 key pair is used as a parameter in the **guardduty\-tester\.template** script that you use to create a new CloudFormation stack\. For more information about generating EC2 key pairs, see [https://docs\.aws\.amazon\.com/AWSEC2/latest/UserGuide/ec2\-key\-pairs\.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)\.

1. Create a new CloudFormation stack using **guardduty\-tester\.template**\. For detailed instructions about creating a stack, see [https://docs\.aws\.amazon\.com/AWSCloudFormation/latest/UserGuide/cfn\-console\-create\-stack\.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cfn-console-create-stack.html)\. Before you run **guardduty\-tester\.template**, modify it with values for the following parameters: Stack Name to identify your new stack, Availability Zone where you want to run the stack, and Key Pair that you can use to launch the EC2 instances\. Then you can use the corresponding private key to SSH into the EC2 instances\.

   **guardduty\-tester\.template** takes around 10 minutes to run and complete\. It creates your environment and copies **guardduty\_tester\.sh** onto your tester EC2 instance\.

1. In the AWS CloudFormation console, choose the checkbox next to your new running CloudFormation stack\. In the displayed set of tabs, select the **Output** tab\. Note the IP addresses assigned to the bastion host and the tester EC2 instance\. You need both of these IP addresses in order to ssh into the tester EC2 instance\.

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
       IdentityFile ~/.ssh/{your-ssh-key.pem
       ProxyCommand ssh bastion nc %h %p
       ServerAliveInterval 240
   ```

   Now you can call $ ssh tester to login to your target EC2 instance\. For more information about configuring and connecting to EC2 instances through bastion hosts, see [https://aws\.amazon\.com/blogs/security/securely\-connect\-to\-linux\-instances\-running\-in\-a\-private\-amazon\-vpc/](https://aws.amazon.com/blogs/security/securely-connect-to-linux-instances-running-in-a-private-amazon-vpc/)\. 

1. Once connected to the tester EC2 instance, run **guardduty\_tester\.sh** to initiate interaction between your tester and target EC2 instances, simulate attacks, and generate GuardDuty Findings\.