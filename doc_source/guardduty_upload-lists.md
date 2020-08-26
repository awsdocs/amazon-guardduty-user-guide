# Working with trusted IP lists and threat lists<a name="guardduty_upload-lists"></a>

Amazon GuardDuty monitors the security of your AWS environment by analyzing and processing VPC Flow Logs, AWS CloudTrail event logs, and DNS logs\. You can customize this monitoring scope by configuring GuardDuty to also use your own *trusted IP lists* and *threat lists*\. The IP lists described below will apply to all VPC Flow Log and CloudTrail findings, but do not apply to DNS findings

Trusted IP lists consist of IP addresses that you have trusted for secure communication with your AWS infrastructure and applications\. GuardDuty does not generate VPC Flow Log or CloudTrail findings for IP addresses on trusted IP lists\. At any given time, you can have only one uploaded trusted IP list per AWS account per Region\.

Threat lists consist of known malicious IP addresses\. GuardDuty generates findings based on threat lists\. At any given time, you can have up to six uploaded threat lists per AWS account per Region\.

Users from master GuardDuty accounts can upload and manage trusted IP lists and threat lists\. Users from member GuardDuty accounts CANNOT upload and manage lists\. Trusted IP lists and threat lists that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty generates findings based on activity that involves known malicious IP addresses from the master's threat lists and does not generate findings based on activity that involves IP addresses from the master's trusted IP lists\. For more information, see [Managing multiple accounts in Amazon GuardDuty](guardduty_accounts.md)\.

**Important**  
GuardDuty uses the same [`AWSServiceRoleForAmazonGuardDuty` service\-linked role](guardduty_managing_access.md#guardduty_service-access) that is automatically assigned to it when you enable GuardDuty for the permissions required to evaluate your trusted IP lists and threat lists\. 

Note the following when creating trusted IP lists and threat lists that you plan to upload with GuardDuty:
+ In your trusted IP lists and threat lists, IP addresses and CIDR ranges must appear one per line\.

  The following is a sample list in Plaintext format:

  ```
  54.20.175.217
  205.0.0.0/8
  ```
+ Trusted IP list and threat lists apply only to traffic destined for publicly routable IP addresses\.
+ GuardDuty doesn't generate findings based on activity that involves domain names that are included in your threat lists\. GuardDuty only generates findings based on activity that involves IP addresses and CIDR ranges in your threat lists\.
+ The maximum size of the file that hosts your trusted IP list or threat list is 35MB\.
+ You can include a maximum of 2000 IP addresses and CIDR ranges in a single trusted IP list\.
+ You can include a maximum of 250,000 IP addresses and CIDR ranges in a single threat list\.
+ If your list is encrypted using server\-side encryption \(SSE\)\-KMS you must grant the GuardDuty service\-linked role **AWSServiceRoleForAmazonGuardDuty** permission to decrypt the file in order to activate the list\. Add the following statement to the KMS key policy and replace the account ID with your own: 

  ```
  {
  	"Sid": "Allow access for GuardDuty Service Role",
  	"Effect": "Allow",
  	"Principal": {
  		"AWS": "arn:aws:iam::123456789123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
  	},
  	"Action": "kms:Decrypt*",
  	"Resource": "*"
  }
  ```

**Topics**
+ [Permissions required to upload trusted IP lists and threat lists](#upload-permissions)
+ [To upload trusted IP lists and threat lists](#upload-procedure)
+ [To activate or deactivate trusted IP lists and threat lists](#activate-procedure)
+ [To update trusted IP lists and threat lists](#update-lists-procedure)

## Permissions required to upload trusted IP lists and threat lists<a name="upload-permissions"></a>

Various IAM identities require special permissions to work with trusted IP lists and threat lists in GuardDuty\. An identity with the **AmazonGuardDutyFullAccess** managed policy attached can only rename and deactivate uploaded trusted IP lists and threat lists\.

To grant various identities full access to working with trusted IP lists and threat lists \(in addition to renaming and deactivating, this includes uploading, activating, deleting, and updating the location of the lists\), make sure that the following actions are present in the permissions policy attached to an IAM user, group, or role: 

```
        {
            "Effect": "Allow",
            "Action": [
                "iam:PutRolePolicy",
                "iam:DeleteRolePolicy"
            ],
            "Resource": "arn:aws:iam::123456789123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
        }
```

**Important**  
These actions are not included in the **AmazonGuardDutyFullAccess** managed policy\.

## To upload trusted IP lists and threat lists<a name="upload-procedure"></a>

The following procedure describes how you can upload trusted IP lists and threat lists using the GuardDuty console\. 

**To upload trusted IP lists and threat lists \(console\)**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation pane, under **Settings**, choose **Lists**\.

1. On the **List management** page, choose **Add a trusted IP list** or **Add a threat list**\.

1. In the dialog box, do the following:
   + For **List name**, type a name for the list\.
   + For **Location**, specify the location of the list \- this is the S3 bucket where you store your trusted IP list or threat list and the file that contains your list\. 
**Note**  
You can specify the location URL in the following formats:  
https://s3\.amazonaws\.com/bucket\.name/file\.txt
https://s3\-aws\-region\.amazonaws\.com/bucket\.name/file\.txt
http://bucket\.s3\.amazonaws\.com/file\.txt
http://bucket\.s3\-aws\-region\.amazonaws\.com/file\.txt
s3://mybucket/file\.txt
   + For **Format**, choose your list's file type\.
   + Select the **I agree** check box\.
   + Choose **Add list**\.

## To activate or deactivate trusted IP lists and threat lists<a name="activate-procedure"></a>

The following procedures describe how you can activate or deactivate trusted IP lists and threat lists in GuardDuty once they are uploaded\. GuardDuty includes the uploaded lists in its monitoring of your AWS environment only if they are active\. 

**To activate trusted IP lists and threat lists \(console\)**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation pane, under **Settings**, choose **Lists**\.

1. On the **List management** page, locate the trusted IP set or a threat list that you want to activate, and then choose the radio button under the **Active** column\.

**To deactivate trusted IP lists and threat lists \(API or CLI\)**
+ Currently in GuardDuty, deactivating trusted IP lists and threat lists through the console is not supported\.

  You can deactivate your trusted IP lists or threat lists by running the [UpdateThreatIntelSet](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateThreatIntelSet.html) and [UpdateIPSet](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateIPSet.html) operations, or the [update\-ip\-set](https://docs.aws.amazon.com/cli/latest/reference/guardduty/update-ip-set.html) and [update\-threat\-intel\-set](https://docs.aws.amazon.com/cli/latest/reference/guardduty/update-threat-intel-set.html) CLI commands\. 

  For example, you can run the following command:

  ```
  aws guardduty update-ip-set --detector-id <detector-id> --ip-set-id <ip-set-id> --no-activate
  ```

  Make sure to replace <detector\-id> and <ip\-set\-id> with a valid detector ID and trusted IP list ID\.

## To update trusted IP lists and threat lists<a name="update-lists-procedure"></a>

If you make changes to a trusted IP list or a threat list that is already uploaded and activated in GuardDuty \(for example, rename the list or add more IP addresses to it\), you must update this list in GuardDuty and reactivate it in order for GuardDuty to use the latest version of the list in its security monitoring scope\. To update a safe or threat list, you can either use the procedure below or run the [UpdateThreatIntelSet](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateThreatIntelSet.html) and [UpdateIPSet](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateIPSet.html) operations of the GuardDuty API\.

**To update trusted IP lists and threat lists \(console\)**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation pane, under **Settings**, choose **Lists**\.

1. On the **List management** page, locate the trusted IP set or a threat list that you want to update, and then choose the pencil icon under the **Active** column\.

1. In the **Update list** pop up window, verify all specified list information, choose **I agree**, and then choose **Update list**\.

1. On the **List management** page, locate the trusted IP set or a threat list that you want to activate again, and then choose the radio button under the **Active** column\.

To learn how to import threat intel feeds programatically, see the [How to automate the import of third\-party threat intelligence feeds](http://aws.amazon.com/blogs/security/how-to-automate-import-third-party-threat-intelligence-feeds-into-amazon-guardduty/) blog article\.