# Managing Amazon GuardDuty findings<a name="findings_management"></a>

 GuardDuty offers several important features to help you sort, store, and manage your findings\. These features will help you tailor findings to your specific environment, reduce noise from low value findings, and help you focus on threats to your unique AWS environment\. Review the topics on this page to understand how you can use these features to increase the value of GuardDuty's findings\.

**Topics:**

[Filtering findings](guardduty_filter-findings.md)  
Learn how to filter GuardDuty findings based on criteria you specify\.

[Suppression rules](findings_suppression-rule.md)  
Learn how to automatically filter the findings GuardDuty alerts you to through suppression rules\. Suppression rules automatically archive findings based on filters\.

[Working with trusted IP lists and threat lists](guardduty_upload-lists.md)  
Customize the GuardDuty monitoring scope using IP Lists and Threat Lists based on publicly\-routable IP addresses\. Trusted IP lists prevent non\-DNS findings from being generated from IP's you consider trusted, while Threat Intel Lists will cause GuardDuty to alert you of activity from user\-defined IPs\.

[Exporting findings](guardduty_exportfindings.md)  
Configure automatic exporting of your findings to an S3 Bucket so you can maintain records past 30 days\. This historical data can be used to track suspicious activity in your account and help you evaluate whether your remediation actions were successful\.

[Creating custom responses to GuardDuty findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)  
Set up automatic notifications for GuardDuty findings through Amazon CloudWatch events\. You can also automate other tasks through CloudWatch Events to help you respond to findings\. 