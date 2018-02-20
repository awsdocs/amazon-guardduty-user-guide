# Managing AWS Accounts in Amazon GuardDuty<a name="guardduty_accounts"></a>

You can invite other accounts to enable GuardDuty and become associated with your AWS account\. If your invitations are accepted, your account is designated as the **master** GuardDuty account, and the associated accounts become your **member** accounts\. You can then view and manage their GuardDuty findings on their behalf\. In GuardDuty, a master account \(per region\) can have up to 1000 member accounts\. 

**Important**  
An AWS account cannot be a GuardDuty master and member account at the same time\. An AWS account can accept only one membership invitation\. Accepting a membership invitation is optional\.


+ [GuardDuty Master Accounts](#guardduty_master)
+ [GuardDuty Member Accounts](#guardduty_member)
+ [Designating Master and Member Accounts Through GuardDuty Console](#guardduty_become_console)
+ [Designating Master and Member Accounts Through the GuardDuty API Operations](#guardduty_become_api)
+ [Enable GuardDuty in Multiple Accounts Simultaneously](#guardduty_become_scripts)

## GuardDuty Master Accounts<a name="guardduty_master"></a>

Users from the master account can configure GuardDuty as well as view and manage GuardDuty findings for their own account and all of their member accounts\. 

The following is how a master account can configure GuardDuty:

+ Users from master accounts can generate sample findings\.

+ Users from master accounts can archive findings in their own accounts and in all member accounts\.

+ Users from master accounts can upload and further manage trusted IP lists and threat lists in their own account\. 
**Important**  
Trusted IP lists and threat lists that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty does not generate findings based on activity that involves IP addresses from the master's trusted IP lists and generates findings based on activity that involves known malicious IP addresses from the master's threat lists\.

+ Users from master accounts can suspend GuardDuty for its own \(master\) account and all member accounts\.

+ Users from master accounts can disable GuardDuty in its own \(master\) account\. However, all member accounts must first be removed to disable GuardDuty in the master account\. A master account CANNOT disable GuardDuty for member accounts\.

## GuardDuty Member Accounts<a name="guardduty_member"></a>

Users from member accounts can configure GuardDuty as well as view and manage GuardDuty findings in their account\. Member account users can't configure GuardDuty or view or manage findings in the master or other member accounts\. 

The following is how a member account can configure GuardDuty:

+ Users from member accounts can generate sample findings\.

+ Users from member accounts CANNOT archive findings either in their own accounts or in their master's account, or in other member accounts\.

+ Users from member accounts CANNOT upload and further manage trusted IP lists and threat lists\. 

  Trusted IP lists and threat lists that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty does not generate findings based on activity that involves IP addresses from the master's trusted IP lists and generates findings based on activity that involves known malicious IP addresses from the master's threat lists\.
**Note**  
When a GuardDuty account becomes a GuardDuty member account, all of its trusted IP lists and threat lists \(uploaded prior to becoming a GuardDuty member account\) are disabled\. If a GuardDuty member account disassociates from its GuardDuty master account, all of its trusted IP lists and threat lists \(uploaded prior to becoming a GuardDuty member account\) are re\-enabled\. Once no longer a GuardDuty member account, this account's users can upload and further manage trusted IP lists and threat lists in this account\. 

+ Users from member accounts can suspend GuardDuty for their own account, but not for the master account or other member accounts\.

+ Users from member accounts can disable GuardDuty for their own account, but not for the master account or other member accounts\.

## Designating Master and Member Accounts Through GuardDuty Console<a name="guardduty_become_console"></a>

In GuardDuty, your account is designated a master account when you add another AWS account to be associated with your account or when another account accepts your invitation to become a member account\. 

If your account is a non\-master account, you can accept an invitation from another account\. When you accept, your account becomes a member account\. 

Use the following procedures to add an account, invite an account, or accept an invitation from another account\.

+ Step 1 \- Add an account

+ Step 2 \- Invite an account

+ Step 3 \- Accept an invitation

**Step 1 \- Add an account**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\.

1. In the navigation pane, under **Settings**, choose **Accounts**\. 

1. Choose **Add accounts**\.

1. On the **Add member** accounts page, under **Enter accounts**, type the AWS account ID and email address of the account that you want to add\. Then choose **Add account**\.

   You can add more accounts, one at a time, by specifying their IDs and email addresses\. You can also choose **Upload list \(\.csv\)** to bulk add accounts\. This can be useful if you want to invite some of these accounts to enable GuardDuty right away but want to delay for others\.
**Important**  
In your \.csv list, accounts must appear one per line\. For each account in your \.csv list, you must specify the account ID and the email address separated by a comma\. The first line of your \.csv file must contain the following header, as shown in the example below: **Account ID,Email**\. Each subsequent line must contain a valid account ID and a valid email address for the account that you want to add\. The account ID and email address must be separated by a comma\.   

   ```
   Account ID,Email
   111111111111,user@example.com
   ```

1. When you are finished adding accounts, choose **Done**\. 

   The added accounts appear in a list on the **Accounts** page\. Each added account in this list has an **Invite** link in the **Status** column\. 

**Step 2 \- Invite an account**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\.

1. In the navigation pane, under **Settings**, choose **Accounts**\. 

1. For the account that you want to invite to enable GuardDuty, choose the **Invite** link that appears in the **Status** column of the added accounts list\.

1. In the **Invitation to GuardDuty** dialog box, type an invitation message \(optional\), and then choose **Send notification**\.

   The value in the **Status** column for the invited account changes to **Pending**\.

**Step 3 \- Accept an invitation**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\.

1. Do one of the following:

   + If you don't have GuardDuty enabled, on the **Enable GuardDuty** page, choose **Enable GuardDuty**\. Then use the **Accept** widget and the **Accept invitation** button to accept the membership invitation\.
**Important**  
You must enable GuardDuty before you can accept a membership invitation\.

   + If you already have GuardDuty enabled, use the **Accept** widget and the **Accept invitation** button to accept the membership invitation\.

   After you accept the invitation, your account becomes a GuardDuty member account\. The account whose user sent the invitation becomes the GuardDuty master account\. The master account user can see that the value in the **Status** column for your member account changes to **Monitored**\. The master account user can now view and manage GuardDuty findings for your member account\.

## Designating Master and Member Accounts Through the GuardDuty API Operations<a name="guardduty_become_api"></a>

You can also designate master and member GuardDuty accounts through the API operations\. The following is the order in which these particular GuardDuty API operations must be run in order to designate master and member accounts in GuardDuty\.

Complete the following procedure using the credentials of the AWS account that you want to designate as the GuardDuty master account\.

****

1. Run the [CreateMembers](create-members.md) API operation using the credentials of the AWS account that has GuardDuty enabled \(this is the account that you want to be the master GuardDuty account\)\.

    You must specify the detector ID of the current AWS account and the account details \(account ID and email address\) of the account\(s\) of the accounts that you want to become GuardDuty members \(you can create one or more members with this API operation\)\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command \(make sure to use your own valid detector ID, account ID, and email: 

   ```
   aws guardduty create-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-details AccountId=123456789012,Email=guarddutymember@amazon.com
   ```

1. Run the [InviteMembers](invite-members.md) API operation using the credentials of the AWS account that has GuardDuty enabled \(this is the account that you want to be the master GuardDuty account\.

    You must specify the detector ID of the current AWS account and the account IDs \(you can invite one or more members with this API operation\) of the accounts that you want to become GuardDuty members\.
**Note**  
You can also specify an optional invitation message using the `message` request parameter\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command \(make sure to use your own valid detector ID and account IDs: 

   ```
   aws guardduty invite-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-ids 123456789012
   ```

Complete the following procedure using the credentials of each AWS account that you want to designate as the GuardDuty member account\.

****

1. Run the [CreateDetector](create-detector.md) API operation for each AWS account that was invited to become a GuardDuty member account and where you want to accept an invitation\. 

   You must specify if the detector resource is to be enabled using the GuardDuty service\. A detector must be created and enabled in order for GuardDuty to become operational\. You must first enable GuardDuty before accepting an invitation\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command: 

   ```
   aws guardduty create-detector --enable
   ```

1. Run the [AcceptInvitation](accept-invitation.md) API operation for each AWS account where you want to accept the membership invitation using that account's credentials\. 

   You must specify the detector ID of this AWS account \(member account\), the master ID of the AWS account that sent the invitation that you are accepting \(you can get this value either from the invitation email or by running the [ListInvitations](list-invitations.md) API operation\. It is the value of the `accountID` response parameter\), and the invitation ID of the invitation that you are accepting\. 

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command \(make sure to use valide detector ID, master account ID, and invitation ID: 

   ```
   aws guardduty accept-invitation --detector-id 12abc34d567e8fa901bc2d34e56789f0 --master-id 012345678901 --invitation-id 84b097800250d17d1872b34c4daadcf5 
   ```

## Enable GuardDuty in Multiple Accounts Simultaneously<a name="guardduty_become_scripts"></a>

To enable GuardDuty in multiple accounts at the same time, you can run enableguardduty\.py and disableguardduty\.py, which you can download from the following page: [https://github\.com/aws\-samples/amazon\-guardduty\-multiaccount\-scripts](https://github.com/aws-samples/amazon-guardduty-multiaccount-scripts)\.

enableguardduty\.py enables GuardDuty, sends invitations from the master account and accepts invitations in all member accounts\. The result is a master GuardDuty account that contains all security findings for all member accounts\. Since GuardDuty is regionally isolated, findings for each member account roll up to the corresponding region in the master account\. For example, the us\-east\-1 region in your GuardDuty master account contains the security findings for all us\-east\-1 findings from all associated member accounts\.

The scripts are modelled with the StackSets service in mind and are therefore dependent on having the IAM role called **AWSCloudFormationStackSetExecutionRole** in each account where you want to enable GuardDuty\. This role provides StackSets with access to GuardDuty\. If you already use StackSets, the scripts can leverage your existing roles\. If not, you can use the instructions in [https://docs\.aws\.amazon\.com/AWSCloudFormation/latest/UserGuide/stacksets\-prereqs\.html](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html) to setup the **AWSCloudFormationStackSetExecutionRole** in each account where you want to enable GuardDuty\. 

Launch a new Amazon Linux instance with a role that has administrative permissions\. Login to this instance and run the following commands:

```
sudo yum install git python 
sudo pip install boto3 
aws configure 
git clone https://github.com/aws-samples/amazon-guardduty-multiaccount-scripts.git
cd amazon-guardduty-multiaccount-scripts 
sudo chmod +x disableguardduty.py enableguardduty.py
```

**Note**  
When prompted, set the region to us\-east\-1 or whatever default region you want\.

The scripts have one parameter \- the account ID of your GuardDuty master account\. Before you execute enableguardduty\.py or disableguardduty\.py, update either script’s global variables to map to your AWS accounts\. You can create a list of the accounts and their associated email addresses\. Specify the master GuardDuty account and \(optionally\) customize the invite message that is sent to member accounts\. 