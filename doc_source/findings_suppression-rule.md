# Suppression rules<a name="findings_suppression-rule"></a>

## <a name="guardduty_filter-suppression-rule"></a>

A suppression rule is a set of criteria, consisting of a filter attribute paired with a value, used to filter findings by automatically archiving new findings that match the specified criteria\. Suppression rules can be used to filter low\-value findings, false positive findings, or threats you do not intend to act on, to make it easier to recognize the security threats with the most impact to your environment\.

 After you create a suppression rule, new findings that match the criteria defined in the rule are automatically archived as long as the suppression rule is in place\. You can use an existing filter to create a suppression rule or create a suppression rule from a new filter you define\. You can configure suppression rules to suppress entire finding types, or define more granular filter criteria to suppress only specific instances of a particular finding type\. Your suppression rules can be edited at any time\. 

Suppressed findings are not sent to AWS Security Hub, Amazon S3, Detective, or CloudWatch, reducing finding noise level if you consume GuardDuty findings via Security Hub, a third\-party SIEM, or other alerting and ticketing applications\.

GuardDuty continues to generate findings even when they match your suppression rules, however, those findings are automatically marked as **archived**\. The archived finding is stored in GuardDuty for 90\-days and can be viewed at any time during that period\. You can view suppressed findings in the GuardDuty console by selecting **Archived** from the findings table, or through the GuardDuty API using the [ListFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFindings.html) API with a `findingCriteria` criterion of `service.archived` equal to true\. 

**Note**  
In a multi\-account environment only the GuardDuty administrator can create suppression rules\.

## Common use cases for suppression rules and examples<a name="guardduty_suppression-best-practices"></a>

The following finding types have common use cases for applying suppression rules, select the finding name to learn more about that finding, or review the info to build a suppression rule for that finding type from the console\.

**Important**  
GuardDuty recommends that you build suppression rules reactively and only for findings you have repeatedly identified false positives for\.
+ [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration\.OutsideAWS](guardduty_finding-types-iam.md#unauthorizedaccess-iam-instancecredentialexfiltrationoutsideaws) – Use a suppression rule to automatically archive findings generated when VPC networking is configured to route internet traffic such that it egresses from an on\-premises gateway rather than from a VPC Internet Gateway\.

  This finding is generated when networking is configured to route internet traffic such that it egresses from an on\-premises gateway rather than from a VPC Internet Gateway \(IGW\)\. Common configurations, such as using [AWS Outposts](https://docs.aws.amazon.com/outposts/latest/userguide/), or VPC VPN connections, can result in traffic routed this way\. If this is expected behavior, it's recommended that you use suppression rules in and create a rule that consists of two filter criteria\. The first criteria is **finding type**, which should be `UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration`\. The second filter criteria is **API caller IPv4 address** with the IP address or CIDR range of your on\-premises internet gateway\. The example below represents the filter you would use to suppress this finding type based on API caller IP address\.

  ```
  Finding type: UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration API caller IPv4 address: 198.51.100.6
  ```
**Note**  
To include multiple API caller IPs you can add a new API Caller IPv4 address filter for each\.
+ [Recon:EC2/Portscan](guardduty_finding-types-ec2.md#recon-ec2-portscan) – Use a suppression rule to automatically archive findings when using a vulnerability assessment application\. 

  The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `Recon:EC2/Portscan`\. The second filter criteria should match the instance or instances that host these vulnerability assessment tools\. You can use either the **Instance image ID** attribute or the **Tag** value attribute depending on which criteria are identifiable with the instances that host these tools\. The example below represents the filter you would use to suppress this finding type based on instances with a certain AMI\.

  ```
  Finding type: Recon:EC2/Portscan Instance image ID: ami-999999999
  ```
+ [UnauthorizedAccess:EC2/SSHBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-sshbruteforce) – Use a suppression rule to automatically archive findings when it is targeted to bastion instances\.

  If the target of the brute force attempt is a bastion host, this may represent expected behavior for your AWS environment\. If this is the case, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `UnauthorizedAccess:EC2/SSHBruteForce`\. The second filter criteria should match the instance or instances that serve as a bastion host\. You can use either the **Instance image ID** attribute or the **Tag** value attribute depending on which criteria is identifiable with the instances that host these tools\. The example below represents the filter you would use to suppress this finding type based on instances with a certain instance tag value\.

  ```
  Finding type: UnauthorizedAccess:EC2/SSHBruteForce Instance tag value: devops
  ```
+ [Recon:EC2/PortProbeUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeunprotectedport) – Use a suppression rule to automatically archive findings when it is targeted to intentionally exposed instances\.

  There may be cases in which instances are intentionally exposed, for example if they are hosting web servers\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `Recon:EC2/PortProbeUnprotectedPort`\. The second filter criteria should match the instance or instances that serve as a bastion host\. You can use either the **Instance image ID** attribute or the **Tag** value attribute, depending on which criteria is identifiable with the instances that host these tools\. The example below represents the filter you would use to suppress this finding type based on instances with a certain instance tag key in the console\.

  ```
  Finding type: Recon:EC2/PortProbeUnprotectedPort Instance tag key: prod
  ```

## To create suppression rules in GuardDuty<a name="findings_suppression-rules-console"></a>

------
#### [ Console ]

The GuardDuty console allows you to easily visualize, create and manage suppression rules\. Suppression rules are generated in the same manner as filters, and your existing saved filters can be used as suppression rules\. For more information on creating filters see [Filtering findings](guardduty_filter-findings.md)\.

**To create a suppression rule using the console:**

1. On the GuardDuty **Findings** page, choose **Suppress findings** to open the suppression rule panel\.

1. Select **Add filter criteria** in the filter bar to open the filter criteria menu\. Select a criterion from the list and then enter a valid value for that criterion\. To determine the correct values to use you can select a finding that you'd like to suppress from the findings table and review it's details from the same page in the console\. You can continue adding filter criteria until only those findings you want to suppress are listed in the findings table\.

1. Enter a name and a description for the suppression rule\.

1. Choose **Save**\.

You can also create a suppression rule from an existing saved filter\. For more information on creating filters see [Filtering findings](guardduty_filter-findings.md)\.

**To create a suppression rule from a saved filter:**

1. On the GuardDuty **Findings** page, choose **Suppress findings** to open the suppression rule panel\.

1. from the **Saved rules** drop down select a saved filter\.

1. Enter a name and a description for the suppression rule\.

1. Choose **Save**\.

Your suppression rules can be viewed, edited, or deleted at any time by selecting the rule from the **Saved rules** drop down in the console\.

------
#### [ API ]

**To create a suppression rule using API:**

1. You can create suppression rules through the [CreateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html) API\. To do so, specify the filter criteria in a JSON file following the format of the example detailed below\. The below example will suppress any unarchived findings where a DNS request to test\.example\.com was made\.

   ```
   {
           "Criterion": {
               "service.archived": {
                   "Eq": [
                       "false"
                   ]
               },
               "service.action.dnsRequestAction.domain": {
                   "Eq": [
                       "test.example.com"
                   ]
               }
           }
       }
   ```

   For a list of JSON field names and their console equivalent see [Filter attributes](guardduty_filter-findings.md#filter_criteria)\.

   You can test your filter criteria first by using the same JSON criterion in the [ListFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFindings.html) API and confirming that the correct findings have been selected or you can do this through the AWS CLI by following the below example using your own detector ID, and \.json file\.

   ```
    AWS  guardduty list-findings --detector-id 12abc34d567e8fa901bc2d34e56789f0 --finding-criteria file://criteria.json
   ```

1. Upload your filter to be used as suppression rule with the [CreateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html) API or by using the AWS CLI following the example below with your own detector ID, a name for the suppression rule, and \.json file\.

   ```
    AWS  guardduty create-filter --action ARCHIVE --detector-id 12abc34d567e8fa901bc2d34e56789f0 --name yourfiltername --finding-criteria file://criteria.json
   ```

You can view a list of your filters programmatically with the [ListFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFilter.html) API, you can see details of an individual filter by supplying the filter name to the [GetFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFilter.html) API\. Update filters using [UpdateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateFilter.html) or delete them with the [DeleteFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_DeleteFilter.html) API\.

------

## <a name="findings_suppression-rules-api"></a>