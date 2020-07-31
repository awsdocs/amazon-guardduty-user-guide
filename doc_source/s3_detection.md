# Amazon S3 protection in Amazon GuardDuty<a name="s3_detection"></a>

The S3 protection feature enables GuardDuty to use S3 data event monitoring to identify potential security risks for data within your S3 buckets\.

 Amazon GuardDuty monitors threats against your Amazon S3 resources by analyzing AWS CloudTrail management events and CloudTrail S3 data events\. These data sources monitor different kinds of activity, for example, S3 related CloudTrail management events include operations that list or configure S3 buckets, such as `ListBuckets`, `DeleteBuckets`, and `PutBucketReplication`\. Examples of S3 data events include object\-level API operations, such as `GetObject`, `ListObjects`, `DeleteObject`, and `PutObject`\. 

GuardDuty monitoring of CloudTrail management events is on by default for all accounts that have enabled GuardDuty and is not configurable\. S3 data event logs are a configurable data source in GuardDuty\. The processes for enabling or disabling S3 data event monitoring is covered in this topic\.

We strongly recommend that you enable S3 protection in GuardDuty, as this data source allows GuardDuty to monitor, and generate findings for, suspicious access to data stored in your S3 buckets\. 

## Understanding how GuardDuty uses S3 data events<a name="s3-data-source"></a>

The S3 protection feature in GuardDuty refers to whether S3 data events are enabled as a data source for GuardDuty\. When S3 data event monitoring is enabled GuardDuty immediately begins to analyze S3 data events from all of your S3 buckets and monitor them for malicious and suspicious activity\. For more information, see [How Amazon GuardDuty uses its data sources](guardduty_data-sources.md)\. 

GuardDuty does not process requests to objects that you have made publicly accessible, but it does alert you when a bucket is made publicly accessible\. When GuardDuty detects a threat based on S3 data event monitoring, it generates a security finding\. For information about the types of findings GuardDuty can generate for Amazon S3 see [GuardDuty S3 finding types](guardduty_finding-types-s3.md)\. 

If you disable S3 protection, GuardDuty immediately stops consuming this data source and stops monitoring access to data stored in your S3 buckets\.

## Configuring S3 protection for an individual account<a name="data-source-configure"></a>

**Important**  
By default, S3 protection is enabled automatically for new detectors\.

If you are a GuardDuty master enabling GuardDuty for the first time on a new account, and you do not want S3 protection turned on, you can disable it through the [createDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) API\.

Accounts that were using GuardDuty before the addition of S3 protection can enable the new data source by configuring GuardDuty through the console or the `UpdateDetector` API operation\.

To configure Amazon S3 data events as a data source for your account, see the following configuration options\.

### To enable or disable S3 protection \(Console\)<a name="data-source-disable_console"></a>

1. Log into the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console\.

1. In the navigation pane, under **Settings**, choose **S3 Protection**\.

1. The **S3 Protection** pane lists the current status of S3 protection for your account\. You may enable or disable it at any time by selecting **Enable** or **Disable** respectively, then confirming your selection\.

### To enable or disable S3 protection \(API\)<a name="data-source-disable_api"></a>
+ Run the [updateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateDetector.html) API operation using your own regional detector ID and passing the `dataSources` object with `"S3 Logs":"enable"` set to true or false, respectively\.

  You can also enable or disable S3 protection using AWS command line tools by running the following AWS CLI command\. Make sure to use your own valid detector ID\. 
**Note**  
The following example code enables S3 protection\. To disable it, replace `true` with `false`\.

  ```
  aws guardduty update-detector --detector-id 12abc34d567e8fa901bc2d34e56789f0 --data-sources '{"S3Logs":{"Enable":true}}'
  ```

#### Disable S3 protection when enabling GuardDuty for new accounts \(API\)<a name="s3-disable-member_api"></a>

If you want to enable GuardDuty in a new account but do not want S3 protection to be enabled by default, you can modify the [createDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) API operation with the optional `dataSources` object\. The following example uses the AWS CLI to enable a new GuardDuty detector with the S3 protection disabled\.

```
aws guardduty create-detector --enable --data-sources '{"S3Logs":{"Enable":false}}'
```

For accounts associated by AWS Organizations, this process can be automated through console settings as described in the next section\.

## Configuring S3 protection in multiple\-account environments<a name="s3-multiaccount"></a>

In a multi\-account environment, only GuardDuty master accounts can configure S3 protection\. GuardDuty master accounts can enable or disable S3 protection for their member accounts\. GuardDuty member accounts cannot enable or disable this data source\. 

GuardDuty master accounts that manage their member accounts with AWS Organizations support can choose to have S3 protection automatically enabled on all new accounts in the organization\. For more information, see [Managing GuardDuty accounts with AWS Organizations](guardduty_organizations.md)\.

### Automatically enabling S3 protection for Organization member accounts<a name="s3-autoenable"></a>

**Note**  
This functionality is only available to masters of GuardDuty members incorporated through AWS Organizations\.

1. Log in to the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console using the administrator account\.

1. In the navigation pane, under **Settings**, choose **Accounts**\.

1.  Ensure **Auto\-enable** for GuardDuty is turned is turned on\. If it is off you can enable by selecting **Enable** from the banner or by selecting **Auto\-enable is OFF**\. This feature will automatically enable GuardDuty for new member accounts within your organization and must be enabled in order to auto\-enable S3 protection\.

1. Once Auto\-enable for GuardDuty is on, you can enable S3 protection for your new members in addition to enabling GuardDuty by selecting the **S3 Protection** toggle icon\. Choose **Update Settings** to confirm\.

### Enable or disable S3 protection for member accounts \(Console\)<a name="s3-disable-member_console"></a>

### To enable S3 protection for all accounts

1. Log into the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console\.

1. If you want to enable S3 protection for all accounts at once, choose **S3 Protection** from the navigation pane\.

1. Your will see a statement reflecting the number of accounts you manage that have S3 protection enabled\. Choose **Enable all** to enable S3 protection for all accounts\.
**Note**  
If you manage accounts within an organization this action also enables the **Auto\-enable** feature to automatically enable S3 protection for future member accounts within your organization\.

### To selectively enable or disable S3 protection in member accounts

1. Log into the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console\.

1. In the navigation pane, under **Settings**, choose **Accounts**\.
**Note**  
From the Accounts table, review the **S3 Protection** column\. A green check mark icon indicates that S3 protection is enabled, and a blue dash icon indicates that it is disabled\. If this column is blank, the account is not eligible for S3 protection\. You can also filter by **ENABLED** or **DISABLED**\.

1. Select the account for which you want to configure S3 protection\. From the **Actions** menu choose **Enable S3 Protection** or **Disable S3 Protection**, then confirm your selection to change the settings for the selected account\. The table will update automatically to show your changes\.

#### Enable or disable S3 protection for member accounts \(API\)<a name="s3-disable-member_api"></a>

To selectively enable or disable S3 protection for your member accounts, run the [updateMemberDetectors](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateMemberDetector.html) API operation using your own detector ID\. The following example shows how you can enable S3 protection for a single member account\. To disable it, replace `true` with `false`\. 

```
aws guardduty update-member-detectors --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-ids 123456789012 --data-sources '{"S3Logs":{"Enable":true}}'
```

**Note**  
You can also pass a list of account IDs separated by a space\.

When the code has successfully executed, it returns an empty list of `UnprocessedAccounts`\. If there were any problems changing the detector settings for an account, that account ID is listed along with a summary of the issue\.

**Note**  
If you use scripts to on\-board new accounts and wish to disable S3 protection in your enw accounts you can modify the [createDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) API operation with the optional `dataSources` object as describe in this topic\.