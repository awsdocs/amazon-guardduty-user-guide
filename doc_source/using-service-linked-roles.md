# Using service\-linked roles for Amazon GuardDuty<a name="using-service-linked-roles"></a>

Amazon GuardDuty uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to GuardDuty\. Service\-linked roles are predefined by GuardDuty and include all the permissions that GuardDuty requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up GuardDuty easier because you don't have to manually add the necessary permissions\. GuardDuty defines the permissions of its service\-linked role, and unless the permissions are defined otherwise, only GuardDuty can assume the role\. The defined permissions include the trust policy and the permissions policy, and that permissions policy can't be attached to any other IAM entity\.

GuardDuty supports using service\-linked roles in all of the Regions where GuardDuty is available\. For more information, see [Regions and endpoints](guardduty_regions.md)\.

You can delete the GuardDuty service\-linked role only after first disabling GuardDuty in all Regions where it is enabled\. This protects your GuardDuty resources because you can't inadvertently remove permission to access them\.

For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide* and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for GuardDuty<a name="slr-permissions"></a>

GuardDuty uses the service\-linked role named `AWSServiceRoleForAmazonGuardDuty`\. This service\-linked role allows GuardDuty to retrieve metadata for the EC2 instances in your AWS environment that are involved in potentially suspicious activity\. It also allows GuardDuty to include the retrieved EC2 instance metadata in the findings that GuardDuty generates about potentially suspicious activity\.

The `AWSServiceRoleForAmazonGuardDuty` service\-linked role trusts the following services to assume the role:
+ `guardduty.amazonaws.com`

The role permissions policy allows GuardDuty to complete the following actions on the specified resources:
+ Action: `ec2:DescribeInstances` 
+ Action: `ec2:DescribeImages` 
+ Action: `organizations:ListAccounts` 
+ Action: `organizations:DescribeAccount` 
+ Resources: `arn:aws:iam::*:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty`

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For the `AWSServiceRoleForAmazonGuardDuty` service\-linked role to be successfully created, the IAM identity that you use GuardDuty with must have the required permissions\. To grant the required permissions, attach the following policy to this IAM user, group, or role: 

**Note**  
Replace the sample account ID in the example below with your actual AWS account ID\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "guardduty:*"
            ],
            "Resource": "*"
        },
        {
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
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:PutRolePolicy",
                "iam:DeleteRolePolicy"
            ],
            "Resource": "arn:aws:iam::1234567890123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
        }
    ]
}
```

## Creating a service\-linked role for GuardDuty<a name="create-slr"></a>

The `AWSServiceRoleForAmazonGuardDuty` service\-linked role is automatically created when you enable GuardDuty for the first time or enable GuardDuty in a supported Region where you previously didn't have it enabled\. You can also create the `AWSServiceRoleForAmazonGuardDuty` service\-linked role manually using the IAM console, the IAM CLI, or the IAM API\. 

**Important**  
The service\-linked role that is created for the master GuardDuty account doesn't apply to the member GuardDuty accounts\.

For more information about creating the role manually, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\.

## Editing a service\-linked role for GuardDuty<a name="edit-slr"></a>

GuardDuty doesn't allow you to edit the `AWSServiceRoleForAmazonGuardDuty` service\-linked role\. After you create a service\-linked role, you can't change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a service\-linked role for GuardDuty<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don't have an unused entity that isn't actively monitored or maintained\. 

**Important**  
You must first disable GuardDuty in all Regions where it is enabled in order to delete the `AWSServiceRoleForAmazonGuardDuty`\.  
If the GuardDuty service isn't disabled when you try to delete the service\-linked role, the deletion fails\. For more information, see [Suspending or disabling GuardDuty](guardduty_suspend-disable.md)\.

When you disable GuardDuty, the `AWSServiceRoleForAmazonGuardDuty` is NOT automatically deleted\. If you then enable GuardDuty again, it'll start using the existing `AWSServiceRoleForAmazonGuardDuty`\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the IAM CLI, or the IAM API to delete the `AWSServiceRoleForAmazonGuardDuty` service\-linked role\. For more information, see [Deleting a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.