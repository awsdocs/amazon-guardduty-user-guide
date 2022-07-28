# Identity\-based policy examples for AWS GuardDuty<a name="security_iam_id-based-policy-examples"></a>

By default, IAM users and roles don't have permission to create or modify GuardDuty resources\. They also can't perform tasks using the AWS Management Console, AWS CLI, or AWS API\. An IAM administrator must create IAM policies that grant users and roles permission to perform actions on the resources that they need\. The administrator must then attach those policies to the IAM users or groups that require those permissions\.

To learn how to create an IAM identity\-based policy using these example JSON policy documents, see [Creating policies on the JSON tab](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html#access_policies_create-json-editor) in the *IAM User Guide*\.

**Topics**
+ [Policy best practices](#security_iam_service-with-iam-policy-best-practices)
+ [Using the GuardDuty console](#security_iam_id-based-policy-examples-console)
+ [Permissions required to enable GuardDuty](#guardduty_enable-permissions)
+ [Allow users to view their own permissions](#security_iam_id-based-policy-examples-view-own-permissions)
+ [Custom IAM policy to grant read\-only access to GuardDuty](#security_iam_id-based-policy-examples-custom-readonly)
+ [Deny Access to GuardDuty findings](#security_iam_id-based-policy-examples-deny-findings)
+ [Using a custom IAM policy to limit access to GuardDuty resources](#security_iam_id-based-policy-examples-guardduty_restrict_access_to_resources)

## Policy best practices<a name="security_iam_service-with-iam-policy-best-practices"></a>

Identity\-based policies are very powerful\. They determine whether someone can create, access, or delete GuardDuty resources in your account\. These actions can incur costs for your AWS account\. When you create or edit identity\-based policies, follow these guidelines and recommendations:
+ **Get started using AWS managed policies** – To start using GuardDuty quickly, use AWS managed policies to give your employees the permissions they need\. These policies are already available in your account and are maintained and updated by AWS\. For more information, see [Get started using permissions with AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-use-aws-defined-policies) in the *IAM User Guide*\.
+ **Grant least privilege** – When you create custom policies, grant only the permissions required to perform a task\. Start with a minimum set of permissions and grant additional permissions as necessary\. Doing so is more secure than starting with permissions that are too lenient and then trying to tighten them later\. For more information, see [Grant least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) in the *IAM User Guide*\.
+ **Enable MFA for sensitive operations** – For extra security, require IAM users to use multi\-factor authentication \(MFA\) to access sensitive resources or API operations\. For more information, see [Using multi\-factor authentication \(MFA\) in AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) in the *IAM User Guide*\.
+ **Use policy conditions for extra security** – To the extent that it's practical, define the conditions under which your identity\-based policies allow access to a resource\. For example, you can write conditions to specify a range of allowable IP addresses that a request must come from\. You can also write conditions to allow requests only within a specified date or time range, or to require the use of SSL or MFA\. For more information, see [IAM JSON policy elements: Condition](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition.html) in the *IAM User Guide*\.

## Using the GuardDuty console<a name="security_iam_id-based-policy-examples-console"></a>

To access the AWS GuardDuty console, you must have a minimum set of permissions\. These permissions must allow you to list and view details about the GuardDuty resources in your AWS account\. If you create an identity\-based policy that is more restrictive than the minimum required permissions, the console won't function as intended for entities \(IAM users or roles\) with that policy\.

You don't need to allow minimum console permissions for users that are making calls only to the AWS CLI or the AWS API\. Instead, allow access to only the actions that match the API operation that you're trying to perform\.

To ensure that users and roles can still use the GuardDuty console, also attach the GuardDuty `ConsoleAccess` or `ReadOnly` AWS managed policy to the entities\. For more information, see [Adding permissions to a user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_change-permissions.html#users_change_permissions-add-console) in the *IAM User Guide*\.

## Permissions required to enable GuardDuty<a name="guardduty_enable-permissions"></a>

This section describes the permissions that various IAM identities \(users, groups, and roles\) must have in order to initially enable GuardDuty either through the console or programmatically \(using the GuardDuty API or the GuardDuty commands in the AWS CLI\)\. 

To grant permissions required to enable GuardDuty, attach the following policy to an IAM user, group, or role:

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
            "Resource": [
                "arn:aws:iam::123456789012:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty",
                "arn:aws:iam::123456789012:role/aws-service-role/malware-protection.guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDutyMalwareProtection"
            ],
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": [
                        "guardduty.amazonaws.com",
                        "malware-protection.guardduty.amazonaws.com"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:PutRolePolicy",
                "iam:DeleteRolePolicy"
            ],
            "Resource": [
                "arn:aws:iam::123456789012:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty",
                "arn:aws:iam::123456789012:role/aws-service-role/malware-protection.guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDutyMalwareProtection"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:GetRole"
            ],
            "Resource": "arn:aws:iam::123456789012:role/aws-service-role/malware-protection.guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDutyMalwareProtection"
        }
    ]
}
```

## Allow users to view their own permissions<a name="security_iam_id-based-policy-examples-view-own-permissions"></a>

This example shows how you might create a policy that allows IAM users to view the inline and managed policies that are attached to their user identity\. This policy includes permissions to complete this action on the console or programmatically using the AWS CLI or AWS API\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ViewOwnUserInfo",
            "Effect": "Allow",
            "Action": [
                "iam:GetUserPolicy",
                "iam:ListGroupsForUser",
                "iam:ListAttachedUserPolicies",
                "iam:ListUserPolicies",
                "iam:GetUser"
            ],
            "Resource": ["arn:aws:iam::*:user/${aws:username}"]
        },
        {
            "Sid": "NavigateInConsole",
            "Effect": "Allow",
            "Action": [
                "iam:GetGroupPolicy",
                "iam:GetPolicyVersion",
                "iam:GetPolicy",
                "iam:ListAttachedGroupPolicies",
                "iam:ListGroupPolicies",
                "iam:ListPolicyVersions",
                "iam:ListPolicies",
                "iam:ListUsers"
            ],
            "Resource": "*"
        }
    ]
}
```

## Custom IAM policy to grant read\-only access to GuardDuty<a name="security_iam_id-based-policy-examples-custom-readonly"></a>

To grant read\-only access to GuardDuty you can use the `AmazonGuardDutyReadOnlyAccess` managed policy\. 

To create a custom policy that grants an IAM user, role, or group read\-only access to GuardDuty you can use the following statement:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "guardduty:ListMembers",
                "guardduty:GetMembers",
                "guardduty:ListInvitations",
                "guardduty:ListDetectors",
                "guardduty:GetDetector",
                "guardduty:ListFindings",
                "guardduty:GetFindings",
                "guardduty:ListIPSets",
                "guardduty:GetIPSet",
                "guardduty:ListThreatIntelSets",
                "guardduty:GetThreatIntelSet",
                "guardduty:GetMasterAccount",
                "guardduty:GetInvitationsCount",
                "guardduty:GetFindingsStatistics"
            ],
            "Resource": "*"
        }
    ]
}
```

## Deny Access to GuardDuty findings<a name="security_iam_id-based-policy-examples-deny-findings"></a>

You can use the following policy to deny an IAM user, role, or group access to GuardDuty findings\. Users can't view findings or the details about findings, but they can access all other GuardDuty operations:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "guardduty:CreateDetector",
                "guardduty:DeleteDetector",
                "guardduty:UpdateDetector",
                "guardduty:GetDetector",
                "guardduty:ListDetectors",
                "guardduty:CreateIPSet",
                "guardduty:DeleteIPSet",
                "guardduty:UpdateIPSet",
                "guardduty:GetIPSet",
                "guardduty:ListIPSets",
                "guardduty:CreateThreatIntelSet",
                "guardduty:DeleteThreatIntelSet",
                "guardduty:UpdateThreatIntelSet",
                "guardduty:GetThreatIntelSet",                      
                "guardduty:ListThreatIntelSets",
                "guardduty:ArchiveFindings",
                "guardduty:UnarchiveFindings",
                "guardduty:CreateSampleFindings",
                "guardduty:CreateMembers",
                "guardduty:InviteMembers",
                "guardduty:GetMembers",
                "guardduty:DeleteMembers",
                "guardduty:DisassociateMembers",
                "guardduty:StartMonitoringMembers",
                "guardduty:StopMonitoringMembers",
                "guardduty:ListMembers",
                "guardduty:GetMasterAccount",
                "guardduty:DisassociateFromMasterAccount",
                "guardduty:AcceptInvitation",
                "guardduty:ListInvitations",
                "guardduty:GetInvitationsCount",
                "guardduty:DeclineInvitations",
                "guardduty:DeleteInvitations"
            ],
            "Resource": "*"
        }, 
         {
            "Effect": "Allow",
            "Action": [
                "iam:CreateServiceLinkedRole"
            ],
            "Resource": "arn:aws:iam::123456789123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty",
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
            "Resource": "arn:aws:iam::123456789123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
        }
    ]
}
```

## Using a custom IAM policy to limit access to GuardDuty resources<a name="security_iam_id-based-policy-examples-guardduty_restrict_access_to_resources"></a>

To define a user's access to GuardDuty based on the detector ID, you can use all [GuardDuty API actions](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_Operations.html) in your custom IAM policies, **except** the following operations:
+ `guardduty:CreateDetector`
+ `guardduty:DeclineInvitations`
+ `guardduty:DeleteInvitations`
+ `guardduty:GetInvitationsCount`
+ `guardduty:ListDetectors`
+ `guardduty:ListInvitations`

Use the following operations in an IAM policy to define a user's access to GuardDuty based on the IPSet ID and ThreatIntelSet ID:
+ `guardduty:DeleteIPSet`
+ `guardduty:DeleteThreatIntelSet`
+ `guardduty:GetIPSet`
+ `guardduty:GetThreatIntelSet`
+ `guardduty:UpdateIPSet`
+ `guardduty:UpdateThreatIntelSet`

The following examples show how to create policies using some of the preceding operations:
+ This policy allows a user to run the `guardduty:UpdateDetector` operation, using the detector ID of 1234567 in the us\-east\-1 Region: 

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                   "guardduty:UpdateDetector",
               ],
              "Resource": "arn:aws:guardduty:us-east-1:012345678910:detector/1234567"
          }
      ]
  }
  ```
+ This policy allows a user to run the `guardduty:UpdateIPSet` operation, using the detector ID of 1234567 and the IPSet ID of 000000 in the us\-east\-1 Region:
**Note**  
Make sure that the user has the permissions required to access trusted IP lists and threat lists in GuardDuty\. For more information, see [Permissions required to upload trusted IP lists and threat lists](guardduty_upload-lists.md#upload-permissions)\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                   "guardduty:UpdateIPSet",
               ],
              "Resource": "arn:aws:guardduty:us-east-1:012345678910:detector/1234567/ipset/000000"
          }
      ]
  }
  ```
+ This policy allows a user to run the `guardduty:UpdateIPSet` operation, using any detector ID and the IPSet ID of 000000 in the us\-east\-1 Region:
**Note**  
Make sure that the user has the permissions required to access trusted IP lists and threat lists in GuardDuty\. For more information, see [Permissions required to upload trusted IP lists and threat lists](guardduty_upload-lists.md#upload-permissions)\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                   "guardduty:UpdateIPSet",
               ],
              "Resource": "arn:aws:guardduty:us-east-1:012345678910:detector/*/ipset/000000"
          }
      ]
  }
  ```
+ This policy allows a user to run the `guardduty:UpdateIPSet` operation, using the detector ID of 1234567 and any IPSet ID in the us\-east\-1 Region:
**Note**  
Make sure that the user has the permissions required to access trusted IP lists and threat lists in GuardDuty\. For more information, see [Permissions required to upload trusted IP lists and threat lists](guardduty_upload-lists.md#upload-permissions)\.

  ```
  {
      "Version": "2012-10-17",
      "Statement": [
          {
              "Effect": "Allow",
              "Action": [
                   "guardduty:UpdateIPSet",
               ],
              "Resource": "arn:aws:guardduty:us-east-1:012345678910:detector/1234567/ipset/*"
          }
      ]
  }
  ```
