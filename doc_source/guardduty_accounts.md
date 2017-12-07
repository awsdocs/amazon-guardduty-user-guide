# Managing AWS Accounts in Amazon GuardDuty<a name="guardduty_accounts"></a>

You can invite other accounts to enable GuardDuty and become associated with your AWS account\. If your invitations are accepted, your account is designated as the **master** GuardDuty account, and the associated accounts become your **member** accounts\. You can then view and manage their GuardDuty findings on their behalf\. In GuardDuty, a master account can have up to 100 member accounts\. 

**Important**  
An AWS account cannot be a GuardDuty master and member account at the same time\. An AWS account can accept only one membership invitation\. Accepting a membership invitation is optional\.


+ [GuardDuty Master Accounts](#guardduty_master)
+ [GuardDuty Member Accounts](#guardduty_member)
+ [Designating Master and Member Accounts Through GuardDuty Console](#guardduty_become_console)
+ [Designating Master and Member Accounts Through the GuardDuty API Operations](#guardduty_become_api)

## GuardDuty Master Accounts<a name="guardduty_master"></a>

Users from the master account can configure GuardDuty as well as view and manage GuardDuty findings for their own account and all of their member accounts\. 

The following is how a master account can configure GuardDuty:

+ Users from master accounts can generate sample findings\.

+ Users from master accounts can upload and further manage trusted IP lists and threat lists in their own account\. 
**Note**  
Trusted IP lists and threat lists that are uploaded by the master account are NOT imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty still generates findings based on activity that involves IP addresses from the master's trusted IP lists and does not generate findings based on activity that involves known malicious IP addresses from the master's threat lists\.

+ Users from master accounts can suspend GuardDuty for its own \(master\) account and all member accounts\.

+ Users from master accounts can disable GuardDuty in its own \(master\) account\. However, all member accounts must first be removed to disable GuardDuty in the master account\. A master account CANNOT disable GuardDuty for member accounts\.

## GuardDuty Member Accounts<a name="guardduty_member"></a>

Users from member accounts can configure GuardDuty as well as view and manage GuardDuty findings in their account\. Member account users can't configure GuardDuty or view or manage findings in the master or other member accounts\. 

The following is how a member account can configure GuardDuty:

+ Users from member accounts can generate sample findings\.

+ Users from member accounts can upload and further manage trusted IP lists and threat lists in their own account\. 
**Note**  
Trusted IP lists and threat lists that are uploaded by the master account are NOT imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty still generates findings based on activity that involves IP addresses from the master's trusted IP lists and does not generate findings based on activity that involves known malicious IP addresses from the master's threat lists\.

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

1. Run the [InviteMembers](invite-members.md) API operation using the credentials of the AWS account that has GuardDuty enabled \(this is the account that you want to be the master GuardDuty account\.

    You must specify the detector ID of the current AWS account and the account IDs \(you can invite one or more members with this API operation\) of the accounts that you want to become GuardDuty members\.
**Note**  
You can also specify an optional invitation message using the `message` request parameter\.

Complete the following procedure using the credentials of each AWS account that you want to designate as the GuardDuty member account\.

****

1. Run the [CreateDetector](create-detector.md) API operation for each AWS account that was invited to become a GuardDuty member account and where you want to accept an invitation\. 

   You must specify if the detector resource is to be enabled using the GuardDuty service\. A detector must be created and enabled in order for GuardDuty to become operational\. You must first enable GuardDuty before accepting an invitation\.

1. Run the [AcceptInvitation](accept-invitation.md) API operation for each AWS account where you want to accept the membership invitation using that account's credentials\. 

   You must specify the detector ID of this AWS account \(member account\), the master ID of the AWS account that sent the invitation that you are accepting \(you can get this value either from the invitation email or by running the [ListInvitations](list-invitations.md) API operation\. It is the value of the `accountID` response parameter\), and the invitation ID of the invitation that you are accepting\. 