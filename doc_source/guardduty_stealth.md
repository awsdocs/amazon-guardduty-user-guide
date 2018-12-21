# GuardDuty Stealth Finding Types<a name="guardduty_stealth"></a>

This section covers the active Stealth threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Stealth:IAMUser/PasswordPolicyChange](#stealth1)
+ [Stealth:IAMUser/CloudTrailLoggingDisabled](#stealth2)
+ [Stealth:IAMUser/LoggingConfigurationModified](#stealth3)

## Stealth:IAMUser/PasswordPolicyChange<a name="stealth1"></a>

### Default severity: Low<a name="stealth1_severity"></a>

### Finding description<a name="stealth1_description"></a>

**Account password policy was weakened\.**

Your AWS account password policy was weakened\. For example, it was deleted or updated to require fewer characters, not require symbols and numbers, or required to extend the password expiration period\. This finding can also be triggered by an attempt to update or delete your AWS account password policy\. The AWS account password policy defines the rules that govern what kinds of passwords can be set for your IAM users\. A weaker password policy permits the creation of passwords that are easy to remember and potentially easier to guess, thereby creating a security risk\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

## Stealth:IAMUser/CloudTrailLoggingDisabled<a name="stealth2"></a>

### Default severity: Low<a name="stealth2_severity"></a>

### Finding description<a name="stealth2_description"></a>

**AWS CloudTrail trail was disabled\.**

This finding informs you that a CloudTrail trail within your AWS environment was disabled\. This can be an attacker's attempt to disable logging to cover their tracks by eliminating any trace of their activity while gaining access to your AWS resources for malicious purposes\. This finding can be triggered by a successful deletion or update of a trail\. This finding can also be triggered by a successful deletion of an S3 bucket that stores the logs from a trail that is associated with GuardDuty\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

## Stealth:IAMUser/LoggingConfigurationModified<a name="stealth3"></a>

### Default severity: Medium<a name="stealth3_severity"></a>

### Finding description<a name="stealth3_description"></a>

**A principal invoked an API commonly used to stop CloudTrail logging, delete existing logs, and otherwise eliminate traces of activity in your AWS account\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when the logging configuration in your AWS account is modified under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the StopLogging API\. This can be an indication of an attacker trying to cover their tracks by eliminating any trace of their activity\. 