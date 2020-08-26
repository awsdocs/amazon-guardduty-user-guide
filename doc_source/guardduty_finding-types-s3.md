# GuardDuty S3 finding types<a name="guardduty_finding-types-s3"></a>

The following findings are specific to S3 bucket resources and will always have a Resource Type of `S3Bucket`\. The severity and details of the findings will differ based on the finding type and the permission associated with the bucket\.

For all S3 Bucket type findings it is recommended that you examine the permissions on the bucket in question and the permissions of any users involved in the finding, if the activity is unexpected see the remediation recommendations detailed in [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

**Topics**
+ [Discovery:S3/BucketEnumeration\.Unusual](#discovery-s3-bucketenumerationunusual)
+ [Discovery:S3/MaliciousIPCaller\.Custom](#discovery-s3-maliciousipcallercustom)
+ [Discovery:S3/TorIPCaller](#discovery-s3-toripcaller)
+ [Exfiltration:S3/ObjectRead\.Unusual](#exfiltration-s3-objectreadunusual)
+ [Impact:S3/PermissionsModification\.Unusual](#impact-s3-permissionsmodificationunusual)
+ [Impact:S3/ObjectDelete\.Unusual](#impact-s3-objectdeleteunusual)
+ [PenTest:S3/KaliLinux](#pentest-s3-kalilinux)
+ [PenTest:S3/ParrotLinux](#pentest-s3-parrotlinux)
+ [PenTest:S3/PentooLinux](#pentest-s3-pentoolinux)
+ [Policy:S3/AccountBlockPublicAccessDisabled](#policy-s3-accountblockpublicaccessdisabled)
+ [Policy:S3/BucketBlockPublicAccessDisabled](#policy-s3-bucketblockpublicaccessdisabled)
+ [Policy:S3/BucketAnonymousAccessGranted](#policy-s3-bucketanonymousaccessgranted)
+ [Policy:S3/BucketPublicAccessGranted](#policy-s3-bucketpublicaccessgranted)
+ [Stealth:S3/ServerAccessLoggingDisabled](#stealth-s3-serveraccessloggingdisabled)
+ [UnauthorizedAccess:S3/MaliciousIPCaller\.Custom](#unauthorizedaccess-s3-maliciousipcallercustom)
+ [UnauthorizedAccess:S3/TorIPCaller](#unauthorizedaccess-s3-toripcaller)

## Discovery:S3/BucketEnumeration\.Unusual<a name="discovery-s3-bucketenumerationunusual"></a>

### An IAM entity invoked an S3 API used to discover S3 buckets within your network\.<a name="discovery-s3-bucketenumerationunusual_description"></a>

#### <a name="discovery-s3-bucketenumerationunusual_severity"></a>

**Default severity: Medium**

This finding informs you that an IAM entity has invoked an S3 API to discover S3 buckets in your environment, such as `ListBuckets`\. This type of activity is associated with the discovery stage of an attack wherein an attacker is gathering information to determine if your AWS environment is susceptible to a broader attack\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="discovery-s3-bucketenumerationunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Discovery:S3/MaliciousIPCaller\.Custom<a name="discovery-s3-maliciousipcallercustom"></a>

### An S3 API was invoked from an IP address on a custom threat list\.<a name="discovery-s3-maliciousipcallercustom_description"></a>

#### <a name="discovery-s3-maliciousipcallercustom_severity"></a>

**Default severity: Medium**

This finding informs you that an S3 API, such as `GetObjectAcl` or `ListObjects`, was invoked from an IP address that is included on a threat list that you uploaded\. The threat list associated with this finding is listed in the **Additional information** section of a finding's details\. This type of activity is associated with the discovery stage of an attack wherein an attacker is gathering information to determine if your AWS environment is susceptible to a broader attack\.

#### <a name="discovery-s3-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Discovery:S3/TorIPCaller<a name="discovery-s3-toripcaller"></a>

### An S3 API was invoked from a Tor exit node IP address\.<a name="discovery-s3-toripcaller_description"></a>

#### <a name="discovery-s3-toripcaller_severity"></a>

**Default severity: Medium**

This finding informs you that an S3 API, such as `GetObjectAcl` or `ListObjects`, was invoked from a Tor exit node IP address\. This type of activity is associated with the discovery stage of an attack wherein an attacker is gathering information to determine if your AWS environment is susceptible to a broader attack\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="discovery-s3-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Exfiltration:S3/ObjectRead\.Unusual<a name="exfiltration-s3-objectreadunusual"></a>

### An IAM entity invoked an S3 API in a suspicious way\.<a name="exfiltration-s3-objectreadunusual_description"></a>

#### <a name="exfiltration-s3-objectreadunusual_severity"></a>

**Default severity: Medium**

This finding informs you that a IAM entity in your AWS environment is making API calls that involve an S3 bucket and that differ from that entity's established baseline\. The API call used in this activity is associated with the exfiltration stage of an attack, wherein and attacker is attempting to collect data\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="exfiltration-s3-objectreadunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Impact:S3/PermissionsModification\.Unusual<a name="impact-s3-permissionsmodificationunusual"></a>

### An IAM entity invoked an API to modify permissions on one or more S3 resources\.<a name="impact-s3-permissionsmodificationunusual_description"></a>

#### <a name="impact-s3-permissionsmodificationunusual_severity"></a>

**Default severity: Medium**

This finding informs you that an IAM entity is making API calls designed to modify the permissions on one or more buckets or objects in your AWS environment\. This action may be performed by an attacker to allow information to be shared outside of the account\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="impact-s3-permissionsmodificationunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Impact:S3/ObjectDelete\.Unusual<a name="impact-s3-objectdeleteunusual"></a>

### An IAM entity invoked an API used to delete data in an S3 bucket\.<a name="impact-s3-objectdeleteunusual_description"></a>

#### <a name="impact-s3-objectdeleteunusual_severity"></a>

**Default severity: Medium**

This finding informs you that a specific IAM entity in your AWS environment is making API calls designed to delete data in the listed S3 bucket by deleting the bucket itself\. This activity is suspicious because the way the IAM entity invoked the API was unusual\. For example, this IAM entity had no prior history of invoking this type of API, or the API was invoked from an unusual location\.

#### <a name="impact-s3-objectdeleteunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## PenTest:S3/KaliLinux<a name="pentest-s3-kalilinux"></a>

### An S3 API was invoked from a Kali Linux machine\.<a name="pentest-s3-kalilinux_description"></a>

#### <a name="pentest-s3-kalilinux_severity"></a>

**Default severity: Medium**

This finding informs you that a machine running Kali Linux is making S3 API calls using credentials that belong to your AWS account\. Your credentials might be compromised\. Kali Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-s3-kalilinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## PenTest:S3/ParrotLinux<a name="pentest-s3-parrotlinux"></a>

### An S3 API was invoked from a Parrot Security Linux machine\.<a name="pentest-s3-parrotlinux_description"></a>

#### <a name="pentest-s3-parrotlinux_severity"></a>

**Default severity: Medium**

This finding informs you that a machine running Parrot Security Linux is making S3 API calls using credentials that belong to your AWS account\. Your credentials might be compromised\. Parrot Security Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-s3-parrotlinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## PenTest:S3/PentooLinux<a name="pentest-s3-pentoolinux"></a>

### An S3 API was invoked from a Pentoo Linux machine<a name="pentest-s3-pentoolinux_description"></a>

#### <a name="pentest-s3-pentoolinux_severity"></a>

**Default severity: Medium**

This finding informs you that a machine running Pentoo Linux is making S3 API calls using credentials that belong to your AWS account\. Your credentials might be compromised\. Pentoo Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-s3-pentoolinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Policy:S3/AccountBlockPublicAccessDisabled<a name="policy-s3-accountblockpublicaccessdisabled"></a>

### An IAM entity invoked an API used to disable S3 block public access on an account\.<a name="policy-s3-accountblockpublicaccessdisabled_description"></a>

#### <a name="policy-s3-accountblockpublicaccessdisabled_severity"></a>

**Default severity: Low**

This finding informs you that Amazon S3 Block Public Access was disabled at the account level\. When S3 Block Public Access settings are enabled, they are used to filter the policies or access control lists \(ACLs\) on buckets as a security measure to prevent inadvertent public exposure of data\. 

Typically, S3 Block Public Access is turned off in an account to allow public access to a bucket or to the objects in the bucket\. When S3 Block Public Access is disabled for an account, access to your buckets is controlled by the policies, ACLs, or bucket\-level Block Public Access settings applied to your individual buckets\. This does not necessarily mean that the buckets are shared publicly, but that you should audit the permissions applied to the buckets to confirm that they provide the appropriate level of access\.

#### <a name="policy-s3-accountblockpublicaccessdisabled_remediation"></a>

**Remediation recommendations:**

## Policy:S3/BucketBlockPublicAccessDisabled<a name="policy-s3-bucketblockpublicaccessdisabled"></a>

### An IAM entity invoked an API used to disable S3 block public access on a bucket\.<a name="policy-s3-bucketblockpublicaccessdisabled_description"></a>

#### <a name="policy-s3-bucketblockpublicaccessdisabled_severity"></a>

**Default severity: Low**

This finding informs you that Amazon S3 Block Public Access was disabled for the listed S3 bucket\. When enabled, S3 Block Public Access settings are used to filter the policies or access control lists \(ACLs\) applied to buckets as a security measure to prevent inadvertent public exposure of data\. 

Typically, S3 Block Public Access is turned off on a bucket to allow public access to the bucket or to the objects within\. When S3 Block Public Access is disabled for a bucket, access to the bucket is controlled by the policies or ACLs applied to it\. This does not mean that the bucket is shared publicly, but you should audit the policies and ACLs applied to the bucket to confirm that appropriate permissions are applied\.

#### <a name="policy-s3-bucketblockpublicaccessdisabled_remediation"></a>

**Remediation recommendations:**

## Policy:S3/BucketAnonymousAccessGranted<a name="policy-s3-bucketanonymousaccessgranted"></a>

### An IAM principal has granted access to an S3 bucket to the internet by changing bucket policies or ACLs\.<a name="policy-s3-bucketanonymousaccessgranted_description"></a>

#### <a name="policy-s3-bucketanonymousaccessgranted_severity"></a>

**Default severity: High**

This finding informs you that the listed S3 bucket has been made publicly accessible on the internet because an IAM entity has changed a bucket policy or ACL on that bucket\. After a policy or ACL change is detected, GuardDuty uses automated reasoning powered by [Zelkova](https://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), to determine if the bucket is publicly accessible\.

**Note**  
If a bucket's ACLs or bucket policies are configured to explicitly deny GuardDuty or to deny all, this finding cannot be generated for that bucket\.

#### <a name="policy-s3-bucketanonymousaccessgranted_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Policy:S3/BucketPublicAccessGranted<a name="policy-s3-bucketpublicaccessgranted"></a>

### An IAM principal has granted public access to an S3 bucket to all AWS users by changing bucket policies or ACLs\.<a name="policy-s3-bucketpublicaccessgranted_description"></a>

#### <a name="policy-s3-bucketpublicaccessgranted_severity"></a>

**Default severity: High**

This finding informs you that the listed S3 bucket has been publicly exposed to all authenticated AWS users because an IAM entity has changed a bucket policy or ACL on that S3 bucket\. After a policy or ACL change is detected, GuardDuty uses automated reasoning powered by [Zelkova](https://aws.amazon.com/blogs/security/protect-sensitive-data-in-the-cloud-with-automated-reasoning-zelkova/), to determine if the bucket is publicly accessible\.

**Note**  
If a bucket's ACLs or bucket policies are configured to explicitly deny GuardDuty or to deny all, this finding cannot be generated for that bucket\.

#### <a name="policy-s3-bucketpublicaccessgranted_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## Stealth:S3/ServerAccessLoggingDisabled<a name="stealth-s3-serveraccessloggingdisabled"></a>

### S3 server access logging was disabled for a bucket\.<a name="stealth-s3-serveraccessloggingdisabled_description"></a>

#### <a name="stealth-s3-serveraccessloggingdisabled_severity"></a>

**Default severity: Low**

This finding informs you that S3 server access logging is disabled for a bucket within your AWS environment\. If disabled, no logs are created for any actions taken on the identified S3 bucket or on the objects in the bucket, unless S3 object level logging is enabled for this bucket\. Disabling logging is a technique used by unauthorized users in order to cover their tracks\. This finding is triggered when Amazon S3 server access logging is disabled for a bucket\. To learn more, see [S3 Server Access Logging](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html)\.

#### <a name="stealth-s3-serveraccessloggingdisabled_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## UnauthorizedAccess:S3/MaliciousIPCaller\.Custom<a name="unauthorizedaccess-s3-maliciousipcallercustom"></a>

### An S3 API was invoked from an IP address on a custom threat list\.<a name="unauthorizedaccess-s3-maliciousipcallercustom_description"></a>

#### <a name="unauthorizedaccess-s3-maliciousipcallercustom_severity"></a>

**Default severity: High**

This finding informs you that an S3 API operation, for example, `PutObject` or `PutObjectAcl`, was invoked from an IP address that is included on a threat list that you uploaded\. The threat list associated with this finding is listed in the **Additional information** section of a finding's details\.

#### <a name="unauthorizedaccess-s3-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.

## UnauthorizedAccess:S3/TorIPCaller<a name="unauthorizedaccess-s3-toripcaller"></a>

### An S3 API was invoked from a Tor exit node IP address\.<a name="unauthorizedaccess-s3-toripcaller_description"></a>

#### <a name="unauthorizedaccess-s3-toripcaller_severity"></a>

**Default severity: High**

This finding informs you that an S3 API operation, such as `PutObject` or `PutObjectAcl`, was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This finding can indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="unauthorizedaccess-s3-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected for the associated principal it may indicate the credentials have been exposed or your S3 permissions are not restrictive enough, see [Remediating a Compromised S3 Bucket](guardduty_remediate.md#compromised-s3)\.