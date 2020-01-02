# Policy Finding Types<a name="guardduty_policy"></a>

This section covers the active Policy threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Policy:IAMUser/S3BlockPublicAccessDisabled](#policy2)
+ [Policy:IAMUser/RootCredentialUsage](#policy1)

## Policy:IAMUser/S3BlockPublicAccessDisabled<a name="policy2"></a>

### Finding description<a name="policy2_description"></a>

**Amazon S3 block public access was disabled for a bucket**

This finding informs you that Amazon S3 block public access was disabled for the S3 bucket referenced under **AffectedResources**\. When enabled, S3 block public access settings are used to filter the policies or ACLs applied to the bucket to prevent inadvertent public exposure of data\. When S3 block public access is disabled, all policies or ACLs applied to the bucket are used to determine who can access it, including any public access\. Typically, S3 block public access is turned off to allow public access to a bucket or the objects in the bucket\. Because S3 block public access is now disabled for this bucket, any policies or ACLs applied to the bucket are now controlling access to the bucket\. This does not mean that the bucket is shared publicly, but you should audit the policies and ACLs applied to the bucket to confirm that appropriate permissions are applied\. To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html)

If you did not disable S3 block public access for the bucket, it may indicate that your credentials are compromised\. To learn more, [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

### Default severity: Low<a name="policy2_severity"></a>

## Policy:IAMUser/RootCredentialUsage<a name="policy1"></a>

### Finding description<a name="policy1_description"></a>

**An API was invoked using root credentials\.**

This finding informs you that the root credentials of your AWS account are being used to make requests to AWS services\. It is recommended that you do NOT use your account's root credentials to access AWS services\. Instead, you can access AWS services using least\-privilege temporary credentials from AWS Security Token Service \(STS\)\. For situations where STS is not supported, you can use IAM user credentials\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

### Default severity: Low<a name="policy1_severity"></a>