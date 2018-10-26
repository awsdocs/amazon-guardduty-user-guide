# Document History for Amazon GuardDuty<a name="doc-history"></a>

| Change | Description | Date | 
| --- |--- |--- |
| [Added support for updating the frequency of notifications sent to CloudWatch Events](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings_cloudwatch.html) | You can now update the frequency of notifications sent to CloudWatch Events for the subsequent occurrences of existing findings\. Possible values are 15 minutes, 1 hour, or the default 6 hours\. [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings_cloudwatch.html) | October 9, 2018 | 
| [Added region support](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html) |  Added region support for AWS GovCloud \(US\) [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html) | July 25, 2018 | 
| [Added support for AWS CloudFormation StackSets in GuardDuty](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_accounts.html) |  You can use the Enable Amazon GuardDuty template to enable GuardDuty simultaneously in multiple accounts\. [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_accounts.html) | June 25, 2018 | 
| [Added support for GuardDuty auto\-archive rules](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html#guardduty_filter-findings) |  Customers can now build granular auto\-archive rules for suppression of findings\. For findings that match an auto\-archive rule, GuardDuty automatically marks them as archived\. This enables customers to further tune GuardDuty to keep only relevant findings in the current findings table\. [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings.html#guardduty_filter-findings) | May 4, 2018 | 
| [GuardDuty is available in the EU \(Paris\) region](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html) | GuardDuty is now available in EU \(Paris\), allowing you to extend continuous security monitoring and threat detection to AWS' newest EU region\. [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_regions.html) | March 29, 2018 | 
| [Creating GuardDuty master and member accounts through AWS CloudFormation is now supported\.](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-master.html) | For more information, see [AWS::GuardDuty::Master](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-master.html) and [AWS::GuardDuty::Member](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-member.html)\. | March 6, 2018 | 
| [Added nine new CloudTrail\-based anomaly detections\.](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types.html) | These new finding types are automatically enabled in GuardDuty in all supported regions\.[ Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types.html) | February 28, 2018 | 
| [Added three new threat intelligence detections \(finding types\)\. ](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types.html) | These new finding types are automatically enabled in GuardDuty in all supported regions\. [Learn more ](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_finding-types.html) | February 5, 2018 | 
| [Limit increase for GuardDuty member accounts\. ](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_accounts.html) | With this release, you can have up to 1000 GuardDuty member accounts added per AWS account \(GuardDuty master account\)\. [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_accounts.html) | January 25, 2018 | 
| [Changes in upload and further management of trusted IP lists and threat lists for GuardDuty master and member accounts\. ](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_upload_lists.html) | With this release, Users from master GuardDuty accounts can upload and manage trusted IP lists and threat lists\. Users from member GuardDuty accounts CANNOT upload and manage lists\. Trusted IP lists and threat lists that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. [Learn more](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_upload_lists.html) | January 25, 2018 | 

The following table describes important changes in each release of the *GuardDuty* User Guide\.

## Earlier updates<a name="doc-history-early-changes"></a>


****  

| Change | Description | Date | 
| --- | --- | --- | 
| Initial publication | Initial publication of the Amazon GuardDuty User Guide\. | November 28, 2017 | 