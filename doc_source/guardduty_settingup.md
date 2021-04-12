# Getting started with GuardDuty<a name="guardduty_settingup"></a>

This tutorial provides a hands\-on introduction to GuardDuty\. The minimum requirements for enabling GuardDuty as a standalone account or as a GuardDuty administrator with AWS Organizations are covered in Step 1\. Steps 2 through 5 cover using additional features recommended by GuardDuty to get the most out of your findings\.

**Topics**
+ [Before you begin](#setup-before)
+ [Step 1: Enable Amazon GuardDuty](#guardduty_enable-gd)
+ [Step 2: Generate sample findings and explore basic operations](#startup-samples)
+ [Step 3: Configure GuardDuty findings export to an S3 bucket](#setup-export)
+ [Step 4: Set up GuardDuty finding alerts through SNS](#setup-sns)
+ [Next steps](#setup_beyond)

## Before you begin<a name="setup-before"></a>

GuardDuty is a monitoring service that analyzes AWS CloudTrail management and Amazon S3 data events, VPC flow logs, and DNS logs to generate security findings for your account\. Once GuardDuty is enabled, it starts monitoring your environment immediately\. GuardDuty can be disabled at any time to stop it from processing all AWS CloudTrail events, VPC Flow Logs, and DNS logs\.

**Note the following about enabling GuardDuty**:
+ GuardDuty is a Regional service, meaning any of the configuration procedures you follow on this page must be repeated in each region that you want to monitor with GuardDuty\.

  We highly recommend that you enable GuardDuty in all supported AWS Regions\. This enables GuardDuty to generate findings about unauthorized or unusual activity even in Regions that you are not actively using\. This also enables GuardDuty to monitor AWS CloudTrail events for global AWS services such as IAM\. If GuardDuty is not enabled in all supported Regions, its ability to detect activity that involves global services is reduced\. For a full list of regions in which GuardDuty is supported see [Regions and endpoints](guardduty_regions.md)\.
+ Any user with administrator privileges in an AWS Account can enable GuardDuty, however, following the security best practice of least privilege, it is recommended that you create an IAM user, role, or group to manage GuardDuty specifically\. For information on the permissions required to enable GuardDuty see [Permissions required to enable GuardDuty](guardduty_managing_access.md#guardduty_enable-permissions)\.
+ When you enable GuardDuty for the first time in any region, it creates a service\-linked role for your account called `AWSServiceRoleForAmazonGuardDuty`\. This role includes the permissions and the trust policies that allow GuardDuty to consume and analyze events directly from AWS CloudTrail, VPC Flow logs, and DNS logs in order to generate security findings\. For more information, see [Using a service\-linked role to delegate permissions to GuardDuty](guardduty_managing_access.md#guardduty_service-access)\. For more information about service\-linked roles, see [Using service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\.
+ When you enable GuardDuty for the first time in any Region your AWS account is automatically enrolled in a 30\-day GuardDuty free trial for that Region\.

## Step 1: Enable Amazon GuardDuty<a name="guardduty_enable-gd"></a>

The first step to using GuardDuty is to enable it in your account, Once enabled, GuardDuty will immediately begin to monitor for security threats in the current region\.

If you want to manage GuardDuty findings for other accounts within your organization as a GuardDuty administrator, you must add member accounts and enable GuardDuty for them as well\. Choose an option to learn how to enable GuardDuty for your environment\.

------
#### [ Standalone account environment ]

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)

1. Choose **Get Started**\.

1. Choose **Enable GuardDuty**\.

------
#### [ Multi\-account environment ]

**Important**  
As prerequisites for this process, you must be in the same organization as all the accounts you wish to manage, and have access to the AWS Organizations management account in order to delegate an administrator for GuardDuty within your organization\. Additional permissions may be required to delegate an administrator, for more info see [Permissions required to designate a delegated administrator](guardduty_organizations.md#organizations_permissions)\. 

 **To delegate an Administrator for GuardDuty** 

1. Log in to the AWS Organizations management account

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

   Is GuardDuty already enabled in your account?
   + If GuardDuty is not already enabled, you can select **Get Started** and then designate a GuardDuty delegated administrator on the **Welcome to GuardDuty** page\.
   + If GuardDuty is enabled, you can designate a GuardDuty delegated administrator on the **Settings** page\.

1. Enter the twelve\-digit AWS account ID of the account that you want to designate as the GuardDuty delegated administrator for the organization and choose **Delegate**\. 
**Note**  
If GuardDuty is not already enabled, designating a delegated administrator will enable GuardDuty for that account in your current Region\.

 **To add member accounts** 

This procedure covers adding members accounts to a GuardDuty delegated administrator account through AWS Organizations\. There is also the option to add members by invitation\. To learn more about both methods for associating members in GuardDuty see [Managing multiple accounts in Amazon GuardDutyAWS Service Integrations with GuardDuty](guardduty_accounts.md)\.

1. Log in to the delegated administrator account

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/)\.

1. In the navigation panel, choose **Settings**, and then choose **Accounts**\.

   The accounts table displays all of the accounts in the organization\.

1. Choose the accounts that you want to add as members by selecting the box next to the account ID\. Then from the **Action** menu select **Add member**\.
**Tip**  
You can automate adding new accounts as members by turning on the **Auto\-enable** feature, however, this only applies to accounts that join your organization after the feature has been enabled\.

------

## Step 2: Generate sample findings and explore basic operations<a name="startup-samples"></a>

When GuardDuty discovers a security issue it generates a finding\. A GuardDuty finding is a data set containing details relating to that unique security issue\. The finding's details can be used to help you investigate the issue\.

GuardDuty supports generating sample findings with placeholder values, which can be used to test GuardDuty functionality and familiarize yourself with findings before needing to respond to a real security issue discovered by GuardDuty\. Follow the guide below to generate sample findings for each finding type available in GuardDuty, for additional ways to generate sample findings, including generating a simulated security event within your account, see [Sample findings](sample_findings.md)\.

**To create and explore sample findings**

1. In the navigation pane, choose **Settings**\.

1. On the **Settings** page, under **Sample findings**, choose **Generate sample findings**\.

1. In the navigation pane, choose **Findings**\. The sample findings are displayed on the **Current findings** page with the prefix **\[SAMPLE\]**\.

1. Select a finding from the list to display details for the finding\.

   1. You can review the different information fields available in the finding details pane\. Different types of findings can have different fields\. For more information on the available fields across all finding types see [Finding details](guardduty_findings-summary.md)\. From the details pane you can take the following actions: 
     + Select the **finding ID** at the top of the pane to open the complete JSON details for the finding\. The complete JSON file can also be downloaded from this panel\. The JSON contains some additional information not included in the console view and is the format that can be ingested by other tools and services\.
     + View the **Resource affected** section\. In a real finding the information here will help you identify a resource in your account that should be investigated and will include links to the appropriate AWS console for actionable resources\.
     + Select the \+ or \- looking glass icons to create an inclusive or exclusive filter for that detail\. For more information on finding filters see [Filtering findings](guardduty_filter-findings.md)

1. Archive all your sample findings

   1. Select all findings by selection the check box at the top of the list\.

   1. Deselect any findings you wish to keep\.

   1. Select the **Actions** menu and then select **Archive** to hide the sample findings\.
**Note**  
To view the archived findings select **Current** and then **Archived** to switch the findings view\.

## Step 3: Configure GuardDuty findings export to an S3 bucket<a name="setup-export"></a>

GuardDuty recommends setting up findings export, which allows you to export your findings to an S3 bucket for indefinite storage beyond the GuardDuty 90 day storage limit\. This allows you to keep records of findings or track issues within your environment over time\. The process outlined here walks you through setting up a new S3 bucket and creating a new KMS key to encrypt findings from within the console, for more information about this, including how to use your own existing bucket or a bucket in another account, see [Exporting findings](guardduty_exportfindings.md)\.

 **To configure S3 export** 

1. In the navigation pane, choose **Settings**\.

1. Under **Findings export options** select **Configure now**\.

1. Select **New bucket**\.

   1. Enter a unique name for your bucket\.

1. To encrypt findings, you will need a KMS key with a policy that allows GuardDuty to use it\. You can attach the policy outlined in the following section to an existing key or create a new KMS key from the console\. The key must be in the same Region as your S3 bucket\. For more information on KMS keys see [create a key](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\. 

   To create a new key, Select **Go to KMS console to create a new key** to open the KMS console in a new tab and follow these instructions:

   1.  In the KMS console select **Create key**\. 

   1.  Choose **Symmetric** then choose **Next**\. 

   1. Give your key an alias and choose **Next**\.

   1. Choose **Next** and then **Next** again to accept the default administration and usage permissions\.

   1. In the **Review and edit key policy** pane add the following statement to the `"Statements":` section\. When editing the key policy make sure your JSON syntax is valid, each statement must be separated by a comma, for more information on writing policies with JSON see [Overview of JSON policies](IAM/latest/UserGuide/access_policies.html#access_policies-json>)\.

      ```
      {
          "Sid": "Allow GuardDuty to use the key",
          "Effect": "Allow",
          "Principal": {
              "Service": "guardduty.amazonaws.com"
                  },
                  "Action": "kms:GenerateDataKey",
                  "Resource": "*"
      }
      ```

1. Return to the GuardDuty console tab where you were configuring findings export\.

   1. Refresh the console by selecting the Refresh icon next to **S3 bucket**, now choose the key you just created from the **Key alias** list then choose **Save**\.

1. \(Optional\) you can test your new export settings by generating sample findings with the process in Step 2\. The new sample findings will appear within 5 minutes as entries in the S3 bucket created by GuardDuty in step 3\. 

## Step 4: Set up GuardDuty finding alerts through SNS<a name="setup-sns"></a>

GuardDuty integrates with Amazon EventBridge which can be used to send findings data to other applications and services for processing\. With EventBridge you can use GuardDuty findings to trigger automatic responses to your findings by connecting finding events to targets such as AWS Lambda functions, Amazon EC2 Systems Manager automation, Amazon Simple Notification Service \(SNS\) and more\.

In this example you will create an SNS topic to be the target of an EventBridge rule, then you'll use EventBridge to create a rule that captures findings data from GuardDuty\. The resulting rule forwards the finding details to an email address\. To learn how you can send findings to Slack or Chime, as well as modify the types of findings alerts are sent for, see [Setup an Amazon SNS topic and endpoint](guardduty_findings_cloudwatch.md#SNS_setup)\.

**To create an SNS topic for your findings alerts**

1. Sign in to the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Select **Topics** from the navigation pane and then **Create Topic**\.

1. In the Create topic section, select **Standard**\. Next, enter a Topic name, for example **GuardDuty**\. Other details are optional\.

1. Choose **Create Topic**\. The Topic details for your new topic will open\.

1. In the Subscriptions section select **Create Subscription**\.

1. From the **Protocol** menu, select **Email**\.

   1. In the **Endpoint** field add the email address you would like to receive notifications at\. You will be required to confirm your subscription through your email client after creating it\.

   1. Choose **Create Subscription**\.

1. Check for a subscription message in your inbox and choose **Confirm Subscription**\.
**Note**  
You can check email confirmation status by selecting the subscription name from the **Topics** list in the SNS console\.

**To create an EventBridge rule to capture GuardDuty findings and format them**

1. Open the EventBridge console at [https://console\.aws\.amazon\.com/events/](https://console.aws.amazon.com/eventsy/)\.

1. Select **Rules** from the navigation pane and then **Create Rule**\.

   1. Choose **Event Pattern** and then **Pre\-defined pattern by service**\.

   1. From the **Service provider** menu, choose **AWS**\.

   1. From the **Service name** menu, choose **GuardDuty**\.

   1. From the **Event Type** menu, choose **GuardDuty Finding**\.

1. In the **Select targets** pane, from the **Target** menu, choose **SNS Topic**\.

1. For **Topic** select the name of the SNS topic you created earlier\.

1. Expand **Configure Input** and Choose **Input transformer**\. The Input transformer code will allow you to format the JSON finding data sent from GuardDuty into an easy human\-readable message\.

1. Copy the following code and paste it into the **Input Path** field\.

   ```
   {
       "severity": "$.detail.severity",
       "Finding_ID": "$.detail.id",
       "Finding_Type": "$.detail.type",
       "region": "$.region",
       "Finding_description": "$.detail.description"
   }
   ```

1. Copy the following code and paste it into the **Input Template** field to format the email\.

   ```
   "You have a severity <severity> GuardDuty finding type <Finding_Type> in the <region> region."
   "Finding Description:"
   "<Finding_description>. "
   "For more details open the GuardDuty console at https://console.aws.amazon.com/guardduty/home?region=<region>#/findings?search=id%3D<Finding_ID>"
   ```

1. Choose **Create** to finalize your rule\.

1. \(Optional\) you can test your new rule by generating sample findings with the process in Step 2\. You will receive an email for each sample finding generated\.

## Next steps<a name="setup_beyond"></a>

As you continue to use GuardDuty, you will come to understand the types of findings that are relevant to your environment\. Whenever you receive a new finding, you can find information, including remediation recommendations about that finding, by selecting **Learn more** from the finding description in the finding details pane, or by searching for the finding name on the [Finding types](guardduty_finding-types-active.md) page\.

The following features will help you tune GuardDuty so that it can provide the most relevant findings for your AWS environment:
+ To easily sort findings based on specific criteria, such as instance ID, account ID, S3 bucket name, and more, you can create and save filters within GuardDuty\. For more information see [Filtering findings](guardduty_filter-findings.md)\.
+ If you are receiving findings for expected behavior in your environment, you can automatically archive findings based on criteria you define with [suppression rules](findings_suppression-rule.md)\.
+ To prevent findings from being generated from a subset of trusted IPs, or to have GuardDuty monitor IPs outside it's normal monitoring scope you can set up [Trusted IP and threat lists](guardduty_upload-lists.md)\.
