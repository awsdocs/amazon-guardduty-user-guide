# Document History for Amazon GuardDuty<a name="doc-history"></a>

The following table describes the documentation for this release of GuardDuty\.
+ **API version:** 1\.0
+ **Latest documentation update:** January 25, 2018


****  

| Change | Description | Date | 
| --- | --- | --- | 
| Initial publication | Initial publication of the Amazon GuardDuty User Guide\. | November 28, 2017 | 
| Limit increase for GuardDuty member accounts | With this release, you can have up to 1000 GuardDuty member accounts added per AWS account \(GuardDuty master account\)\.  | January 25, 2018 | 
| Changes in upload and further management of trusted IP lists and threat lists for GuardDuty master and member accounts | With this release, Users from master GuardDuty accounts can upload and manage trusted IP lists and threat lists\. Users from member GuardDuty accounts CANNOT upload and manage lists\. Trusted IP lists and threat lists that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md) and [Working with Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)\.  | January 25, 2018 | 
| Added the following three threat intelligence detections \(finding types\): [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/doc-history.html)  | These new finding types are automatically enabled in GuardDuty in all supported regions\. For more information, see [Amazon GuardDuty Finding Types](guardduty_finding-types.md)\. | February 5, 2018 | 
| Added the following nine CloudTrail\-based anomaly detections \(finding types\): [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/doc-history.html)  | These new finding types are automatically enabled in GuardDuty in all supported regions\. For more information, see [Amazon GuardDuty Finding Types](guardduty_finding-types.md)\. | February 28, 2018 | 
| Creating GuardDuty master and member accounts through AWS CloudFormation is now supported\.  | For more information, see [AWS::GuardDuty::Master](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-master.html) and [AWS::GuardDuty::Member](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-member.html)\. | March 6, 2018 | 
| GuardDuty is available in the EU \(Paris\) region | GuardDuty is now available in EU \(Paris\), allowing you to extend continuous security monitoring and threat detection to AWS' newest EU region\.  | March 29, 2018 | 