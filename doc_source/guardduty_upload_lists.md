# Uploading Trusted IP Lists and Threat Lists<a name="guardduty_upload_lists"></a>

Amazon GuardDuty monitors the security of your AWS environment by analyzing and processing VPC Flow Logs, AWS CloudTrail event logs, and DNS logs\. You can expand this monitoring scope by configuring GuardDuty to also use your own custom *trusted IP lists* and *threat lists*\.

Trusted IP lists consist of IP addresses that you have whitelisted for secure communication with your AWS infrastructure and applications\. GuardDuty does not generate findings for IP addresses on trusted IP lists\. At any given time, you can have only one uploaded trusted IP list\.

Threat lists consist of known malicious IP addresses\. GuardDuty generates findings based on threat lists\. At any given time, you can have up to six uploaded threat lists\.

Users from both, master and member GuardDuty accounts can upload and manage trusted IP lists and threat lists\. For more information, see [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

**Important**  
GuardDuty uses the same `AWSServiceRoleForAmazonGuardDuty` service\-linked role that is automatically assigned to it when you enable GuardDuty for the permissions required to evaluate your trusted IP lists and threat lists\. 

Note the following when creating trusted IP lists and threat lists that you plan to upload with GuardDuty:

+ In your trusted IP lists and threat lists, IP addresses and CIDR ranges must appear one per line\.

  The following is a sample list in Plaintext format:

  ```
  54.20.175.217
  205.0.0.0/8
  ```

+ GuardDuty doesn't generate findings for any non\-routable or internal IP addresses in your threat lists\.

+ GuardDuty doesn't generate findings based on activity that involves domain names that are included in your threat lists\. GuardDuty only generates findings based on activity that involves IP addresses and CIDR ranges in your threat lists\.

## Permissions Required to Upload Trusted IP Lists and Threat Lists<a name="upload-permissions"></a>

To provide various identities with the ability to upload and manage trusted IP lists and threat lists, make sure that the following actions are present in the permissions policy attached to an IAM user, group, or role:

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

## To Upload Trusted IP Lists and Threat Lists<a name="upload-procedure"></a>

The following procedure describes how you can upload trusted IP lists and threat lists using the GuardDuty console\. 

**To upload trusted IP lists and threat lists \(console\)**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\.

1. In the navigation pane, under **Settings**, choose **Lists**\.

1. On the **List management** page, choose **Add a trusted IP list** or **Add a threat list**\.

1. In the dialog box, do the following:

   + For **List name**, type a name for the list\.

   + For **Location**, specify the location of the list in the format of `https://s3.amazonaws.com/bucket.name/file.txt` \- this is the S3 bucket where you store your trusted IP list or threat list and the file that contains your list\. 

   + For **Format**, choose your list's file type\.

   + Select the **I agree** check box\.

   + Choose **Add list**\.