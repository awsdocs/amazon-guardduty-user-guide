# Suppression rules<a name="findings_suppression-rule"></a>

## <a name="guardduty_filter-suppression-rule"></a>

A suppression rule is a set of criteria used to filter findings by automatically archiving new findings that match the specified criteria\. Suppression rules can be used to filter low\-value findings, false positive findings, or threats you do not intend to act on, to make it easier to recognize the security threats with the most impact to your environment\.

 After you create a suppression rule, new findings that match the criteria defined in the rule are automatically archived as long as the suppression rule is in place\. You can use an existing filter to create a suppression rule, or define a new filter for the suppression rule as you create it\. You can configure suppression rules to suppress entire finding types, or define more granular filter criteria to suppress only specific instances of a particular finding type\. Your suppression rules can be edited at any time\. 

Suppressed findings are not sent to AWS Security Hub, Amazon S3 or CloudWatch Events, reducing finding noise level if you consume GuardDuty findings via Security Hub or a third\-party SIEM, alerting and ticketing applications\.

GuardDuty continues to generate findings even when they match your suppression rules, however, those findings are automatically marked as "archived"\. The archived finding is stored in GuardDuty for 90\-days and can be viewed at any time during that period\. You can view suppressed findings in the GuardDuty console by selecting **Archived** from the findings table, or through the GuardDuty API using the [ListFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFindings.html) API with a `findingCriteria` criterion of `service.archived` equal to true\. 

## Common use cases for suppression rules<a name="guardduty_suppression-best-practices"></a>

The following are finding types with common use cases for applying suppression rules, select the finding name to learn more about how to apply a suppression rules for that use case\.
+ [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](guardduty_finding-types-iam.md#unauthorizedaccess-iam-instancecredentialexfiltration) – Use a suppression rule to automatically archive findings generated when VPC networking is configured to route Internet traffic such that it egresses from an on\-premises gateway rather than from a VPC Internet Gateway\.
+ [Recon:EC2/Portscan](guardduty_finding-types-ec2.md#recon-ec2-portscan) – Use a suppression rule to automatically archive findings when using a vulnerability assessment application\.
+ [UnauthorizedAccess:EC2/SSHBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-sshbruteforce) – Use a suppression rule to automatically archive findings when it is targeted to bastion instances\.
+ [Recon:EC2/PortProbeUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeunprotectedport) – Use a suppression rule to automatically archive findings when it is targeted to intentionally exposed instances\.

## To create a suppression rule using the console:<a name="findings_suppression-rules-console"></a>

The GuardDuty console allows you to easily visualize, create and manage suppression rules\.

1. On the GuardDuty **Findings** page, choose **Suppress findings**\.

1. Do one of the following:
   + To use an existing filter for the rule, choose the filter from the **Saved rules** drop\-down list\.
   + To create a new rule add filter criteria to create a filter for the suppression rule\. To save the filter for use later, choose **Save** at the end of the filter criteria field\.

1. Enter a name and a description for the suppression rule\.

1. Choose **Save**\.

Your suppression rules can be viewed, edited, or deleted at any time by selecting the rule from the **Saved rules** drop down in the console\.

## <a name="findings_suppression-rules-api"></a>

**To create a suppression rule using API:**

1. You can also create suppression rules through the [CreateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html) API\. You can specify the filter criteria in a JSON file following the format of the example detailed below, which would select any unarchived findings where a DNS request to test\.example\.com was made\.

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

   For a list of JSON field names and their console equivalent see [Filter criteria](guardduty_filter-findings.md#filter_criteria)\.

   You can test your filter criteria first by using the same JSON criterion in the [ListFindings](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFindings.html) API and confirming that the correct findings have been selected or you can do this through the AWS CLI by following the example below using your own detector ID, and \.json file\.

   ```
   aws guardduty list-findings --detector-id 12abc34d567e8fa901bc2d34e56789f0 --finding-criteria file://criteria.json
   ```

1. Upload your filter to be used as suppression rule with the [CreateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html) API or by using the AWS CLI following the example below with your own detector ID, a name for the suppression rule, and \.json file\.

   ```
   aws guardduty create-filter --action ARCHIVE --detector-id 12abc34d567e8fa901bc2d34e56789f0 --name yourfiltername --finding-criteria file://criteria.json
   ```

You can view a list of your filters programmatically with the [ListFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListFilter.html) API, you can see details of an individual filter by supplying the filter name to the [GetFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_GetFilter.html) API\. Update filters using [UpdateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateFilter.html) or delete them with the [DeleteFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_DeleteFilter.html) API\.