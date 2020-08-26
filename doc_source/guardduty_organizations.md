# Managing GuardDuty accounts with AWS Organizations<a name="guardduty_organizations"></a>

When you use GuardDuty with an AWS Organizations organization, you can designate any account within the organization to be the GuardDuty delegated administrator\. Only the organization master account can designate GuardDuty delegated administrators\.

**Note**  
The Organization master can be the delegated administrator, but this is not recommended based on AWS Security best practices following the principle of least privilege\.

An account that is designated as a delegated administrator becomes a GuardDuty master account, has GuardDuty automatically enabled in the designated Region, and is granted permission to enable and manage GuardDuty for all accounts in the organization within that Region\. The other accounts in the organization can be viewed and added as GuardDuty member accounts associated with the master account\.

 If you have already set up a GuardDuty master with associated member accounts by invitation, and the member accounts are part of the same organization, their **Type** changes from **by Invitation** to **via Organizations** when you set a GuardDuty delegated administrator for your organization\. If the organization's GuardDuty master previously added members by invitation that are not part of the same organization, their **Type** is **by Invitation**\. In both cases, these previously added accounts are member accounts to the organization's GuardDuty delegated administrator\.

You can continue to add accounts as members even if they are outside of your organization\. To learn more, see [Designating master and member accounts through invitation \(console\)](guardduty_invitations.md#guardduty_become_console) and [Designating GuardDuty master and member accounts through invitation \(API\)](guardduty_invitations.md#guardduty_become_api)\.

**Note**  
There is a limit of 5000 member accounts per GuardDuty master account\. However, there could be more than 5000 accounts in your organization\. The number of **All** accounts in your organization is displayed on the **Accounts** page of the GuardDuty console\.  
If you exceed 5000 member accounts you will receive a notification through CloudWatch, Personal Health Dashboard, and in an email to the master account\.

Use the following procedures to register a GuardDuty delegated administrator for your organization, add existing organization accounts as members, and automate the addition of new organization accounts as GuardDuty member accounts\.

**Important**  
unlike AWS Organizations, GuardDuty is a Regional service\. This means that GuardDuty delegated administrators and member accounts must be added in each desired Region for account management through AWS Organizations to be active in each Region\. In other words, if the organization master designates a delegated administrator for GuardDuty in only US East \(N\. Virginia\) that delegated administrator will only manage member accounts added in that Region\. For more information on Regions in GuardDuty see [Regions and endpoints](guardduty_regions.md)\.

## Permissions required to designate a delegated administrator<a name="organizations_permissions"></a>

When delegating a GuardDuty master you must have permissions to the following actions:
+ organizations:EnableAWSServiceAccess
+ organizations:ListAWSServiceAccessForOrganization
+ organizations:RegisterDelegatedAdministrator
+ organizations:DescribeOrganization

You can add the following statement to the end of an existing GuardDuty policy to grant these permissions:

```
{
    "Sid": "Permissions to Enable GuardDuty Delegated Administrator",
    "Effect": "Allow",
    "Action": [
        "organizations:EnableAWSServiceAccess",
        "organizations:ListAWSServiceAccessForOrganization",
        "organizations:RegisterDelegatedAdministrator",
        "organizations:DescribeOrganization"
    ],
    "Resource": "*"
}
```

Additionally, if you wish to designate your AWS Organizations master account as the GuardDuty delegated administrator that entity will need `CreateServiceLinkedRole` permissions to initialize GuardDuty\. This can be added to an IAM policy using the following statement, replacing the account ID with the ID of your organization master:

```
{
	'Sid": "Permissions to Enable GuardDuty"
	"Effect": "Allow",
	"Action": [
		"iam:CreateServiceLinkedRole"
	],
	"Resource": "arn:aws:iam::123456789012:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty",
	"Condition": {
		"StringLike": {
			"iam:AWSServiceName": "guardduty.amazonaws.com"
		}
	}
}
```

**Note**  
If you're using GuardDuty in an manually\-enabled Region, replace the value for the "Service" with the service endpoint for the Region\. For example, if you're using GuardDuty in the Middle East \(Bahrain\) \(me\-south\-1\) Region, replace `"Service": "guardduty.amazonaws.com"` with `"Service": "guardduty.me-south-1.amazonaws.com"`\.

## Designate a delegated administrator and add member accounts \(console\)<a name="organization_thru_console"></a>

 Follow these steps to designate a GuardDuty delegated administrator and add member accounts using the GuardDuty console\.

### Step 1 \- register a GuardDuty delegated administrator for your organization<a name="guardduty_register_delegate_admin_proc"></a>

1. Log in to the AWS Management Console using the master account for your AWS Organizations organization\.

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

   Is GuardDuty already enabled in your account?
   + If GuardDuty is not already enabled, you can select **Get Started** and then designate a GuardDuty delegated administrator on the **Welcome to GuardDuty** page\.
   + If GuardDuty is enabled you can designate a GuardDuty delegated administrator on the **Settings** page\.

1. Enter the twelve\-digit AWS account ID of the account that you want to designate as the GuardDuty delegated administrator for the organization\.

1. Choose **Delegate**\. If GuardDuty is not already enabled, designating a delegated administrator will enable GuardDuty for that account in your current Region\.

1. \(Recommended\) Repeat the previous steps in each AWS Region\. It is recommended that you register the same delegated administrator in each Region\.

After you designate the delegated administrator, you only need to use the organization master account to change or remove the delegated administrator account\.

**Note**  
If you remove the delegated administrator, all associated member accounts are removed as GuardDuty members, but GuardDuty is not disabled in those accounts\.

### Step 2 \- add existing organization accounts as members<a name="guardduty_add_orgs_accounts"></a>

**Important**  
When you add an account as a member, GuardDuty is automatically enabled in that account in the current Region\. This behaviour differs from the invitation method, in which GuardDuty must be enabled prior to the account being added as a member\.

You must add your organization members in each Region to enable GuardDuty for those Regions\.

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation panel, choose **Settings**, and then choose **Accounts**\.

   The accounts table displays all of the accounts in the organization\. The **Type** for these accounts is **via organizations**\. The status of accounts that are not member accounts associated with the organization's GuardDuty delegated administrator is **Not a member**\.

1. Select the account or accounts that you want to add as members by checking the box next to the account ID\.
**Note**  
You can enable GuardDuty in the current Region for all organization accounts by selecting **enable** in the banner at the top of the page\. This action also triggers the *Auto\-Enable* feature that will enable GuardDuty in any future accounts added to your organization\.  
 Alternately, you can use the **filter** field to filter by **Relationship status: Not a member**, and then select every account that does not have GuardDuty enabled in the current Region\.

1. Choose **Actions** then choose **Add member**\.

1. Confirm that you want to add as members the number of accounts selected\. The **Status** for the invited accounts will change to **Enabled**\.

1. \(Recommended\) Repeat these steps in each AWS Region to ensure that your delegated administrator can manage findings for member accounts in all Regions\.

### Step 3 \- automate the addition of new organization accounts as members<a name="guardduty_auto_enable_org_members"></a>

1. Log in to the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console using the delegated administrator account\.

1. In the navigation pane, under **Settings**, choose **Accounts**\.

1. select Auto\-enable\.

1. Select the first toggle icon to turn auto\-enable on, if you wish to enable S3 Threat Detection for your new members in addition to enabling GuardDuty select the **S3 Protection** toggle icon, for more information see [Configuring S3 protection in multiple\-account environments](s3_detection.md#s3-multiaccount)\. When you have made updates choose **Update Settings**\.

1. \(Recommended\) Repeat these steps in each AWS Region to ensure that GuardDuty is automatically enabled on any new account, in every Region\.

When this setting is enabled, all new accounts that are created in, or added to, the organization are added as a member accounts of the organization's GuardDuty delegated administrator and GuardDuty is enabled in that Region\. When the number of member accounts reaches the limit of 5000, the Auto\-enable feature is automatically turned off\. If an account is removed and the total number of members decreases to fewer than 5000, the Auto\-enable feature turns back on\. 

## Designate a delegated administrator and add member accounts \(API\)<a name="organization_thru_api"></a>

 You can designate an Organizations delegated administrator and GuardDuty member accounts through the API operations\. Complete the following procedures to add a delegated administrator and member accounts in GuardDuty with organizations\.

****

1. Run the [enableOrganizationAdminAccount](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_EnableOrganizationAdminAccount.html) API operation using the credentials of the AWS account of the Organizations master\.

   You can also use the AWS Command Line to do this by running the following CLI command\. Make sure to specify the account ID of the account you want to make a GuardDuty delegated administrator\.

   ```
   aws guardduty enable-organization-admin-account —admin-account-id 11111111111
   ```

   This command sets the delegated administrator for your current Region only\. If GuardDuty is not already enabled for that account in the current Region, it will be automatically enabled\.

    To set the delegated administrator for other Regions, you must specify the Regional endpoint for the Region you want your delegated administrator to manage\. For more information, see [GuardDuty endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/guardduty.html)\. The following example demonstrates how to set your endpoint to US West \(Oregon\)\. 

   ```
   aws guardduty enable-organization-admin-account —admin-account-id 11111111111 --endpoint-url guardduty.us-west-2.amazonaws.com
   ```

1.  Run the [CreateMembers](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateMembers.html) API operation using the credentials of the AWS account you designated as the delegated administrator for GuardDuty in the previous step\.

    You must specify the regional detector ID of the delegated administrator AWS account and the account details, including the account IDs and email addresses, of the accounts that you want to become GuardDuty members\. You can create one or more members with this API operation\.
**Important**  
Accounts added as members will have GuardDuty enabled in that region, with the exception of the organization master account, which must first enable GuardDuty before it can be added as a member account\.

   You can also do this using AWS Command Line Tools by running the following CLI command\. Make sure to use your own valid detector ID, account ID, and email\. 

   ```
   aws guardduty create-members --detector-id 12abc34d567e8fa901bc2d34e56789f0 --account-details AccountId=123456789012,Email=guarddutymember@amazon.com
   ```

   You can view a list of all organization members using the [ListAccounts](https://docs.aws.amazon.com/organizations/latest/APIReference/API_ListAccounts.html) API operation or by running the following CLI command\.

   ```
   aws organizations list-accounts
   ```

1. Run the [updateOrganizationConfiguration](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_UpdateOrganizationConfiguration.html) API operation using the credentials of the GuardDuty delegated administrator account to automatically enable GuardDuty in that Region for new member accounts\.

   You must specify the detector ID of the delegated administrator AWS account\.

   You can also do this using AWS Command Line Tools by running the following CLI command\. Make sure to use your own valid detector ID\. 

   ```
   aws guardduty update-organization-configuration --detector-id 12abc34d567e8fa901bc2d34e56789f0 --auto-enable 
   ```

   You can confirm that you have turned on the auto enable GuardDuty feature in a Region by running the [describeOrganizationConfiguration](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_DescribeOrganizationConfiguration.html) API operation or by running the following CLI command using the detector ID of the delegated administrator in the desired Region\.

   ```
   aws guardduty describe-organization-configuration —detector-id 12abc34d567e8fa901bc2d34e56789f0 
   ```

1. \(Recommended\) Repeat these steps in each Region using your unique detector ID for that Region to enable GuardDuty monitoring coverage for all members in all AWS Regions\.

## Consolidating GuardDuty master accounts under a single organization delegated administrator<a name="consolidate-orgs"></a>

GuardDuty recommends using association through AWS Organizations to manage member accounts under a master account\. You can use the example process outlined below to consolidate master and member associated by invitation under a single organization master\.

1. Ensure all accounts you wish to manage GuardDuty for are part of your organization\. For information on adding account to your organization see [Inviting an AWS account to join your organization ](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_accounts_invites.html)\. 

1. Disassociate all member accounts from pre\-existing master accounts, except those under the account you wish to designate as the GuardDuty delegated administrator for the organization\.
**Note**  
Accounts already being managed by a GuardDuty master or master accounts with active members cannot be added to a different GuardDuty master account\. Each organization can have only one GuardDuty master account per region, and each member account can have only one master\.

1. Designate a GuardDuty delegated administrator for the organization from the **Settings** page\.

1. Log in to the designated delegated admin account\.

1. Proceed to add members from the organization\.
**Important**  
Remember that GuardDuty is a regional service\. It is recommended that you designate your master account and add all your members in every region to maximize the effectiveness of GuardDuty
