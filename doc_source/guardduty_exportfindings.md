# Export Findings<a name="guardduty_exportfindings"></a>

GuardDuty supports exporting Active findings to CloudWatch Events and, optionally, to an Amazon S3 bucket\. New Active findings that GuardDuty generates are automatically exported within about 5 minutes after the finding is generated\. You can set the frequency for how often updated Active findings are exported to CloudWatch Events and your S3 bucket, if configured\. The frequency you select applies to exporting to both CloudWatch Events and S3, but only for updated findings\.

When you configure findings export options, the settings apply only to the account in the current region\. Only findings that are generated in the current account and region are exported\. If you enable findings export in a GuardDuty master account, all findings from associated member accounts that are generated in the current region are also exported to the same location that is configured for the master account\. Because GuardDuty is enabled per region, to export findings from all regions you need to configure export options for each region in which you are using GuardDuty\. You can export findings from all regions into one bucket located in one region\. You can choose to export findings to a bucket in a different account\.

**Important**  
Archived findings, including new instances of auto\-archived findings, are not exported\. If you unarchive a finding, its status is updated to Active and it is then exported\.

To learn more, see [Monitoring GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

## Permissions Required to Configure Findings Export<a name="guardduty_exportfindings-permissions"></a>

When you configure findings export options, you select a bucket to store the findings, and a KMS key to use for data encryption\. In addition to permissions to GuardDuty actions, you must also have permissions to the following actions successfully configure options for exporting findings\.
+ kms:ListAliases
+ s3:CreateBucket
+ s3:GetBucketLocation
+ s3:ListAllMyBuckets
+ s3:PutBucketAcl
+ s3:PutBucketPublicAccessBlock
+ s3:PutBucketPolicy
+ s3:PutObject

## Set the Frequency for Exporting Updated Active Findings<a name="guardduty_exportfindings-frequency"></a>

Configure the frequency for exporting updated Active findings as appropriate for your environment\. By default, updated findings are exported every 6 hours\. This means that any findings that are updated after the most recent export are included in the next export\. If updated findings are exported every 6 hours, and the export occurs at 12:00, any finding that you update after 12:00 is exported at 18:00\.

1. Sign in to the AWS Management Console and open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

1. In the **Findings export options** section, select the **Frequency for updated findings**\. This sets the frequency for exporting updated Active findings to both CloudWatch Events and Amazon S3\. You can choose from the following:
   + **Update CWE and S3 every 15 minutes**
   + **Update CWE and S3 every 1 hour**
   + **Update CWE and S3 every 6 hours \(default\)**

1. Choose **Save**\.

## Configure Findings Export to an Amazon S3 Bucket<a name="guardduty_exportfindings-s3"></a>

Configure settings for exporting Active findings to an Amazon S3 bucket from the **Settings** page in the GuardDuty console\. When you configure findings export, you can choose an existing S3 bucket, or have GuardDuty create a new bucket to store exported findings\. If you choose to use a new bucket, GuardDuty applies all necessary permissions to the created bucket\. If you use an existing bucket, you must update the bucket policy to allow GuardDuty to put findings into the bucket\.

**Important**  
The bucket and KMS key you use must be in the same Region\.

### Changing the key policy<a name="guardduty_exprotfindings-key-policy"></a>

GuardDuty encrypts the findings data in the bucket using a AWS KMS key\. To successfully configure findings export, you must first give GuardDuty permission to use the key you choose when you configure findings export\. The permissions are granted by [changing the key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html) for the key you use\. If you plan to use a new key for GuardDuty findings, [create a key](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) before proceeding\. If the key is not in your account, you need to log in to the account that owns the key to apply the key policy\. You also need the key ARN for a key from another account when you configure export settings\.

**To modify the key policy to allow GuardDuty to use the key**

1. Determine which key you want to use, either an existing or a new customer managed key \(CMK\)\. The key must be in the same Region as the bucket\.

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose the key you plan to use for encrypting exported findings\.

1. Choose **Key policy**, then choose **Edit**\.
**Note**  
If **Switch to policy view** is displayed, choose that to display the key policy, then choose **Edit**\.

1. Add the following policy statement to the policy\. The statement allows GuardDuty to use only the key you change the policy for\.

   ```
   {
       "Sid": "Allow GuardDuty to use the key",
       "Effect": "Allow",
       "Principal": {
           "Service": "guardduty.amazonaws.com"
               },
               "Action": "kms:GenerateDataKey",
               "Resource": "*"
   }
   ```
**Note**  
If you are using GuardDuty in an opt\-in Region, replace the value for the "Service" with the service endpoint for the Region\. For example, if you are using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"Service": "guardduty.me-south-1.amazonaws.com"`\.

1. Choose **Save**\.

When you add the statement to the policy, make sure that the syntax is valid\. Policies are displayed in JavaScript Object Notation \(JSON\) format\. When you add a new section to the policy, you need to include a comma either before or after the added section\. The position of the comma depends on how you add the new statement\. If you add the statement as the last statement in the policy, add a comma after the closing bracket for the preceding section\. If you add it as the first statement, or add it between two existing statements, add a comma after the closing bracket\. The following examples show how to add the policy statement to a default key policy\.

The following example shows a default key policy with no additional permissions granted:

```
{
    "Id": "key-consolepolicy",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::111122223333:root"
            },
            "Action": "kms:*",
            "Resource": "*"
        }
    ]
}
```

The following example shows how to add the policy statement as the first statement:

```
{
    "Id": "key-consolepolicy",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Allow GuardDuty to use the key",
            "Effect": "Allow",
            "Principal": {"Service": "guardduty.amazonaws.com"},
            "Action": "kms:GenerateDataKey",
            "Resource": "*"
        },<--Add a comma after this bracket
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {"AWS": "arn:aws:iam::111122223333:root"},
            "Action": "kms:*",
            "Resource": "*"
        }
    ]
}
```

The following example shows how to add the policy statement as the last statement:

```
{
    "Id": "key-consolepolicy",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {"AWS": "arn:aws:iam::111122223333:root"},
            "Action": "kms:*",
            "Resource": "*"
        }, <--Add a comma after this bracket
        {
            "Sid": "Allow GuardDuty to use the key",
            "Effect": "Allow",
            "Principal": {"Service": "guardduty.amazonaws.com"},
            "Action": "kms:GenerateDataKey",
            "Resource": "*"
        }
    ]
}
```

### Export Findings to a New Bucket<a name="guardduty_exportfindings-new-bucket"></a>

When you choose to create a new bucket to configure findings export, GuardDuty adds a bucket policy to the bucket that grants GuardDuty permission to put findings into the bucket\.

**Configure findings export using a new bucket**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

1. Choose **New bucket** to create a new bucket to store exported findings\.

   In the **Name the bucket** field, enter a name for the bucket\. The name must be unique across all buckets in S3\. Bucket names must start with a lowercase letter or a number\.

1. Optional\. Under **Log file prefix**, enter the path prefix to use in the path to the location in the bucket where findings are stored\. When you enter a value, the example path below the field is updated to reflect the path to exported findings in the bucket\.

1. Under **KMS encryption**, do one of the following:
   + Select **Choose key from your account**\.

     Then select key alias of the key that you changed the policy for from the **Key alias** list\.
   + Select **Choose key from another account**\.

     Then enter the full ARN to the key that you changed the policy for\.

     The key you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the Key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/viewing-keys.html#find-cmk-id-arn)\.

1. Choose **Save**\.

### Export Findings to an Existing Bucket<a name="guardduty_exportfindings-existing-bucket"></a>

When you create a new bucket to export findings to, GuardDuty modifies the bucket policy to grant GuardDuty the necessary permissions to put findings in the bucket\. If you choose to an existing bucket, you must update the bucket policy to grant GuardDuty those permissions to successfully configure findings export settings\. To learn more, see [How Do I Add an S3 Bucket Policy?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/add-bucket-policy.html)

#### Granting GuardDuty Permissions to Export Findings to Your Bucket<a name="guardduty_exportfindings-s3-policies"></a>

**To add a bucket policy**

Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket you plan to use for exported findings\.

1. Choose **Permissions**, then choose **Bucket Policy**\.

1. Copy the example policy and paste it into the **Bucket policy editor**\.

1. Replace the placeholder values in the example policy with the values appropriate for your environment\.

   Replace *myBucketName* with the name of the bucket you are adding the bucket policy for\. Replace *region* with the Region the KMS key is in\. Replace *111122223333* with your AWS account number, and replace *KMSKeyId* with the key ID of the key you chose for encryption\.

The following example policy shows how to grant GuardDuty permission to send findings to your Amazon S3 bucket\. If you change the path after you configure findings export, you must modify the policy to grant permission to the new location\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Allow GuardDuty to use the getBucketLocation operation",
            "Effect": "Allow",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:GetBucketLocation",
            "Resource": "arn:aws:s3:::myBucketName"
        },
        {
            "Sid": "Allow GuardDuty to upload objects to the bucket",
            "Effect": "Allow",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::myBucketName/[optional prefix]/*"
        },
        {
            "Sid": "Deny unencrypted object uploads. This is optional",
            "Effect": "Deny",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::myBucketName/[optional prefix]/*",
            "Condition": {
                "StringNotEquals": {
                    "s3:x-amz-server-side-encryption": "aws:kms"
                }
            }
        },
        {
            "Sid": "Deny incorrect encryption header. This is optional",
            "Effect": "Deny",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::myBucketName/[optional prefix]/*",
            "Condition": {
                "StringNotEquals": {
                    "s3:x-amz-server-side-encryption-aws-kms-key-id": "arn:aws:kms:region:111122223333:key/KMSKeyId"
                }
            }
        },
        {
            "Sid": "Deny non-HTTPS access",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::myBucketName/*",
            "Condition": {
                "Bool": {
                    "aws:SecureTransport": "false"
                }
            }
        }
    ]
}
```

**Note**  
If you are using GuardDuty in an opt\-in Region, replace the value for the service with the service endpoint for the Region\. For example, if you are using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"guardduty.me-south-1.amazonaws.com"`\.

**Configure findings export using an existing bucket**

1. Identify the bucket you plan to export findings to\.

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

1. Under **S3 bucket**, choose **Configure now**\.

1. Do one of the following:
   + Choose **Existing bucket in your account** to select a bucket in your account\.

     Under **Choose a bucket**, select the bucket from your account to use to store exported findings\.
   + Choose **Existing bucket in another account**

     In the **Bucket ARN field**, enter the ARN for the bucket from another account to use\. The ARN can be for any bucket, including buckets in the current account\.

1. Optional\. Under **Log file prefix**, enter the path prefix to use in the path to the location in the bucket where findings are stored\. When you enter a value, the example path below the field is updated to reflect the path to exported findings in the bucket\.

1. Under **KMS encryption**, do one of the following:
   + Select **Choose key from your account**\.

     Then select key alias of the key that you changed the policy for from the **Key alias** list\.
   + Select **Choose key from another account**\.

     Then enter the full ARN to the key that you changed the policy for\.

     The key you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the Key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/viewing-keys.html#find-cmk-id-arn)\.

1. Choose **Save**\.

## Export Access Error<a name="access-error"></a>

After you configure finding export options, if GuardDuty is unable to export findings an error message is displayed on the **Settings** page\. This can happen when GuardDuty can no longer access the target resource, such as when the S3 bucket is deleted or the permissions to the bucket are changed\. This can also happen when the KMS key used to encrypt data in the bucket becomes inaccessible\. When exporting fails, GuardDuty sends a notification to the email associated with the account to let you know about the issue\. If you do not resolve the issue, GuardDuty disables finding export in the account\. You can update the configuration to restart finding export at any time\.

If you receive this error, review the information in this topic about how to enable and configure findings export\. For example, review the key policy and confirm that the correct policy is applied to the KMS key that you chose for encryption\.