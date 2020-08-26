# Managing GuardDuty accounts by invitation<a name="guardduty_invitations"></a>

To manage accounts outside of your organization, you can use the legacy invitation method\. When you use this method, your account is designated as a master account when another account accepts your invitation to become a member account\. 

If your account is not a master account, you can accept an invitation from another account\. When you accept, your account becomes a member account\. An AWS account cannot be a GuardDuty master and member account at the same time\.

Accounts associated by invitation have the same overall master\-to\-member relationship as accounts associated by AWS Organizations, as described in [Understanding the relationship between GuardDuty master and member accounts](guardduty_accounts.md#master_member_relationships)\. However, invitation master account users cannot enable GuardDuty on behalf of associated member accounts or view other non\-member accounts within their AWS Organizations organization\.

**Important**  
Cross\-Regional data transfer may occur when GuardDuty creates member accounts using this method\. In order to verify member accounts' email addresses, GuardDuty uses an email verification service that operates only in the US East \(N\. Virginia\) Region\.

## Designating master and member accounts through invitation \(console\)<a name="guardduty_become_console"></a>

Use the following procedures to add an account, invite an account, or accept an invitation from another account\.

### Step 1 \- add an account<a name="guardduty_add_member_proc"></a>

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation pane, choose **Accounts**\. 

1. Choose **Add accounts by invitation** in the top panel\.

1. On the **Add member accounts** page, under **Enter accounts**, enter the AWS account ID and email address of the account that you want to add\. Then choose **Add**\.
**Important**  
The email address that you specify in this step MUST be identical to the email address associated with the AWS account that you want to add as GuardDuty member account\.

   You can add more accounts, one at a time, by specifying their IDs and email addresses\. You can also choose **Upload list \(\.csv\)** to bulk add accounts\. This can be useful if you want to invite some of these accounts to enable GuardDuty right away but want to delay for others\.
**Important**  
The first line of your CSV file must contain the following header, as shown in the following example: **Account ID,Email**\. Each subsequent line must contain a single valid account ID and a single valid email address for the account that you want to add\. Accounts must appear one per line, and the account ID and email address must be separated by a comma\.   

   ```
   Account ID,Email
   111111111111,user@example.com
   ```

1. When you are finished adding accounts, choose **Next**\. 

   The added accounts appear in a list on the **Accounts** page\. Each added account in this list has an **Invite** link in the **Status** column\. 

### Step 2 \- invite an account<a name="guardduty_invite_member_proc"></a>

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation pane, choose **Accounts**\. 

1. For the account that you want to invite to enable GuardDuty, choose the **Invite** link that appears in the **Status** column of the added accounts list\.

1. In the **Invitation to GuardDuty** dialog box, enter an invitation message \(optional\), and then choose **Send notification**\.
**Note**  
If the invited account does not have access to email, select **Also send an email notification to the root user on the invitee's AWS account and generate an alert in the invitee's Personal Health Dashboard** before sending the invitation\.

   The value in the **Status** column for the invited account changes to **Pending**\.

### Step 3 \- accept an invitation<a name="guardduty_accept_invite_proc"></a>

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. Do one of the following:
   + If you don't have GuardDuty enabled, on the **Enable GuardDuty** page, choose **Enable GuardDuty**\. Then use the **Accept** widget and the **Accept invitation** button to accept the membership invitation\.
**Important**  
You must enable GuardDuty before you can accept a membership invitation\.
   + If you already have GuardDuty enabled, use the **Accept** widget and the **Accept invitation** button to accept the membership invitation\.

   After you accept the invitation, your account becomes a GuardDuty member account\. The account whose user sent the invitation becomes the GuardDuty master account\. The master account user can see that the value in the **Status** column for your member account changes to **Monitored**\. The master account user can now view and manage GuardDuty findings for your member account\.

## Designating GuardDuty master and member accounts through invitation \(API\)<a name="guardduty_become_api"></a>

You can designate master and member GuardDuty accounts by invitation through the API operations\. Run the following GuardDuty API operations in order to designate master and member accounts in GuardDuty\.

Complete the following procedure using the credentials of the AWS account that you want to designate as the GuardDuty master account\.

****

1. Run the [CreateMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateMembers.html) API operation using the credentials of the AWS account that has GuardDuty enabled\. This is the account that you want to be the master GuardDuty account\.

    You must specify the detector ID of the current AWS account and the account ID and email address of the accounts that you want to become GuardDuty members\. You can create one or more members with this API operation\.

   You can also use AWS Command Line Tools to designate a master account by running the following CLI command\. Make sure to use your own valid detector ID, account ID, and email\.

   ```
   aws guardduty create-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-details AccountId=123456789012,Email=guarddutymember@amazon.com
   ```

1. Run the [InviteMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_InviteMembers.html) API operation using the credentials of the AWS account that has GuardDuty enabled\. This is the account that you want to be the master GuardDuty account\.

    You must specify the detector ID of the current AWS account and the account IDs of the accounts that you want to become GuardDuty members\. You can invite one or more members with this API operation\.
**Note**  
You can also specify an optional invitation message using the `message` request parameter\.

   You can also use AWS Command Line Tools to designate member accounts by running the following CLI command\. Make sure to use your own valid detector ID and valid account IDs for the accounts you want to invite\. 

   ```
   aws guardduty invite-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-ids 123456789012
   ```

Complete the following procedure using the credentials of each AWS account that you want to designate as a GuardDuty member account\.

****

1. Run the [CreateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) API operation for each AWS account that was invited to become a GuardDuty member account and that you want to accept an invitation\. 

   You must specify if the detector resource is to be enabled using the GuardDuty service\. A detector must be created and enabled in order for GuardDuty to become operational\. You must first enable GuardDuty before accepting an invitation\.

   You can also do this by using AWS Command Line Tools using the following CLI command\.

   ```
   aws guardduty create-detector --enable
   ```

1. Run the [AcceptInvitation](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_AcceptInvitation.html) API operation for each AWS account that you want to accept the membership invitation, using that account's credentials\. 

   You must specify the detector ID of this AWS account for the member account, the account ID of the master account that sent the invitation, and the invitation ID of the invitation that you are accepting\. You can find the account ID of the master account in the invitation email or by using the [https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListInvitations.html](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListInvitations.html) operation of the API\.

   You can also accept an invitation using AWS Command Line Tools by running the following CLI command\. Make sure to use a valid detector ID, master account ID, and invitation ID\.

   ```
   aws guardduty accept-invitation --detector-id 12abc34d567e8fa901bc2d34e56789f0 --master-id 012345678901 --invitation-id 84b097800250d17d1872b34c4daadcf5 
   ```

## Enable GuardDuty in multiple accounts simultaneously<a name="guardduty_become_multiple"></a>

Use the following method to enable GuardDuty in multiple accounts at the same time\.

### Use Python scripts to enable GuardDuty in multiple accounts simultaneously<a name="guardduty_become_scripts"></a>

You can automate the enabling or disabling of GuardDuty on multiple accounts using the scripts from the sample repository on GitHub at [https://github\.com/aws\-samples/amazon\-guardduty\-multiaccount\-scripts](https://github.com/aws-samples/amazon-guardduty-multiaccount-scripts)\. Use the process in this section to enable GuardDuty for a list of member accounts using Amazon EC2\. For information about using the disable script or setting up the script locally refer, to the GitHub instructions\.

The enableguardduty\.py script enables GuardDuty, sends invitations from the master account, and accepts invitations in all member accounts\. The result is a master GuardDuty account that contains all security findings for all member accounts\. Because GuardDuty is isolated by Region, findings for each member account roll up to the corresponding Region in the master account\. For example, the us\-east\-1 Region in your GuardDuty master account contains the security findings for all us\-east\-1 findings from all associated member accounts\.

These scripts have a dependency on a shared IAM role with the managed policy **AmazonGuardDutyFullAccess**\. This policy provides entities access to GuardDuty and must be present on the master account and in each account for which you want to enable GuardDuty\.

The following process enables GuardDuty in all available Regions by default\. You can enable GuardDuty in specified Regions only by using the optional `--enabled_regions` argument and providing a comma\-separated list of Regions\. You can also optionally customize the invitation message that is sent to member accounts by opening the `enableguardduty.py` and editing the `gd_invite_message` string\. 

1. Create an IAM role in the GuardDuty master account and attach the **AmazonGuardDutyFullAccess** managed policy with the following permissions\.

   ```
                           {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": "guardduty:*",
               "Resource": "*"
           },
           {
               "Effect": "Allow",
               "Action": "iam:CreateServiceLinkedRole",
               "Resource": "*",
               "Condition": {
                   "StringLike": {
                       "iam:AWSServiceName": "guardduty.amazonaws.com"
                   }
               }
           }
       ]
   }
   ```

1. Create an IAM role in each member account you want to be managed by your GuardDuty master account\. This role must have the same name as the role created in step 1, it should allow the master account as a trusted entity, and it should have the same **AmazonGuardDutyFullAccess** managed policy described previously\.

1. Launch a new Amazon Linux instance with an attached role that has the following trust relationship that allows the instance to assume a service role\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "ec2.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

1. Log in to the new instance and run the following commands to set it up\.

   ```
   sudo yum install git python 
   sudo yum install python-pip
   pip install boto3 
   aws configure 
   git clone https://github.com/aws-samples/amazon-guardduty-multiaccount-scripts.git
   cd amazon-guardduty-multiaccount-scripts 
   sudo chmod +x disableguardduty.py enableguardduty.py
   ```

1. Create a CSV file containing a list of account IDs and emails of the member accounts that you added a role to in step 2\. Accounts must appear one per line, and the account ID and email address must be separated by a comma as in the following example\.

   ```
   111111111111,user@example.com
   ```
**Note**  
 The CSV file must be in the same location as your `enableguardduty.py` script\. You can copy an existing CSV file from Amazon S3 to your current directory with the following method\.   

   ```
   aws s3 cp s3://my-bucket/my_key_name example.csv
   ```

1. Run the Python script\. Make sure to supply your GuardDuty master account ID, the name of the role created in the first steps, and the name of your CSV file as arguments\.

   ```
   python enableguardduty.py --master_account 111111111111 --assume_role roleName accountID.csv
   ```