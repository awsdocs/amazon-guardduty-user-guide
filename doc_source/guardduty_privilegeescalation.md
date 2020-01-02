# PrivilegeEscalation Finding Types<a name="guardduty_privilegeescalation"></a>

This section covers the active PrivilegeEscalation threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [PrivilegeEscalation:IAMUser/AdministrativePermissions](#privilegeescalation1)

## PrivilegeEscalation:IAMUser/AdministrativePermissions<a name="privilegeescalation1"></a>

### Finding description<a name="privilegeescalation1_description"></a>

**A principal has attempted to assign a highly permissive policy to themselves\. This behavior is associated with a privilege escalation attack\.**

This finding informs you that a specific principal in your AWS environment is exhibiting behavior that can be indicative of a privilege escalation attack\. This finding is triggered when a user or role attempts to assign a highly permissive policy to themselves\. If the user or role in question is not meant to have administrative privileges, either the user's credentials may be compromised or the role's permissions may not be configured properly\. In an effort to maximize their ability to access your account, even after they have been discovered, attackers can use stolen credentials or a misconfigured role to escalate their privileges and then create new users, add access policies to existing users, create access keys, etc\. For more information, see [Remediating Compromised AWS Credentials](guardduty_remediate.md#compromised-creds)\. 

### Default severity: Low<a name="privilegeescalation1_severity"></a>

This finding’s severity is Low if the attempt at privilege escalation was unsuccessful, and Medium if the attempt at privilege escalation was successful\.