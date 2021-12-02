# Exporting findings<a name="guardduty_exportfindings"></a>

GuardDuty supports exporting active findings to CloudWatch Events and, optionally, to an Amazon S3 bucket\. New Active findings that GuardDuty generates are automatically exported within about 5 minutes after the finding is generated\. You can set the frequency for how often updates to Active findings are exported to CloudWatch Events\. The frequency that you select applies to the exporting of new occurences of existing findings to CloudWatch Events, your S3 bucket \(if configured\), and Detective \(if integrated\)\. For more information on updates to existing findings see [GuardDuty finding aggregation ](guardduty_findings.md#finding-aggregation)

**Note the following about export settings for findings:**
+ Export settings are regional, which means you need to configure export options for each Region in which you're using GuardDuty\. However, you can use the same bucket in a single Region as the export destination for each Region you use GuardDuty in\.
+ Archived findings, including new instances of suppressed findings, aren't exported\. If you unarchive a finding, its status is updated to **Active**, and it will be exported at the next interval\.
+ If you enable findings export in a GuardDuty administrator account all findings from associated member accounts that are generated in the current Region are also exported to the same location that you configured for the administrator account\.

To configure settings for exporting Active findings to an Amazon S3 bucket you will need a KMS key that GuardDuty can use to encrypt findings, and an S3 bucket with permissions that allows GuardDuty to upload objects\. Review this topic to learn how to configure findings export and frequency\. 

## Permissions required to configure findings export<a name="guardduty_exportfindings-permissions"></a>

When you configure options for exporting findings, you select a bucket to store the findings in and a KMS key to use for data encryption\. In addition to permissions to GuardDuty actions, you must also have permissions to the following actions to successfully configure options for exporting findings\.
+ kms:ListAliases
+ s3:CreateBucket
+ s3:GetBucketLocation
+ s3:ListAllMyBuckets
+ s3:PutBucketAcl
+ s3:PutBucketPublicAccessBlock
+ s3:PutBucketPolicy
+ s3:PutObject

**Important**  
If your policy explicitly denies `putObjectAcl` you will be unable to publish findings\.

## Granting GuardDuty permission to a KMS key<a name="guardduty_exportfindings-key-policy"></a>

GuardDuty encrypts the findings data in your bucket by using an AWS KMS key\. To successfully configure findings export, you must first give GuardDuty permission to use a KMS key\. You grant the permissions by [changing the key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html) for the key you use\. 

If you plan to use a new key for GuardDuty findings, [create a key](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) before proceeding\. If you are using a key in another account, you need to log in to the account that owns the key to apply the key policy\. You also need the key ARN for a key from another account when you configure export settings\.

**To modify the key policy to allow GuardDuty to use the key**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Create a new key or choose an existing key that you plan to use for encrypting exported findings\. The key must be in the same Region as the bucket, however, you can use this same bucket and key pair for each region you want to export findings from\.

1. Select your key then copy the key ARN from the **General configuration** panel\.

1. Under **Key policy**, choose **Edit**\.
**Tip**  
If **Switch to policy view** is displayed, choose that to display the key policy, and then choose **Edit**\.

1. Add the following key policy granting GuardDuty access to your key\. Replace the values in red to match your environment\.

   Replace *Region* with the Region that the KMS key is in\. Replace *111122223333* with the AWS account number of the source account that owns the GuardDuty detector\. Replace *KMSKeyId* with the key ID of the key that you chose for encryption and replace *SourceDetectorID* with the source account's GuardDuty detector ID for the current Region\.

    This statement allows GuardDuty to use only the key that you changed the policy for\. When editing the key policy make sure your JSON syntax is valid, if you add the statement before the final statement you must add a comma after the closing bracket\.

   ```
   {    
       "Sid": "AllowGuardDutyKey",
       "Effect": "Allow",
       "Principal": {
           "Service": "guardduty.amazonaws.com"
       },
       "Action": "kms:GenerateDataKey",
       "Resource": "arn:aws:kms:Region:111122223333:key/KMSKeyId",
       "Condition": {
           "StringEquals": {
               "aws:SourceAccount": "111122223333",
               "aws:SourceArn": "arn:aws:guardduty:Region:111122223333:detector/SourceDetectorID"	
           }
       }
   }
   ```
**Note**  
If you're using GuardDuty in an manually\-enabled Region, replace the value for the "Service" with the Regional endpoint for that Region\. For example, if you're using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"Service": "guardduty.me-south-1.amazonaws.com"`\.

1. Choose **Save**\.

1. \(Optional\) If you plan on using an existing bucket, copy the key ARN to a notepad for use in later steps\. To locate the key ARN, see [Finding the key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/viewing-keys.html#find-cmk-id-arn)\.

## Granting GuardDuty permissions to a bucket<a name="guardduty_exportfindings-s3-policies"></a>

When using a pre\-existing bucket withing your account, or in a different AWS account, you must grant GuardDuty permission to upload objects to that bucket\. You grant these permissions by [adding an S3 bucket policy](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/add-bucket-policy)\. If you are using a pre\-existing bucket, expand the following section for step\-by\-step instructions on adding a bucket policy\.

### To add a bucket policy that allows GuardDuty to upload objects your bucket<a name="bucket-policy"></a>

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket you plan to use for exported findings\.

1. Choose **Permissions**, and then choose **Bucket Policy**\.

1. Copy the **example policy** and paste it into the **Bucket policy editor**\.

1. Replace the placeholder values in the example policy with the values appropriate for your environment\.

   Replace *myBucketName* \. Replace *\[optional prefix\]* with a folder location for your exported findings \(GuardDuty will create this location during set up if it does not already exist\)\. Replace *Region* with the Region that the KMS key is in\. Replace *111122223333* with the AWS account number of the account that owns the bucket\. Replace *KMSKeyId* with the key ID of the key that you chose for encryption and replace *SourceDetectorID* with the source account's GuardDuty detector ID for the current Region\.

**Example policy**

The following example policy shows how to grant GuardDuty permission to send findings to your Amazon S3 bucket\. If you change the path after you configure findings export, you must modify the policy to grant permission to the new location\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowGuardDutygetBucketLocation",
            "Effect": "Allow",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:GetBucketLocation",
            "Resource": "arn:aws:s3:::myBucketName",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "111122223333",
                    "aws:SourceArn": "arn:aws:guardduty:Region:111122223333:detector/SourceDetectorID"	

                }
            }
        },
        {
            "Sid": "AllowGuardDutyPutObject",
            "Effect": "Allow",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::myBucketName/[optional prefix]/*",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "111122223333",
                    "aws:SourceArn": "arn:aws:guardduty:Region:111122223333:detector/SourceDetectorID"	

                }
            }
        },
        {
            "Sid": "DenyUnencryptedUploadsThis is optional",
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
            "Sid": "DenyIncorrectHeaderThis is optional",
            "Effect": "Deny",
            "Principal": {
                "Service": "guardduty.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::myBucketName/[optional prefix]/*",
            "Condition": {
                "StringNotEquals": {
                    "s3:x-amz-server-side-encryption-aws-kms-key-id": "arn:aws:kms:Region:111122223333:key/KMSKeyId"
                }
            }
        },
        {
            "Sid": "DenyNon-HTTPS",
            "Effect": "Deny",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::myBucketName/[optional prefix]/*",
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
If you're using GuardDuty in an manually\-enabled Region, replace the value for the service with the Regional endpoint for the Region\. For example, if you're using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"guardduty.me-south-1.amazonaws.com"`\.

## Exporting findings to a bucket with the Console<a name="guardduty_exportfindings-new-bucket"></a>

When you configure findings export, you can choose an existing S3 bucket or have GuardDuty create a new bucket to store exported findings in\. If you choose to use a new bucket, GuardDuty applies all necessary permissions to the created bucket\. If you use an existing bucket, you must first update the bucket policy to allow GuardDuty to put findings into the bucket\.

You may also export findings to an existing bucket in another account\.

When choosing a new or existing bucket in your account, you can add a prefix\. When configuring findings export GuardDuty creates a new folder in the S3 bucket for your findings\. The prefix will prepend the default folder structure created by GuardDuty, which is `/AWSLogs/111122223333/GuardDuty/Region`\.

**Important**  
The KMS key and S3 bucket must be in the same Region\.

Before completing these steps makes sure you have configured a KMS key and, if using an existing bucket, added a bucket policy to allow GuardDuty to create objects\.

------
#### [ New bucket in your account ]

**To configure findings export using a new bucket**

1. Add a policy to the KMS key GuardDuty will use to encrypt findings\. For an example policy see [Granting GuardDuty permission to a KMS key ](#guardduty_exportfindings-key-policy)

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

   1. Choose **New bucket** to create a new bucket to store exported findings\.

      In the **Name the bucket** field, enter a name for the bucket\. The name must be unique across all S3 buckets\. Bucket names must start with a lowercase letter or a number\.

   1. If you used an `[optional prefix]` in your bucket policy you must enter that prefix under **Log file prefix**, otherwise this is optional\. When you enter a value, the example path below the field is updated to reflect the path to bucket location where your exported findings will be stored\.

   1. Under **KMS encryption**, do one of the following:
      + Select **Choose key from your account**\.

        Then choose the key alias of the key that you changed the policy for from the **Key alias** list\.
      + Select **Choose key from another account**\.

        Then enter the full ARN to the key that you changed the policy for\.

        The key that you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/find-cmk-id-arn.html)\.

   1. Choose **Save**\.

------
#### [ Existing bucket in your account ]

**To configure findings export using an existing bucket**

1. Add a policy to the KMS key GuardDuty will use to encrypt findings\. For an example policy see [Granting GuardDuty permission to a KMS key ](#guardduty_exportfindings-key-policy)

1. Attach a policy granting GuardDuty permission to upload objects to your S3 bucket\. For an example policy see [Granting GuardDuty permissions to a bucket](#guardduty_exportfindings-s3-policies)

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

   1. Choose **Existing bucket in your account**\.

      In the **Name the bucket** field enter the name of your bucket\.

   1. Optional\. Under **Log file prefix**, enter a path prefix to use\. GuardDuty will create a new folder in the bucket with specified prefix name\. When you enter a value, the example path below the field is updated to reflect the path to exported findings in the bucket\.

   1. Under **KMS encryption**, do one of the following:
      + Select **Choose key from your account**\.

        Then choose the key alias of the key that you changed the policy for from the **Key alias** list\.
      + Select **Choose key from another account**\.

        Then enter the full ARN to the key that you changed the policy for\.

        The key that you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/viewing-keys.html#find-cmk-id-arn)\.

   1. Choose **Save**\.

------
#### [ Existing bucket in another account ]

**To configure findings export using an existing bucket in another account**

1. Add a policy to the KMS key GuardDuty will use to encrypt findings\. For an example policy see [Granting GuardDuty permission to a KMS key ](#guardduty_exportfindings-key-policy)

1. Attach a policy granting GuardDuty permission to upload objects to the S3 bucket in another account\. For an example policy see [Granting GuardDuty permissions to a bucket](#guardduty_exportfindings-s3-policies)\.
**Note**  
Use the account ID of the account that owns the bucket in the policy

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Choose **Settings**\.

   1. Choose **Existing bucket in another account**\.

   1. In the **Bucket ARN field**, enter the ARN for the bucket from another account to use\.

   1. Under **KMS encryption** enter the full ARN of the key that you changed the policy for\.

      The key you choose must be in the same Region as the bucket\. To learn how to find the key ARN, see [Finding the key ID and ARN](https://docs.aws.amazon.com/kms/latest/developerguide/find-cmk-id-arn.html)\.

   1. Choose **Save**\.

------

## Export access error<a name="access-error"></a>

After you configure finding export options, if GuardDuty is unable to export findings, an error message is displayed on the **Settings** page\. This can happen when GuardDuty can no longer access the target resource, such as when the S3 bucket is deleted or the permissions to the bucket are changed\. This can also happen when the KMS key used to encrypt data in the bucket becomes inaccessible\. 

When exporting fails, GuardDuty sends a notification to the email associated with the account to let you know about the issue\. If you don't resolve the issue, GuardDuty disables finding export in the account\. You can update the configuration to restart finding export at any time\.

If you receive this error, review the information in this topic about how to enable and configure findings export\. For example, review the key policy and confirm that the correct policy is applied to the KMS key that you chose for encryption\.

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