# AWS Service Integrations with GuardDuty<a name="guardduty_integrations"></a>

GuardDuty can be integrated with other AWS security services\. These services can ingest data from GuardDuty to allow you to view findings in new ways\. Review the following integration options to learn more about how that service is set up to work with GuardDuty\.

## Integrating GuardDuty with AWS Security Hub<a name="gd-securityhub"></a>

AWS Security Hub collects security data from across your AWS accounts, services, and supported third party partner products to assess the security state of your environment according to industry standards and best practices\. In addition to evaluating your security posture, Security Hub creates a central location for findings across all of your integrated AWS services, and AWS Partner products\. Enabling Security Hub with GuardDuty will automatically allow GuardDuty findings data to be ingested by Security Hub\. 

 For more information about using Security Hub with GuardDuty see [Integration with AWS Security Hub](securityhub-integration.md)\. 

## Integrating GuardDuty with Amazon Detective<a name="gd-detective"></a>

Amazon Detective uses log data from across your AWS accounts to create data visualizations for your resources and IP addresses interacting with your environment\. Detective's visualizations help you quickly and easily investigate security issues\. You can pivot from GuardDuty finding details to information in the Detective console once both services are enabled\. 

 For more information about using Detective with GuardDuty see [Integration with Amazon Detective](detective-integration.md)\. 