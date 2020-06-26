# GuardDuty S3 Finding Types<a name="guardduty_finding-types-s3"></a>

The following findings are specific to S3 bucket resources and will always have a **Resource Type** of `S3Bucket` or `Access Key`\. The severity and details of the findings will differ based on the finding type and the permission associated with the bucket\.

For all S3 Bucket type findings it is recommended that you examine the permissions on the bucket in question and the permissions of any users involved in the finding, if the activity is unexpected consider restricting permissions or reviewing the involved IAM entity for signs of compromise\.

**Topics**
+ [Policy:S3/BucketBlockPublicAccessDisabled](#policy-s3-bucketblockpublicaccessdisabled)
+ [Stealth:S3/ServerAccessLoggingDisabled](#stealth-s3-serveraccessloggingdisabled)

## Policy:S3/BucketBlockPublicAccessDisabled<a name="policy-s3-bucketblockpublicaccessdisabled"></a>

### An IAM principal invoked an API used to disable S3 block public access on a bucket\.<a name="policy-s3-bucketblockpublicaccessdisabled_description"></a>

#### <a name="policy-s3-bucketblockpublicaccessdisabled_severity"></a>

**Default severity: Low**

This finding informs you that Amazon S3 block public access was disabled for the S3 bucket referenced under **AffectedResources**\. When enabled, S3 block public access settings are used to filter the policies or ACLs applied to the bucket to prevent inadvertent public exposure of data\. When S3 block public access is disabled, all policies or ACLs applied to the bucket are used to determine who can access it, including any public access\. 

Typically, S3 block public access is turned off to allow public access to a bucket or the objects in the bucket\. Because S3 block public access is now disabled for this bucket, any policies or ACLs applied to the bucket are now controlling access to the bucket\. This does not mean that the bucket is shared publicly, but you should audit the policies and ACLs applied to the bucket to confirm that appropriate permissions are applied\. 

#### <a name="policy-s3-bucketblockpublicaccessdisabled_remediation"></a>

**Remediation Recommendations:**

 If your use case requires that your S3 buckets be publicly available you should audit the policies and ACLs applied to the bucket to confirm that appropriate permissions are applied\. To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html)

If this activity is unexpected your credentials may be compromised, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:S3/ServerAccessLoggingDisabled<a name="stealth-s3-serveraccessloggingdisabled"></a>

### Amazon S3 server access logging was disabled for a bucket\.<a name="stealth-s3-ServerAccessLoggingDisabled_description"></a>

#### <a name="stealth-s3-ServerAccessLoggingDisabled_severity"></a>

**Default severity: Low**

This finding informs you that Amazon S3 server access logging is disabled for a bucket within your AWS environment\. If disabled, no logs are created for any actions taken on the identified S3 bucket, or the objects in the bucket, unless Amazon S3 object level logging is enabled for this bucket\. Disabling logging is a technique often used by unauthorized users in order to cover their tracks\. This finding is triggered when Amazon S3 server access logging is disabled for a bucket\. To learn more, see [S3 Server Access Logging](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html)\.

#### <a name="pentest-s3-PentooLinux_remediation"></a>

**Remediation Recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\.