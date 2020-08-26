# Exporting findings<a name="guardduty_exportfindings"></a>

GuardDuty supports exporting active findings to CloudWatch Events and, optionally, to an Amazon S3 bucket\. New Active findings that GuardDuty generates are automatically exported within about 5 minutes after the finding is generated\. You can set the frequency for how often updated Active findings are exported to CloudWatch Events and your S3 bucket \(if configured\)\. The frequency that you select applies to exporting to both CloudWatch Events and your S3 bucket, but only for updated findings\.

When you configure options for exporting findings, the settings apply only to the account in the current AWS Region\. Only findings that are generated in the current account and Region are exported\. If you enable findings export in a GuardDuty master account, all findings from associated member accounts that are generated in the current Region are also exported to the same location that is configured for the master account\. 

Because GuardDuty is enabled per Region, to export findings from all Regions, you need to configure export options for each Region in which you're using GuardDuty\. You can export findings from all Regions into one bucket located in one Region\. You can also choose to export findings to a bucket in a different account\.

**Important**  
Archived findings, including new instances of auto\-archived findings, aren't exported\. If you unarchive a finding, its status is updated to **Active**, and then it's exported\.

To learn more, see [Creating custom responses to GuardDuty findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

## Permissions required to configure findings export<a name="guardduty_exportfindings-permissions"></a>

When you configure options for exporting findings, you select a bucket to store the findings, and a KMS key to use for data encryption\. In addition to permissions to GuardDuty actions, you must also have permissions to the following actions to successfully configure options for exporting findings\.
+ kms:ListAliases
+ s3:CreateBucket
+ s3:GetBucketLocation
+ s3:ListAllMyBuckets
+ s3:PutBucketAcl
+ s3:PutBucketPublicAccessBlock
+ s3:PutBucketPolicy
+ s3:PutObject

## Setting the frequency for exporting updated active findings<a name="guardduty_exportfindings-frequency"></a>

Configure the frequency for exporting updated Active findings as appropriate for your environment\. By default, updated findings are exported every 6 hours\. This means that any findings that are updated after the most recent export are included in the next export\. If updated findings are exported every 6 hours and the export occurs at 12:00, any finding that you update after 12:00 is exported at 18:00\.

**To set the frequency**

1. Sign in to the AWS Management Console and open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

1. In the **Findings export options** section, select **Frequency for updated findings**\. This sets the frequency for exporting updated Active findings to both CloudWatch Events and Amazon S3\. You can choose from the following:
   + **Update CWE and S3 every 15 minutes**
   + **Update CWE and S3 every 1 hour**
   + **Update CWE and S3 every 6 hours \(default\)**

1. Choose **Save**\.

## Configuring findings export to an Amazon S3 bucket<a name="guardduty_exportfindings-s3"></a>

Configure settings for exporting Active findings to an Amazon S3 bucket from the **Settings** page in the GuardDuty console\. When you configure findings export, you can choose an existing S3 bucket, or have GuardDuty create a new bucket to store exported findings\. If you choose to use a new bucket, GuardDuty applies all necessary permissions to the created bucket\. If you use an existing bucket, you must update the bucket policy to allow GuardDuty to put findings into the bucket\.

**Important**  
The bucket and KMS key that you use must be in the same Region\.

### Updating the KMS key policy<a name="guardduty_exprotfindings-key-policy"></a>

GuardDuty encrypts the findings data in the bucket by using an AWS KMS key\. To successfully configure findings export, you must first give GuardDuty permission to use the key that you choose when you configure findings export\. You grant the permissions by [changing the key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html) for the key you use\. 

If you plan to use a new key for GuardDuty findings, [create a key](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) before proceeding\. If the key isn't in your account, you need to log in to the account that owns the key to apply the key policy\. You also need the key ARN for a key from another account when you configure export settings\.

**To modify the key policy to allow GuardDuty to use the key**

1. Determine which key you want to use, either an existing or a new customer master key \(CMK\)\. The key must be in the same Region as the bucket\.

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose the key that you plan to use for encrypting exported findings\.

1. Choose **Key policy**, and then choose **Edit**\.
**Note**  
If **Switch to policy view** is displayed, choose that to display the key policy, and then choose **Edit**\.

1. Add the following policy statement to the policy\. The statement allows GuardDuty to use only the key that you changed the policy for\. When editing the key policy make sure your JSON syntax is valid, if you add the statement before the final statement you must add a comma after the closing bracket\.

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
If you're using GuardDuty in an manually\-enabled Region, replace the value for the "Service" with the service endpoint for the Region\. For example, if you're using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"Service": "guardduty.me-south-1.amazonaws.com"`\.

1. Choose **Save**\.

### Exporting findings to a new bucket<a name="guardduty_exportfindings-new-bucket"></a>

When you choose to create a new bucket to configure findings export, GuardDuty adds a bucket policy to the bucket that grants GuardDuty permission to put findings into the bucket\.

**To configure findings export using a new bucket**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

1. Choose **New bucket** to create a new bucket to store exported findings\.

   In the **Name the bucket** field, enter a name for the bucket\. The name must be unique across all S3 buckets\. Bucket names must start with a lowercase letter or a number\.

1. Optional\. Under **Log file prefix**, enter the path prefix to use in the path to the location in the bucket where findings are stored\. When you enter a value, the example path below the field is updated to reflect the path to exported findings in the bucket\.

1. Under **KMS encryption**, do one of the following:
   + Select **Choose key from your account**\.

     Then choose the key alias of the key that you changed the policy for from the **Key alias** list\.
   + Select **Choose key from another account**\.

     Then enter the full ARN to the key that you changed the policy for\.

     The key that you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/viewing-keys.html#find-cmk-id-arn)\.

1. Choose **Save**\.

### Exporting findings to an existing bucket<a name="guardduty_exportfindings-existing-bucket"></a>

When you create a new bucket to export findings to, GuardDuty modifies the bucket policy to grant GuardDuty the necessary permissions to put findings in the bucket\. If you choose to use an existing bucket, you must update the bucket policy to grant GuardDuty those permissions to successfully configure findings export settings\. To learn more, see [How do I add an S3 Bucket policy?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/add-bucket-policy.html)\.

#### Granting GuardDuty permissions to export findings to your bucket<a name="guardduty_exportfindings-s3-policies"></a>

**To add a bucket policy**

Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket you plan to use for exported findings\.

1. Choose **Permissions**, and then choose **Bucket Policy**\.

1. Copy the example policy and paste it into the **Bucket policy editor**\.

1. Replace the placeholder values in the example policy with the values appropriate for your environment\.

   Replace *myBucketName* with the name of the bucket that you're adding the bucket policy for\. Replace *region* with the Region that the KMS key is in\. Replace *111122223333* with your AWS account number, and replace *KMSKeyId* with the key ID of the key that you chose for encryption\.

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
If you're using GuardDuty in an manually\-enabled Region, replace the value for the service with the service endpoint for the Region\. For example, if you're using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"guardduty.me-south-1.amazonaws.com"`\.

**To configure findings export using an existing bucket**

1. Identify the bucket that you plan to export findings to\.

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

1. Under **S3 bucket**, choose **Configure now**\.

1. Do one of the following:
   + Choose **Existing bucket in your account** to choose a bucket in your account\.

     Under **Choose a bucket**, choose the bucket from your account to use to store exported findings\.
   + Choose **Existing bucket in another account**\.

     In the **Bucket ARN field**, enter the ARN for the bucket from another account to use\. The ARN can be for any bucket, including buckets in the current account\.

1. Optional\. Under **Log file prefix**, enter the path prefix to use in the path to the location in the bucket where findings are stored\. When you enter a value, the example path below the field is updated to reflect the path to exported findings in the bucket\.

1. Under **KMS encryption**, do one of the following:
   + Select **Choose key from your account**\.

     Then choose the key alias of the key that you changed the policy for from the **Key alias** list\.
   + Select **Choose key from another account**\.

     Then enter the full ARN to the key that you changed the policy for\.

     The key you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/viewing-keys.html#find-cmk-id-arn)\.

1. Choose **Save**\.

## Export access error<a name="access-error"></a>

After you configure finding export options, if GuardDuty is unable to export findings, an error message is displayed on the **Settings** page\. This can happen when GuardDuty can no longer access the target resource, such as when the S3 bucket is deleted or the permissions to the bucket are changed\. This can also happen when the KMS key used to encrypt data in the bucket becomes inaccessible\. 

When exporting fails, GuardDuty sends a notification to the email associated with the account to let you know about the issue\. If you don't resolve the issue, GuardDuty disables finding export in the account\. You can update the configuration to restart finding export at any time\.

If you receive this error, review the information in this topic about how to enable and configure findings export\. For example, review the key policy and confirm that the correct policy is applied to the KMS key that you chose for encryption\.