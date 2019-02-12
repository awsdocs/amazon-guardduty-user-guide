# GuardDuty Policy Finding Types<a name="guardduty_policy"></a>

This section covers the active Policy threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Policy:IAMUser/RootCredentialUsage](#policy1)

## Policy:IAMUser/RootCredentialUsage<a name="policy1"></a>

### Default severity: Low<a name="policy1_severity"></a>

### Finding description<a name="behavior3_description"></a>

**An API was invoked using root credentials\.**

This finding informs you that the root credentials of your AWS account are being used to make requests to AWS services\. It is recommended that you do NOT use your account's root credentials to access AWS services\. Instead, you can access AWS services using least\-privilege temporary credentials from AWS Security Token Service \(STS\)\. For situations where STS is not supported, you can use IAM user credentials\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.