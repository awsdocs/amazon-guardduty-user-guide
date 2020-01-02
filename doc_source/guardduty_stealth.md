# Stealth Finding Types<a name="guardduty_stealth"></a>

This section covers the active Stealth threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Stealth:IAMUser/S3ServerAccessLoggingDisabled](#stealth4)
+ [Stealth:IAMUser/PasswordPolicyChange](#stealth1)
+ [Stealth:IAMUser/CloudTrailLoggingDisabled](#stealth2)
+ [Stealth:IAMUser/LoggingConfigurationModified](#stealth3)

## Stealth:IAMUser/S3ServerAccessLoggingDisabled<a name="stealth4"></a>

### Finding description<a name="stealth4_description"></a>

**Amazon S3 server access logging was disabled for a bucket**

This finding informs you that Amazon S3 server access logging is disabled for a bucket within your AWS environment\. If disabled, no logs are created for any actions taken on the identified S3 bucket, or the objects in the bucket, unless Amazon S3 object level logging is enabled for this bucket\. Disabling logging is a technique often used by unauthorized users in order to cover their tracks\. This finding is triggered when Amazon S3 server access logging is disabled for a bucket\. To learn more, see [S3 Server Access Logging](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html)\. 

If you did not disable Amazon S3 server access logging for the identified bucket, it may indicate that your credentials are compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

### Default severity: Low<a name="stealth4_severity"></a>

## Stealth:IAMUser/PasswordPolicyChange<a name="stealth1"></a>

### Finding description<a name="stealth1_description"></a>

**Account password policy was weakened\.**

Your AWS account password policy was weakened\. For example, it was deleted or updated to require fewer characters, not require symbols and numbers, or required to extend the password expiration period\. This finding can also be triggered by an attempt to update or delete your AWS account password policy\. The AWS account password policy defines the rules that govern what kinds of passwords can be set for your IAM users\. A weaker password policy permits the creation of passwords that are easy to remember and potentially easier to guess, thereby creating a security risk\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

### Default severity: Low<a name="stealth1_severity"></a>

## Stealth:IAMUser/CloudTrailLoggingDisabled<a name="stealth2"></a>

### Finding description<a name="stealth2_description"></a>

**AWS CloudTrail trail was disabled\.**

This finding informs you that a CloudTrail trail within your AWS environment was disabled\. This can be an attacker's attempt to disable logging to cover their tracks by eliminating any trace of their activity while gaining access to your AWS resources for malicious purposes\. This finding can be triggered by a successful deletion or update of a trail\. This finding can also be triggered by a successful deletion of an S3 bucket that stores the logs from a trail that is associated with GuardDuty\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

### Default severity: Low<a name="stealth2_severity"></a>

## Stealth:IAMUser/LoggingConfigurationModified<a name="stealth3"></a>

### Finding description<a name="stealth3_description"></a>

**A principal invoked an API commonly used to stop CloudTrail logging, delete existing logs, and otherwise eliminate traces of activity in your AWS account\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that is different from the established baseline\. This principal has no prior history of invoking this API\. Your credentials might be compromised\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

This finding is triggered when the logging configuration in your AWS account is modified under suspicious circumstances\. For example, if a principal with no prior history of doing so, invoked the StopLogging API\. This can be an indication of an attacker trying to cover their tracks by eliminating any trace of their activity\. 

### Default severity: Medium<a name="stealth3_severity"></a>

This finding’s default severity is Medium\. However, if the API is invoked using temporary AWS credentials that are created on an Amazon EC2 instance, the finding’s severity is High\.