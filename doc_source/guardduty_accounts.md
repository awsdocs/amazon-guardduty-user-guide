# Managing Accounts in Amazon GuardDuty<a name="guardduty_accounts"></a>

You can invite other accounts to enable GuardDuty and become associated with your AWS account\. When an invitation is accepted, your account is designated as the **master** GuardDuty account\. The account that accepts the invitation becomes a **member** account associated with your master account\. You can then view and manage the GuardDuty findings on behalf of the member account\. In GuardDuty, a master account \(per region\) can have up to 1000 member accounts\.

An AWS account cannot be a GuardDuty master and member account at the same time\. An AWS account can accept only one GuardDuty membership invitation\. Accepting a membership invitation is optional\.

The following sections describe how to create master and member accounts using the GuardDuty console, CLI, and APIs\. You can also create master and member accounts through AWS CloudFormation\. For more information, see [AWS::GuardDuty::Master](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-master.html) and [AWS::GuardDuty::Member](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-guardduty-member.html)\.

**Note**  
Cross\-regional data transfer can occur when GuardDuty member accounts are created\. In order to verify member accounts' email addresses, GuardDuty uses a non\-AWS account information verification service that operates only in the AWS US East \(N\. Virginia\) Region\.

**Topics**
+ [GuardDuty Master Accounts](#guardduty_master)
+ [GuardDuty Member Accounts](#guardduty_member)
+ [Designating Master and Member Accounts Through GuardDuty Console](#guardduty_become_console)
+ [Designating Master and Member Accounts Through the GuardDuty API Operations](#guardduty_become_api)
+ [Enable GuardDuty in Multiple Accounts Simultaneously](#guardduty_become_multiple)

## GuardDuty Master Accounts<a name="guardduty_master"></a>

Users from the master account can configure GuardDuty as well as view and manage GuardDuty findings for their own account and all associated member accounts\.

The following is how users from a master account can configure GuardDuty:
+ Users from a master account can generate sample findings in their own account\. Users from a master account CANNOT generate sample findings in members' accounts\.
+ Users from a master account can archive findings in their own accounts and in all member accounts\. 
+ Users from a master account can upload and further manage trusted IP lists and threat lists in their own account\. 
**Important**  
Trusted IP lists and threat lists that are uploaded by the master account and in the master account are imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty generates findings based on activity that involves known malicious IP addresses from the master's threat lists and does not generate findings based on activity that involves IP addresses from the master's trusted IP lists\.
+ Users from a master account can customize the default frequency of notifications sent about the subsequent finding occurrences to CloudWatch Events\. Possible values are 15 minutes, 1 hour, or the default 6 hours\. For more information, see [Monitoring GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.

  The frequency value set by the master account in its own account is imposed on GuardDuty functionality in all its member accounts\. In other words, if a user from a master account sets this frequency value to 1 hour, all member accounts will also have the 1 hour frequency of notifications about the subsequent finding occurrences sent to CloudWatch Events\. 
+ Users from a master account can suspend GuardDuty for its own \(master\) account\. Users from a master account can also suspend GuardDuty in its member accounts\.
**Note**  
If a master account user suspends GuardDuty in the master account, this suspension is NOT automatically imposed on the member accounts\. To suspend GuardDuty for member accounts, a user from a master account must select these member accounts and suspend GuardDuty through the console or specify their account IDs when running the [StopMonitoringMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_StopMonitoringMembers.html) operation of the GuardDuty API\.  
A master account user can also re\-enable GuardDuty in member accounts either through the console or by running the [StartMonitoringMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_StartMonitoringMembers.html) operation\.
+ Users from a master account can disable GuardDuty in its own \(master\) account\. However, all member accounts must first be removed to disable GuardDuty in the master account\. Users from a master account CANNOT disable GuardDuty for member accounts\.

## GuardDuty Member Accounts<a name="guardduty_member"></a>

Users from member accounts can configure GuardDuty as well as view and manage GuardDuty findings in their account\. Member account users can't configure GuardDuty or view or manage findings in the master or other member accounts\. 

The following is how users from a member account can configure GuardDuty:
+ Users from a member account can generate sample findings in their own member account\. Users from a member account can't generate sample findings in the master or other member accounts\.
+ Users from a member account can't archive findings either in their own account or in their master's account, or in other member accounts\.
+ Users from a member account can't upload and further manage trusted IP lists and threat lists\. 

  Trusted IP lists and threat lists that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. In other words, in member accounts GuardDuty generates findings based on activity that involves known malicious IP addresses from the master's threat lists and does not generate findings based on activity that involves IP addresses from the master's trusted IP lists\.
**Note**  
When a GuardDuty account becomes a GuardDuty member account, all of its trusted IP lists and threat lists \(uploaded prior to becoming a GuardDuty member account\) are disabled\. If a GuardDuty member account disassociates from its GuardDuty master account, all of its trusted IP lists and threat lists \(uploaded prior to becoming a GuardDuty member account\) are re\-enabled\. Once no longer a GuardDuty member account, this account's users can upload and further manage trusted IP lists and threat lists in this account\. 
+ Users from member accounts can't customize the frequency of notifications about the subsequent finding occurrences sent to CloudWatch Events\. The frequency value set by the master account in its own account is imposed on GuardDuty functionality in all its member accounts\. In other words, if a user from a master account sets this frequency value to 1 hour, all member accounts will also have the 1 hour frequency of notifications about the subsequent finding occurrences sent to CloudWatch Events\. For more information, see [Monitoring GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.
+ Users from a member account can suspend GuardDuty for their own account\. Users from a member account can't suspend GuardDuty for the master account or other member accounts\.
+ Users from member accounts can disable GuardDuty for their own account\. Users from a member account can't disable GuardDuty for the master account or other member accounts\.

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
**Important**  
The email address that you specify in this step MUST be identical to the email address associated with the AWS account that you want to add as GuardDuty member account\.

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

1. Run the [CreateMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateMembers.html) API operation using the credentials of the AWS account that has GuardDuty enabled \(this is the account that you want to be the master GuardDuty account\)\.

    You must specify the detector ID of the current AWS account and the account details \(account ID and email address\) of the accounts that you want to become GuardDuty members \(you can create one or more members with this API operation\)\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command \(make sure to use your own valid detector ID, account ID, and email: 

   ```
   aws guardduty create-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-details AccountId=123456789012,Email=guarddutymember@amazon.com
   ```

1. Run the [InviteMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_InviteMembers.html) API operation using the credentials of the AWS account that has GuardDuty enabled \(this is the account that you want to be the master GuardDuty account\.

    You must specify the detector ID of the current AWS account and the account IDs \(you can invite one or more members with this API operation\) of the accounts that you want to become GuardDuty members\.
**Note**  
You can also specify an optional invitation message using the `message` request parameter\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command \(make sure to use your own valid detector ID and account IDs: 

   ```
   aws guardduty invite-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-ids 123456789012
   ```

Complete the following procedure using the credentials of each AWS account that you want to designate as the GuardDuty member account\.

****

1. Run the [CreateDetector](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateDetector.html) API operation for each AWS account that was invited to become a GuardDuty member account and where you want to accept an invitation\. 

   You must specify if the detector resource is to be enabled using the GuardDuty service\. A detector must be created and enabled in order for GuardDuty to become operational\. You must first enable GuardDuty before accepting an invitation\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command: 

   ```
   aws guardduty create-detector --enable
   ```

1. Run the [AcceptInvitation](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_AcceptInvitation.html) API operation for each AWS account where you want to accept the membership invitation using that account's credentials\. 

   You must specify the detector ID of this AWS account \(member account\), the account ID of the master account that sent the invitation, and the invitation ID of the invitation that you are accepting\. You can find the account ID of the master account from the invitation email, or by using the [https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListInvitations.html](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_ListInvitations.html) operation of the API\.

   You can also do this by using AWS Command Line Tools\. You can run the following CLI command \(make sure to use valid detector ID, master account ID, and invitation ID: 

   ```
   aws guardduty accept-invitation --detector-id 12abc34d567e8fa901bc2d34e56789f0 --master-id 012345678901 --invitation-id 84b097800250d17d1872b34c4daadcf5 
   ```

## Enable GuardDuty in Multiple Accounts Simultaneously<a name="guardduty_become_multiple"></a>

Use either of the methods below to enable GuardDuty in multiple accounts at the same time:

### Use Python Scripts to Enable GuardDuty in Multiple Accounts Simultaneously<a name="guardduty_become_scripts"></a>

You can run `enableguardduty.py` and `disableguardduty.py`, which you can download from the following page: [https://github\.com/aws\-samples/amazon\-guardduty\-multiaccount\-scripts](https://github.com/aws-samples/amazon-guardduty-multiaccount-scripts)\.

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

The scripts have one parameter \- the account ID of your GuardDuty master account\. Before you execute enableguardduty\.py or disableguardduty\.py, update either script's global variables to map to your AWS accounts\. You can create a list of the accounts and their associated email addresses\. Specify the master GuardDuty account and \(optionally\) customize the invite message that is sent to member accounts\. 

### Use AWS CloudFormation StackSets to Enable GuardDuty in Multiple Accounts Simultaneously<a name="guardduty_become_stackset"></a>

AWS CloudFormation stack sets enable you to create stacks in AWS accounts across regions by using a single AWS CloudFormation template\. All the resources included in each stack are defined by the stack set's AWS CloudFormation template\. As you create the stack set, you specify the template to use, as well as any parameters and capabilities that template requires\. 

You can use the **Enable Amazon GuardDuty** template to enable GuardDuty simultaneously in multiple accounts\. 

**Important**  
Before performing the procedure below, complete the prerequisite steps of granting permissions for stack set operations within your AWS accounts\. For more information, see [Prerequisites: Granting Permissions for Stack Set Operations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html)\.

1. Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation)\. 

1. At the top of the page, choose **StackSets**, and then choose **Create stack set**\. 

1. On the **Select template** page of the** Create stack set** wizard, choose **Select a sample template from the following templates**\. 

1. Choose the **Enable Amazon GuardDuty** sample template, and then choose **Next**\. 

1. On the **Specify details** page of the wizard, provide the following information\. 
   + Provide a name for the stack set\. Stack set names must begin with an alphabetical character, and contain only letters, numbers, and hyphens\.
   + Optional: provide the GuardDuty master account ID\.
**Important**  
If you specify the master account ID, this stack set creates a GuardDuty detector in each specified account and accepts the GuardDuty membership invitation sent to each of the specified accounts by this master account\. If this value is specified, before you can create this stack set, all accounts in all regions to which **Enable Amazon GuardDuty** stack set template is to be applied must already have an invitation from this master GuardDuty account and must NOT have a detector already created\. In other words, specify this value only if you want to use this stack set to enable GuardDuty in multiple member accounts and regions simultaneously and designate a particular account as the master GuardDuty account for all of these members\.  
If you do not specify the master account ID, this stack set simply creates a GuardDuty detector in each specified account\. In other words, do not specify this value if you want to use this stack set to enable GuardDuty in multiple unrelated \(with no member/master relationship\) accounts simultaneously\.

1. On the **Set deployment options** page, provide the accounts and regions into which you want stacks in your stack set deployed\. AWS CloudFormation deploys stacks in the specified accounts within the first region, then moves on to the next, and so on, as long as a region's deployment failures do not exceed a specified failure tolerance\. 
**Note**  
If you specify the master account ID on the previous page, this stack set creates a GuardDuty detector in each account listed in the **Specify accounts** section and accepts the GuardDuty membership invitation sent to each of these accounts by the master account\. Therefore, if you specified a GuardDuty master account, do not include this master account ID in the **Specify accounts** section and include only those accounts that you want to designate as members to this GuardDuty master account\. 

1. On the **Options** page, in the **Tags** section, you can add tags by specifying a key and value pair for the resources in your stack\.

   In the **Permissions** section, choose an IAM role that StackSets can use to manage your target accounts\. For detailed instructions on how to set up the IAM service roles for your administrator and all target accounts, see [Set Up Basic Permissions for Stack Sets Operations](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-prereqs.html#stacksets-prereqs-accountsetup)\.

1. On the **Review** page, review your choices and your stack set's properties\. When you are ready to create your stack set, choose **Create**\. 

For more information, see [Working with AWS CloudFormation StackSets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/what-is-cfnstacksets.html)\.