# Understanding Amazon GuardDuty findings<a name="guardduty_findings"></a>

 A GuardDuty finding represents a potential security issue detected within your network\. GuardDuty generates a finding whenever it detects unexpected and potentially malicious activity in your AWS environment\.

You can view and manage your GuardDuty findings on the **Findings** page in the GuardDuty console or by using the GuardDuty CLI or API operations\. For an overview of the ways you can manage findings see [Managing Amazon GuardDuty findings](findings_management.md)\.

**Topics:**

[Finding details](guardduty_findings-summary.md)  
Learn about the types of data available within GuardDuty findings\.

[Sample findings](sample_findings.md)  
Learn how to generate sample findings to test or better understand GuardDuty\.

[GuardDuty finding format](guardduty_finding-format.md)  
Understand the format of GuardDuty finding types and the different threat purposes tracked by GuardDuty\.

[Finding types](guardduty_finding-types-active.md)  
View and search all available GuardDuty finding by type\. Each finding type entry includes an explanation of that finding as well as tips and suggestions for remediation\.

## Severity levels for GuardDuty findings<a name="guardduty_findings-severity"></a>

Each GuardDuty finding has an assigned severity level and value that reflects the potential risk the finding could have to your network as determined by our security engineers\. The value of the severity can fall anywhere within the 0\.1 to 8\.9 range, with higher values indicating greater security risk\. To help you determine a response to a potential security issue that is highlighted by a finding, GuardDuty breaks down this range into, High, Medium, and Low severity levels\.

**Note**  
Values 0 and 9\.0 to 10\.0 are currently reserved for future use\.

The following are the currently defined severity levels and values for the GuardDuty findings as well as general recommendations for each:


| Severity level | Value range | 
| --- | --- | 
| **High**  | 8\.9 \- 7\.0  | 
| A High severity level indicates that the resource in question \(an EC2 instance or a set of IAM user credentials\) is compromised and is actively being used for unauthorized purposes\.   We recommend that you treat any High severity finding security issue as a priority and take immediate remediation steps to prevent further unauthorized use of your resources\. For example, clean up your EC2 instance or terminate it, or rotate the IAM credentials\. See [Remediation Steps](guardduty_remediate.md) for more details\.  | 
| **Medium**  | 6\.9 \- 4\.0  | 
| A Medium severity level indicates suspicious activity that deviates from normally observed behavior and, depending on your use case, may be indicative of a resource compromise\.   We recommend that you investigate the implicated resource at your earliest convenience\. Remediation steps will vary by resource and Finding family, but in general, you should be looking to confirm that the activity is authorized and consistent with your use case\. If you cannot identify the cause or confirm the activity was authorized you should consider the resource compromised and follow [Remediation Steps](guardduty_remediate.md) to secure the resource\.  Here are some things to consider when reviewing a Medium level finding: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html)  | 
| **Low**  | 3\.9 \- 1\.0  | 
| A low severity level indicates attempted suspicious activity that did not compromise your network, for example, a port scan or a failed intrusion attempt\. There is no immediate recommended action, but it is worth making note of this information as it may indicate someone is looking for weak points in your network\.  | 

## GuardDuty finding aggregation<a name="finding-aggregation"></a>

All findings are dynamic, meaning that if GuardDuty detects new activity related to the same security issue it will update the original finding with the new information instead of generating a new finding\. This behaviour allows you to identify ongoing issues without needing to look through multiple similar reports, and reduces the overall noise from security issues you are already aware of\.

For example, for a UnauthorizedAccess:EC2/SSHBruteForce finding, multiple access attempts against your instance will be aggregated to the same finding ID, increasing the Count number in the finding's details\. This is because that finding represents a single security issue with the instance indicating that the SSH port on the instance is not properly secured against this type of activity\. However, if GuardDuty detects SSH access activity targeting a new instance in your environment, it will create a new finding with a unique finding ID to alert you to the fact that there is a security issue associated with the new resource\.

When a finding is aggregated it will be updated with information from the latest occurrence of that activity, meaning that in the above example if your instance is the target of a brute force attempt from a new actor, the finding details will be updated to reflect the remote IP of the most recent source and older information will be replaced\. Full Information about individual activity attempts will still be available in your CloudTrail or VPC flow logs\.

The criteria that trigger GuardDuty to generate a new finding instead of aggregating an existing one is dependent on the finding type\. The aggregation criteria for each finding type are determined by our security engineers to give you the best overview of distinct security issues within your account\.

## Locating and analyzing GuardDuty findings<a name="guardduty_working-with-findings"></a>

Use the following procedure to view and analyze your GuardDuty findings\.

****

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Findings** and then select a specific finding to view its details\.

   The details for each finding will differ depending on the Finding type, resources involved, and nature of the activity\. For more information on available finding fields see [Finding details](guardduty_findings-summary.md)\.

1. \(Optional\) If you wish to archive a finding select it from the list of your findings and then choose the **Actions** menu\. Then choose **Archive**\. 

   Archived findings can be viewed by choosing **Archived** from the **Current** dropdown\.

   Currently in GuardDuty, users from GuardDuty member accounts can't archive findings\.
**Important**  
If you archive a finding manually using the procedure above, all subsequent occurrences of this finding \(generated after the archiving is complete\) are added to the list of your current findings\. To never see this finding in your current list, you can auto\-archive it\. For more information, see [Suppression rules](findings_suppression-rule.md)\.

1. \(Optional\) To download a finding, select it from the list of your findings and then choose the **Actions** menu\. Then choose **Export**\. When you **Export** a finding, you can see its full JSON document\.
**Note**  
If, and only if, the confidence level of a GuardDuty finding is set to 0, the **Confidence** field is displayed in the full finding JSON\. The presence of the **Confidence** field set to 0 indicates that this GuardDuty finding is a false positive\.