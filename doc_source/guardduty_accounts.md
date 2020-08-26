# Managing multiple accounts in Amazon GuardDuty<a name="guardduty_accounts"></a>

To manage multiple accounts in Amazon GuardDuty, you must choose a single AWS account to be the master account for GuardDuty\. You can then associate other AWS accounts with the master account as member accounts\. There are two ways to associate accounts with a GuardDuty master account: either through an AWS Organizations organization that both accounts are members of, or by sending an invitation through GuardDuty\.

GuardDuty recommends using the AWS Organizations method\. For more information about setting up an organization, see [Creating an organization](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_create.html) in the *AWS Organizations User Guide*\. 

## Managing multiple accounts with AWS Organizations<a name="organization_method"></a>

If the account that you want to specify as the GuardDuty master account is part of an organization in AWS Organizations, then you can specify that account as the organization's delegated administrator for GuardDuty\. The account that is registered as the delegated administrator automatically becomes the GuardDuty master account\. 

You can use the master account to enable GuardDuty for any account in the organization and then add that account as a member account\. 

If you already have a GuardDuty master account with associated member accounts by invitation, you can register that account as the GuardDuty delegated administrator for the organization\. When you do, all currently associated member accounts remain members, allowing you to take full advantage of the added functionality of managing your GuardDuty accounts with AWS Organizations\.

 For more information about supporting multiple accounts in GuardDuty through an organization see [Managing GuardDuty accounts with AWS Organizations](guardduty_organizations.md)\. 

## Managing multiple accounts by invitation<a name="invitation_method"></a>

If the accounts you want to associate are not part of an AWS Organizations organization, you can specify a master account in GuardDuty and then use the master account to invite other AWS accounts to become member accounts\. When the invited account accepts the invitation, that account becomes a GuardDuty member account associated with the master account\. 

For more information about supporting multiple accounts by Invitation in GuardDuty see [Managing GuardDuty accounts by invitation](guardduty_invitations.md)\. 

## Understanding the relationship between GuardDuty master and member accounts<a name="master_member_relationships"></a>

When you use GuardDuty in a multiple\-account environment, the master account can manage certain aspects of GuardDuty on behalf of the member accounts\. The primary functions the master account can perform are the following:
+ Add and remove associated member accounts\. The process by which this is done differs based on whether the accounts are associated through organizations or by invitation\.
+ Manage the status of GuardDuty within associated member accounts, including enabling and suspending GuardDuty\.
**Note**  
Master accounts managed with AWS Organizations automatically enable GuardDuty in accounts added as members\.
+ Customize findings within the GuardDuty network through the creation and management of suppression rules, trusted IP lists, and threat lists\. Member accounts lose access to these features in a multiple\-account environment\.

The following table details the relationship between GuardDuty master and member accounts\.

Account designations listed as *Self* can take the listed action only in their own accounts\. A designation of *Any* indicates that account can perform the described action for any associated account, and *All* denotes actions that are applied to all associated accounts when taken by the designated account\. Table cells with dashes \(–\) indicate that an account of that designation cannot preform the listed action\.

[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/guardduty_accounts.html)

\* Indicates this action must be taken for all associated accounts before being taken in the designated account\.