# Managing access<a name="guardduty_managing_access"></a>

**Topics**
+ [Permissions required to enable GuardDuty](#guardduty_enable-permissions)
+ [Using a service\-linked role to delegate permissions to GuardDuty](#guardduty_service-access)
+ [Using IAM policies to delegate access to GuardDuty to IAM identities](#guardduty_user-access)

## Permissions required to enable GuardDuty<a name="guardduty_enable-permissions"></a>

This section describes the permissions that various IAM identities \(users, groups, and roles\) must have in order to initially enable GuardDuty either through the console or programmatically \(using the GuardDuty API or the GuardDuty commands in the AWS CLI\)\. 

To grant permissions required to enable GuardDuty, attach the following policy to an IAM user, group, or role:

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

## Using a service\-linked role to delegate permissions to GuardDuty<a name="guardduty_service-access"></a>

This section describes the permissions that the GuardDuty service itself requires to function and perform operations on your behalf, such as generating findings\.

When you enable GuardDuty \(using the GuardDuty console or programmatically through the API operations or AWS CLI commands\), it is automatically assigned a service\-linked role called `AWSServiceRoleForAmazonGuardDuty`\. A service\-linked role is a unique type of IAM role that is linked directly to an AWS service \(in this case, GuardDuty\)\. Service\-linked roles are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf\. The linked service \(in this case, GuardDuty\) also defines how you create, modify, and delete a service\-linked role\. For more information about service\-linked roles, see [Using service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html)\. 

The `AWSServiceRoleForAmazonGuardDuty` service\-linked role is created automatically when GuardDuty is enabled\. It includes the permissions and the trust policies that GuardDuty requires to consume and analyze events directly from AWS CloudTrail, VPC Flow Logs, and DNS logs and generate security findings\.

You cannot edit the `AWSServiceRoleForAmazonGuardDuty` service\-linked role\. You can view its permissions or delete this service\-linked role via the IAM console\. To delete the `AWSServiceRoleForAmazonGuardDuty` service\-linked role, you must first [disable GuardDuty](guardduty_suspend-disable.md) in all Regions in that AWS account\. 

To view the permissions attached to `AWSServiceRoleForAmazonGuardDuty`, choose the **View service role permissions** button in the **Setting/General** tab of the GuardDuty console\. 

The following is the permissions policy document that is attached to the `AWSServiceRoleForAmazonGuardDuty` service\-linked role:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeInstances",
                "ec2:DescribeImages"
            ],
            "Resource": "*"
        }
    ]
}
```

The following is the trust policy that is attached to the `AWSServiceRoleForAmazonGuardDuty` service\-linked role:

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
```

## Using IAM policies to delegate access to GuardDuty to IAM identities<a name="guardduty_user-access"></a>

This section describes how to delegate access to GuardDuty to various IAM identities \(users, groups, and roles\)\. 

By default, access to the GuardDuty resources \(detector, trusted IP lists, threat lists, findings, members, master account, and invitations\) is restricted to the owner of the AWS account that the resources were created in\. If you are the owner, you can choose to grant full or limited access to GuardDuty to the various IAM identities in your account\. For more information about creating IAM access policies, see the [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)\.

**Topics**
+ [AWS managed \(predefined\) policies for GuardDuty](#guardduty_managedpolicies)
+ [Using a custom IAM policy to grant full access to GuardDuty](#guardduty_allow)
+ [Using a custom IAM policy to grant read\-only access to GuardDuty](#guardduty_read-only)
+ [Using a custom IAM policy to deny access to GuardDuty findings](#guardduty_restrict_access_to_findings)
+ [Using a custom IAM policy to limit access to GuardDuty resources](#guardduty_restrict_access_to_resources)
+ [Resources defined by GuardDuty](#guardduty-resources)

### AWS managed \(predefined\) policies for GuardDuty<a name="guardduty_managedpolicies"></a>

AWS addresses many common use cases by providing standalone IAM policies that are created and administered by AWS\. These *managed policies* grant necessary permissions for common use cases so that you can avoid having to investigate which permissions are needed\. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) in the *IAM User Guide*\.

The following AWS managed policies, which you can attach to users in your account, are specific to GuardDuty:
+ **AmazonGuardDutyFullAccess ** – provides access to all of GuardDuty functionality\. However, when it comes to working with trusted IP lists and threat lists in GuardDuty, this managed policy provides identities with only limited access\. More specifically, an identity with the **AmazonGuardDutyFullAccess** managed policy attached can only rename and deactivate uploaded trusted IP lists and threat lists\.

   To grant various identities full access to working with trusted IP lists and threat lists \(in addition to renaming and deactivating, this includes uploading, activating, deleting, and updating the location of the lists\), make sure that the following actions are present in the permissions policy attached to an IAM user, group, or role: 

  ```
  {
      "Effect": "Allow",
      "Action": [
          "iam:PutRolePolicy",
          "iam:DeleteRolePolicy"
      ],
      "Resource": "arn:aws:iam::123456789123:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
  }
  ```
+ **AmazonGuardDutyReadOnlyAccess ** – Provides read\-only access to GuardDuty\. 

### Using a custom IAM policy to grant full access to GuardDuty<a name="guardduty_allow"></a>

You can use the following custom policy to grant an IAM user, role, or group full access to the GuardDuty console and all GuardDuty operations\.

**Note**  
Replace the sample account ID in the example below with your actual AWS account ID\.

```
 "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "iam:CreateServiceLinkedRole",
            "Resource": "arn:aws:iam::123456789012:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty",
            "Condition": {
                "StringLike": {
                    "iam:AWSServiceName": "guardduty.amazonaws.com"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": "guardduty:*",
            "Resource": "*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:DeleteRolePolicy",
                "iam:ListAttachedRolePolicies",
                "iam:PutRolePolicy",
                "iam:ListRolePolicies"
            ],
            "Resource": "arn:aws:iam::123456789012:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
        },
        {
            "Effect": "Allow",
            "Action": [
                "iam:ListPolicyVersions",
                "iam:GetPolicy",
                "iam:GetPolicyVersion"
            ],
            "Resource": "*"
        }
    ]
```

### Using a custom IAM policy to grant read\-only access to GuardDuty<a name="guardduty_read-only"></a>

You can use the following policy to grant an IAM user, role, or group read\-only access to GuardDuty:

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

### Using a custom IAM policy to deny access to GuardDuty findings<a name="guardduty_restrict_access_to_findings"></a>

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

### Using a custom IAM policy to limit access to GuardDuty resources<a name="guardduty_restrict_access_to_resources"></a>

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

### Resources defined by GuardDuty<a name="guardduty-resources"></a>


| **Resource type** | **ARN** | 
| --- | --- | 
| detector | arn:$\{Partition\}:guardduty:$\{Region\}:$\{Account\}:detector/$\{DetectorId\} | 
| ipset | arn:$\{Partition\}:guardduty:$\{Region\}:$\{Account\}:detector/$\{DetectorId\}/ipset/$\{IPSetId\} | 
| threatintelset | arn:$\{Partition\}:guardduty:$\{Region\}:$\{Account\}:detector/$\{DetectorId\}/threatintelset/$\{ThreatIntelSetId\} | 
| filter | arn:$\{Partition\}:guardduty:$\{Region\}:$\{Account\}:detector/$\{DetectorId\}/filter/$\{FilterName\} | 