# Managing GuardDuty Accounts with AWS Organizations<a name="guardduty_organizations"></a>

When you use GuardDuty with an AWS Organizations organization, you designate an account to be the GuardDuty delegated administrator for the organization\. Only the organization master account can designate GuardDuty delegated administrators\.

**Note**  
The Organization master can be the delegated administrator, but this is not recommended based on AWS Security best practices following the principle of least of privilege\.

An account that is designated as a delegated administrator becomes a GuardDuty master account, has GuardDuty automatically enabled in the designated Region, and is granted permission to enable and manage GuardDuty for all accounts in the organization within that Region\. The other accounts in the organization can be viewed and added as GuardDuty member accounts associated with the master account\.

 If the organization’s GuardDuty delegated administrator is already a GuardDuty master with associated member accounts by invitation, and the member accounts are part of the same organization, their **Type** is **via Organizations** and the status is **Enabled**\. If the organization’s GuardDuty master previously added members by invitation that are not part of the same organization, their **Type** is **by Invitation**\. In both cases, these previously added accounts are member accounts to the organization’s GuardDuty delegated administrator\.

You can continue to add accounts as members even if they are outside of your organization\. To learn more, see [Designating Master and Member Accounts Through Invitation \(Console\)](guardduty_invitations.md#guardduty_become_console) and [Designating GuardDuty Master and Member Accounts Through Invitation \(API\)](guardduty_invitations.md#guardduty_become_api)\.

**Note**  
There is a limit of 5000 member accounts per GuardDuty master account\. However, there could be more than 5000 accounts in your organization\. The number of **All** accounts in your organization is displayed on the **Accounts** page of the GuardDuty console\.  
If you exceed 5000 member accounts you will receive a notification through CloudWatch, Personal Health Dashboard, and in an email to the master account\.

Use the following procedures to register a GuardDuty delegated administrator for your organization, add existing organization accounts as members, and automate the addition of new organization accounts as GuardDuty member accounts\.

## Designate a Delegated Administrator and add Member Accounts \(Console\)<a name="organization_thru_console"></a>

 Follow these steps to designate a GuardDuty delegated administrator and add member accounts using the GuardDuty console\.

**Important**  
You need to repeat these steps in each Region where you are using GuardDuty if you want to monitor all Regions for organization member accounts associated with the delegated administrator\.

### Step 1 \- Register a GuardDuty delegated administrator for your organization<a name="guardduty_register_delegate_admin_proc"></a>

1. Log in to the AWS Management Console using the master account for your AWS Organizations organization\.

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

   Is GuardDuty already enabled in your account?
   + If GuardDuty is not already enabled, you can designate a GuardDuty delegated administrator on the **Welcome to GuardDuty** page\.
   + If GuardDuty is enabled you can designate a GuardDuty delegated administrator on the **Settings** page\.

1. Enter the twelve\-digit AWS account ID of the account that you want to designate as the GuardDuty delegated administrator for the organization\.

1. Choose **Delegate**\.
**Note**  
If GuardDuty is not already enabled, designating a delegated administrator will enable GuardDuty for that account in your current Region\.

1. \(Recommended\) Repeat the previous steps in each AWS Region\.
**Note**  
It is recommended that you register the same delegated administrator in each AWS Region\.

After you designate the delegated administrator, you only need to use the master account organization to change or remove the delegated administrator account\.

**Note**  
If you remove the delegated administrator, all associated member accounts are removed as GuardDuty members, but GuardDuty is not disabled in those accounts\.

### Step 2 \- Add existing organization accounts as members<a name="guardduty_add_orgs_accounts"></a>

When you add an account as a member, GuardDuty is automatically enabled in that account in the current Region\.

You must add your organization members in each Region to enable GuardDuty for those Regions\.

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation panel, choose **Settings**, and then choose **Accounts**\.

   The accounts table displays all of the accounts in the organization\. The **Type** for these accounts is **via organizations**\. The status of accounts that are not member accounts associated with the organization’s GuardDuty delegated administrator is **Not a member**\.

1. Select the account or accounts that you want to add as members by checking the box next to the account ID\.
**Note**  
You can enable GuardDuty in the current Region for all organization accounts by selecting **enable** in the banner at the top of the page\. This action also triggers the *Auto\-Enable* feature that will enable GuardDuty in any future accounts added to your organization\.  
 Alternately, you can use the **filter** field to filter by **Relationship status: Not a member**, and then select every account that does not have GuardDuty enabled in the current Region\.

1. Choose **Actions** then choose **Add member**\.

1. Confirm that you want to add as members the number of accounts selected\. The **Status** for the invited accounts will change to **Enabled**\.

1. \(Recommended\) Repeat these steps in each AWS Region to ensure that your delegated administrator can manage findings for member accounts in all Regions\.

### Step 3 \- Automate the addition of new organization accounts as members<a name="guardduty_auto_enable_org_members"></a>

1. Log in to the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console using the delegated administrator account\.

1. In the navigation pane, under **Settings**, choose **Accounts**\.

1. Turn on Auto\-enable\.

1. Confirm your selection\.

1. \(Recommended\) Repeat these steps in each AWS Region to ensure that GuardDuty is automatically enabled on any new account, in every Region\.

When this setting is enabled, all new accounts that are created in, or added to, the organization are dded as a member accounts of the organization’s GuardDuty delegated administrator and GuardDuty is enabled in that Region\. When the number of member accounts reaches the limit of 5000, the Auto\-enable feature is automatically turned off\. If an account is removed and the total number of members decreases to fewer than 5000, the Auto\-enable feature turns back on\.\. 

## Designate a Delegated Administrator and add Member Accounts \(API\)<a name="organization_thru_api"></a>

 You can designate an Organizations delegated administrator and GuardDuty member accounts through the API operations\. Complete the following procedures to add a delegated administrator and member accounts in GuardDuty with organizations\.

**Important**  
You need to repeat these steps in each Region where you are using GuardDuty if you want to monitor all Regions for organization member accounts associated with the delegated administrator\.

****

1. Run the [enableOrganizationAdminAccount](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_enableOrganizationAdminAccount.html) API operation using the credentials of the AWS account of the Organizations master\.

    You must specify the account ID of the account you want to make a GuardDuty delegated administrator\.

   You can also use the AWS Command Line to do this by running the following CLI command\. Make sure to use a valid account ID\.

   ```
   aws guardduty enable-organization-admin-account —admin-account-id 11111111111
   ```
**Note**  
This command sets the delegated administrator for you current Region only\. If GuardDuty is not already enabled for that account in the current Region, it will be automatically enabled\.

    To set the delegated administrator for other Regions, you must specify the Regional endpoint for the Region you want your delegated administrator to manage\. For more information, see [GuardDuty endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/guardduty.html)\. The following example demonstrates how to set your endpoint to US West \(Oregon\)\. 

   ```
   aws guardduty enable-organization-admin-account —admin-account-id 11111111111 --endpoint guardduty.us-west-2.amazonaws.com
   ```

1.  Run the [CreateMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateMembers.html) API operation using the credentials of the AWS account you designated as the delegated administrator for GuardDuty in the previous step\.

    You must specify the detector ID of the delegated administrator AWS account and the account details, including account ID and email address, of the accounts that you want to become GuardDuty members\. You can create one or more members with this API operation\.

   You can also do this using AWS Command Line Tools by running the following CLI command\. Make sure to use your own valid detector ID, account ID, and email\. 

   ```
   aws guardduty create-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-details AccountId=123456789012,Email=guarddutymember@amazon.com
   ```

   You can view a list of all organization members using the [ListAccounts](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListAccounts.html) API operation or by running the following CLI command\.

   ```
   aws organizations list-accounts
   ```
**Note**  
 The detector ID is Regional\. To enable GuardDuty for organization members in other Regions, you must supply the unique detector ID of the delegated administrator for each Region\. 

1. Run the [updateOrganizationConfiguration](https://docs.aws.amazon.com/guardduty/latest/APIReference/updateOrganizationConfiguration.html) API operation using the credentials of the GuardDuty delegated administrator account to automatically enable GuardDuty in that Region for new member accounts\.

   You must specify the detector ID of the delegated administrator AWS account\.
**Note**  
 The detector ID is Regional, to automatically enable GuardDuty for new members in each Region, you must supply the unique detector ID of the delegated administrator for each Region\. 

   You can also do this using AWS Command Line Tools by running the following CLI command\. Make sure to use your own valid detector ID\. 

   ```
   aws guardduty update-organization-configuration --detector-id 12abc34d567e8fa901bc2d34e56789f0 --auto-enable 
   ```

   You can confirm that you have turned on the auto enable GuardDuty feature in a Region by running the [describeOrganizationConfiguration](https://docs.aws.amazon.com/guardduty/latest/APIReference/describeOrganizationConfiguration.html) API operation or by running the following CLI command using the detector ID of the delegated administrator in the desired Region\.

   ```
   aws guardduty describe-organization-configuration —detector-id 12abc34d567e8fa901bc2d34e56789f0 
   ```