# AWS managed policies for Amazon GuardDuty<a name="security-iam-awsmanpol"></a>

To add permissions to users, groups, and roles, it is easier to use AWS managed policies than to write policies yourself\. It takes time and expertise to [create IAM customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create-console.html) that provide your team with only the permissions they need\. To get started quickly, you can use our AWS managed policies\. These policies cover common use cases and are available in your AWS account\. For more information about AWS managed policies, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

AWS services maintain and update AWS managed policies\. You can't change the permissions in AWS managed policies\. Services occasionally add additional permissions to an AWS managed policy to support new features\. This type of update affects all identities \(users, groups, and roles\) where the policy is attached\. Services are most likely to update an AWS managed policy when a new feature is launched or when new operations become available\. Services do not remove permissions from an AWS managed policy, so policy updates won't break your existing permissions\.

Additionally, AWS supports managed policies for job functions that span multiple services\. For example, the **ReadOnlyAccess** AWS managed policy provides read\-only access to all AWS services and resources\. When a service launches a new feature, AWS adds read\-only permissions for new operations and resources\. For a list and descriptions of job function policies, see [AWS managed policies for job functions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html) in the *IAM User Guide*\.

## <a name="w282aac27c25c11"></a>

## AWS managed policy: AmazonGuardDutyFullAccess<a name="security-iam-awsmanpol-AmazonGuardDutyFullAccess"></a>

You can attach the `AmazonGuardDutyFullAccess` policy to your IAM identities\.

This policy grants administrative permissions that allow a user full access to all GuardDuty actions\.

**Permissions details**

This policy includes the following permissions\.




+ `GuardDuty` – Allows users full access to all GuardDuty actions\.
+ `IAM` – Allows users to create the GuardDuty service\-linked role\. This allows a GuardDuty administrator to enable GuardDuty for member accounts\.
+ `Organizations` – Allows users to designate a delegated administrator and manage members for a GuardDuty organization\.



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
        },
        {
            "Effect": "Allow",
            "Action": [
                "organizations:EnableAWSServiceAccess",
                "organizations:RegisterDelegatedAdministrator",
                "organizations:ListDelegatedAdministrators",
                "organizations:ListAWSServiceAccessForOrganization",
                "organizations:DescribeOrganizationalUnit",
                "organizations:DescribeAccount",
                "organizations:DescribeOrganization"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AmazonGuardDutyReadOnlyAccess<a name="security-iam-awsmanpol-AmazonGuardDutyReadOnlyAccess"></a>

You can attach the `AmazonGuardDutyReadOnlyAccess` policy to your IAM identities\.

This policy grants read\-only permissions that allow a user to view GuardDuty findings and details of your GuardDuty organization\.

**Permissions details**

This policy includes the following permissions\.




+ `GuardDuty` – Allows users to view GuardDuty findings and perform API operations that start with `Get`, `List`, or `Describe`\.
+ `Organizations` – Allows users to retrieve information about your GuardDuty organization configuration, including details of the delegated administrator account\.



```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "guardduty:Describe*",
                "guardduty:Get*",
                "guardduty:List*"
            ],
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "organizations:ListDelegatedAdministrators",
                "organizations:ListAWSServiceAccessForOrganization",
                "organizations:DescribeOrganizationalUnit",
                "organizations:DescribeAccount",
                "organizations:DescribeOrganization"
            ],
            "Resource": "*"
        }
    ]
}
```

## AWS managed policy: AWSServiceRoleForAmazonGuardDuty<a name="security-iam-awsmanpol-AWSServiceRoleForAmazonGuardDuty"></a>

You can't attach AWSServiceRoleForAmazonGuardDuty to your IAM entities\. This AWS managed policy is attached to a service\-linked role that allows GuardDuty to perform actions on your behalf\. For more information, see [ Using service\-linked roles for Amazon GuardDutyUsing service\-linked roles  How to use service\-linked roles to give Amazon GuardDuty access to resources in your AWS account\.   Amazon GuardDuty uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to GuardDuty\. Service\-linked roles are predefined by GuardDuty and include all the permissions that GuardDuty requires to call other AWS services on your behalf\.  A service\-linked role makes setting up GuardDuty easier because you don't have to manually add the necessary permissions\. GuardDuty defines the permissions of its service\-linked role, and unless the permissions are defined otherwise, only GuardDuty can assume the role\. The defined permissions include the trust policy and the permissions policy, and that permissions policy can't be attached to any other IAM entity\. GuardDuty supports using service\-linked roles in all of the Regions where GuardDuty is available\. For more information, see [Regions and endpoints](guardduty_regions.md)\. You can delete the GuardDuty service\-linked role only after first disabling GuardDuty in all Regions where it is enabled\. This protects your GuardDuty resources because you can't inadvertently remove permission to access them\. For information about other services that support service\-linked roles, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) in the *IAM User Guide* and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.  Service\-linked role permissions for GuardDuty  GuardDuty uses the service\-linked role named `AWSServiceRoleForAmazonGuardDuty`\. This service\-linked role allows GuardDuty to retrieve metadata for the EC2 instances in your AWS environment that are involved in potentially suspicious activity\. It also allows GuardDuty to include the retrieved EC2 instance metadata in the findings that GuardDuty generates about potentially suspicious activity\. The `AWSServiceRoleForAmazonGuardDuty` service\-linked role trusts the `guardduty.amazonaws.com` service to assume the role\. The permissions policy for the role allows GuardDuty to perform tasks such as:   Use Amazon EC2 actions to retrieve information about your EC2 instances and images\. Use Amazon EC2 actions to retrieve information about your EC2 networking components such as VPCs, subnets, and transit gateways\. Use Amazon S3 actions to retrieve information about S3 buckets and objects\. Use AWS Organizations actions to describe associated accounts\.  The role is configured with the following [AWS managed policy](https://docs.aws.amazon.com/guardduty/latest/ug/security-iam-awsmanpol), named `AWSServiceRoleForAmazonGuardDuty`\. 

```
        {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:DescribeImages",
        "ec2:DescribeVpcEndpoints",
        "ec2:DescribeSubnets",
        "ec2:DescribeVpcPeeringConnections",
        "ec2:DescribeTransitGatewayAttachments"
        "organizations:ListAccounts",
        "organizations:DescribeAccount",
        "s3:GetBucketPublicAccessBlock",
        "s3:GetEncryptionConfiguration",
        "s3:GetBucketTagging",
        "s3:GetAccountPublicAccessBlock",
        "s3:ListAllMyBuckets",
        "s3:GetBucketAcl",
        "s3:GetBucketPolicy",
        "s3:GetBucketPolicyStatus",
      ],
      "Resource": "*"
    }
  ]
}
``` The following is the trust policy that is attached to the `AWSServiceRoleForAmazonGuardDuty` service\-linked role: 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "guardduty.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```   Creating a service\-linked role for GuardDuty  The `AWSServiceRoleForAmazonGuardDuty` service\-linked role is automatically created when you enable GuardDuty for the first time or enable GuardDuty in a supported Region where you previously didn't have it enabled\. You can also create the `AWSServiceRoleForAmazonGuardDuty` service\-linked role manually using the IAM console, the IAM CLI, or the IAM API\.   The service\-linked role that is created for the GuardDuty delegated administrator account doesn't apply to the member GuardDuty accounts\.  You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For the `AWSServiceRoleForAmazonGuardDuty` service\-linked role to be successfully created, the IAM identity that you use GuardDuty with must have the required permissions\. To grant the required permissions, attach the following policy to this IAM user, group, or role:   Replace the sample account ID in the example below with your actual AWS account ID\.  

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
``` For more information about creating the role manually, see [Creating a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\.   Editing a service\-linked role for GuardDuty  GuardDuty doesn't allow you to edit the `AWSServiceRoleForAmazonGuardDuty` service\-linked role\. After you create a service\-linked role, you can't change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.   Deleting a service\-linked role for GuardDuty  If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don't have an unused entity that isn't actively monitored or maintained\.   You must first disable GuardDuty in all Regions where it is enabled in order to delete the `AWSServiceRoleForAmazonGuardDuty`\. If the GuardDuty service isn't disabled when you try to delete the service\-linked role, the deletion fails\. For more information, see [Suspending or disabling GuardDuty](guardduty_suspend-disable.md)\.  When you disable GuardDuty, the `AWSServiceRoleForAmazonGuardDuty` is NOT automatically deleted\. If you then enable GuardDuty again, it'll start using the existing `AWSServiceRoleForAmazonGuardDuty`\. **To manually delete the service\-linked role using IAM** Use the IAM console, the IAM CLI, or the IAM API to delete the `AWSServiceRoleForAmazonGuardDuty` service\-linked role\. For more information, see [Deleting a service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.  ](using-service-linked-roles.md#using-service-linked-roles.title)\. 

## GuardDuty updates to AWS managed policies<a name="security-iam-awsmanpol-updates"></a>



View details about updates to AWS managed policies for GuardDuty since this service began tracking these changes\. For automatic alerts about changes to this page, subscribe to the RSS feed on the GuardDuty Document history page\.




| Change | Description | Date | 
| --- | --- | --- | 
|  [AWSServiceRoleForAmazonGuardDuty](using-service-linked-roles.md#slr-permissions) – Update to an existing policy  |  GuardDuty added new permissions to allow GuardDuty to use Amazon EC2 networking actions to improve findings\. GuardDuty can now perform the following EC2 actions to gain information about how your EC2 instances are communicating\. This information is used to improve finding accuracy\. [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/security-iam-awsmanpol.html)  | Aug 3, 2021 | 
|  GuardDuty started tracking changes  |  GuardDuty started tracking changes for its AWS managed policies\.  | Aug 3, 2021 | 
