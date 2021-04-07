# GuardDuty IAM finding types<a name="guardduty_finding-types-iam"></a>

The following findings are specific to IAM entities and access keys and always have a **Resource Type** of `AccessKey`\. The severity and details of the findings differ based on the finding type\.

For all IAM related findings, it is recommended that you examine the permissions on the entity in question and ensure that this entity follows the best practice of least privilege\. If the activity is unexpected, the credentials may be compromised\. See actions detailed in [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

**Topics**
+ [CredentialAccess:IAMUser/AnomalousBehavior](#credentialaccess-iam-anomalousbehavior)
+ [DefenseEvasion:IAMUser/AnomalousBehavior](#defenseevasion-iam-anomalousbehavior)
+ [Discovery:IAMUser/AnomalousBehavior](#discovery-iam-anomalousbehavior)
+ [Exfiltration:IAMUser/AnomalousBehavior](#exfiltration-iam-anomalousbehavior)
+ [Impact:IAMUser/AnomalousBehavior](#impact-iam-anomalousbehavior)
+ [InitialAccess:IAMUser/AnomalousBehavior](#initialaccess-iam-anomalousbehavior)
+ [PenTest:IAMUser/KaliLinux](#pentest-iam-kalilinux)
+ [PenTest:IAMUser/ParrotLinux](#pentest-iam-parrotlinux)
+ [PenTest:IAMUser/PentooLinux](#pentest-iam-pentoolinux)
+ [Persistence:IAMUser/AnomalousBehavior](#persistence-iam-anomalousbehavior)
+ [Policy:IAMUser/RootCredentialUsage](#policy-iam-rootcredentialusage)
+ [PrivilegeEscalation:IAMUser/AnomalousBehavior](#privilegeescalation-iam-anomalousbehavior)
+ [Recon:IAMUser/MaliciousIPCaller](#recon-iam-maliciousipcaller)
+ [Recon:IAMUser/MaliciousIPCaller\.Custom](#recon-iam-maliciousipcallercustom)
+ [Recon:IAMUser/TorIPCaller](#recon-iam-toripcaller)
+ [Stealth:IAMUser/CloudTrailLoggingDisabled](#stealth-iam-cloudtrailloggingdisabled)
+ [Stealth:IAMUser/PasswordPolicyChange](#stealth-iam-passwordpolicychange)
+ [UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](#unauthorizedaccess-iam-consoleloginsuccessb)
+ [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](#unauthorizedaccess-iam-instancecredentialexfiltration)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller](#unauthorizedaccess-iam-maliciousipcaller)
+ [UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](#unauthorizedaccess-iam-maliciousipcallercustom)
+ [UnauthorizedAccess:IAMUser/TorIPCaller](#unauthorizedaccess-iam-toripcaller)

## CredentialAccess:IAMUser/AnomalousBehavior<a name="credentialaccess-iam-anomalousbehavior"></a>

### An API used to gain access to an AWS environment was invoked in an anomalous way\.<a name="credentialaccess-iam-anomalousbehavior_description"></a>

#### <a name="credentialaccess-iam-anomalousbehavior_severity"></a>

**Default severity: Medium**

#### <a name="credentialaccess-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with the credential access stage of an attack when an adversary is attempting to collect passwords, usernames, and access keys for your environment\. The API’s in this category are `GetPasswordData`, `GetSecretValue`, and `GenerateDbAuthToken`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="credentialaccess-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## DefenseEvasion:IAMUser/AnomalousBehavior<a name="defenseevasion-iam-anomalousbehavior"></a>

### An API used to evade defensive measures was invoked in an anomalous way\.<a name="defenseevasion-iam-anomalousbehavior_description"></a>

#### <a name="defenseevasion-iam-anomalousbehavior_severity"></a>

**Default severity: Medium**

#### <a name="defenseevasion-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with defense evasion tactics where an adversary is trying to cover their tracks and avoid detection\. API’s in this category are typically delete, disable, or stop operations, such as, `DeleteFlowLogs`, `DisableAlarmActions`, or `StopLogging`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="defenseevasion-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Discovery:IAMUser/AnomalousBehavior<a name="discovery-iam-anomalousbehavior"></a>

### An API commonly used to discover resources was invoked in an anomalous way\.<a name="discovery-iam-anomalousbehavior_description"></a>

#### <a name="discovery-iam-anomalousbehavior_severity"></a>

**Default severity: Low**

#### <a name="discovery-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with the discovery stage of an attack when an adversary is gathering information to determine if your AWS environment is susceptible to a broader attack\. API’s in this category are typically get, describe, or list operations, such as, `DescribeInstances`, `GetRolePolicy`, or `ListAccessKeys`\.

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="discovery-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Exfiltration:IAMUser/AnomalousBehavior<a name="exfiltration-iam-anomalousbehavior"></a>

### An API commonly used to collect data from an AWS environment was invoked in an anomalous way\.<a name="exfiltration-iam-anomalousbehavior_description"></a>

#### <a name="exfiltration-iam-anomalousbehavior_severity"></a>

**Default severity: High**

#### <a name="exfiltration-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with exfiltration tactics where an adversary is trying to collect data from your network using packaging and encryption to avoid detection\. API’s for this finding type are CloudTrail management \(control\-plane\) operations only and are typically related to S3, snapshots, and databases, such as, `PutBucketReplication`, `CreateSnapshot`, or `RestoreDBInstanceFromDBSnapshot`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="exfiltration-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Impact:IAMUser/AnomalousBehavior<a name="impact-iam-anomalousbehavior"></a>

### An API commonly used to tamper with data or processes in an AWS environment was invoked in an anomalous way\.<a name="impact-iam-anomalousbehavior_description"></a>

#### <a name="impact-iam-anomalousbehavior_severity"></a>

**Default severity: High**

#### <a name="impact-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with impact tactics where an adversary is trying to disrupt operations and manipulate, interrupt, or destroy data in your account\. API’s for this finding type are typically delete, update, or put operations, such as, `DeleteSecurityGroup`, `UpdateUser`, or `PutBucketPolicy`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="impact-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## InitialAccess:IAMUser/AnomalousBehavior<a name="initialaccess-iam-anomalousbehavior"></a>

### An API commonly used to gain unauthorized access to an AWS environment was invoked in an anomalous way\.<a name="initialaccess-iam-anomalousbehavior_description"></a>

#### <a name="initialaccess-iam-anomalousbehavior_severity"></a>

**Default severity: Medium**

#### <a name="initialaccess-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with the initial access stage of an attack when an adversary is attempting to establish access to your environment\. API’s in this category are typically get token, or session operations, such as, `GetFederationToken`, `StartSession`, or `GetAuthorizationToken`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="initialaccess-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PenTest:IAMUser/KaliLinux<a name="pentest-iam-kalilinux"></a>

### An API was invoked from a Kali Linux EC2 machine\.<a name="pentest-iam-kalilinux_description"></a>

#### <a name="pentest-iam-kalilinux_severity"></a>

**Default severity: Medium**

#### <a name="pentest-iam-kalilinux_full"></a>

This finding informs you that a machine running Kali Linux is making API calls using credentials that belong to the listed AWS account in your environment\. Kali Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\. 

#### <a name="pentest-iam-kalilinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PenTest:IAMUser/ParrotLinux<a name="pentest-iam-parrotlinux"></a>

### An API was invoked from a Parrot Security Linux machine\.<a name="pentest-iam-parrotlinux_description"></a>

#### <a name="pentest-iam-parrotlinux_severity"></a>

**Default severity: Medium**

#### <a name="pentest-iam-parrotlinux_full"></a>

This finding informs you that a machine running Parrot Security Linux is making API calls using credentials that belong to the listed AWS account in your environment\. Parrot Security Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-iam-parrotlinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PenTest:IAMUser/PentooLinux<a name="pentest-iam-pentoolinux"></a>

### An API was invoked from a Pentoo Linux machine\.<a name="pentest-iam-pentoolinux_description"></a>

#### <a name="pentest-iam-pentoolinux_severity"></a>

**Default severity: Medium**

#### <a name="pentest-iam-pentoolinux_full"></a>

This finding informs you that a machine running Pentoo Linux is making API calls using credentials that belong to the listed AWS account in your environment\. Pentoo Linux is a popular penetration testing tool that security professionals use to identify weaknesses in EC2 instances that require patching\. Attackers also use this tool to find EC2 configuration weaknesses and gain unauthorized access to your AWS environment\.

#### <a name="pentest-iam-pentoolinux_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Persistence:IAMUser/AnomalousBehavior<a name="persistence-iam-anomalousbehavior"></a>

### An API commonly used to maintain unauthorized access to an AWS environment was invoked in an anomalous way\.<a name="persistence-iam-anomalousbehavior_description"></a>

#### <a name="persistence-iam-anomalousbehavior_severity"></a>

**Default severity: Medium**

#### <a name="persistence-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with persistence tactics where an adversary has gained access to your environment and is attempting to maintain that access\. API’s in this category are typically create, import, or modify operations, such as, `CreateAccessKey`, `ImportKeyPair`, or `ModifyInstanceAttribute`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="persistence-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Policy:IAMUser/RootCredentialUsage<a name="policy-iam-rootcredentialusage"></a>

### An API was invoked using root credentials\.<a name="policy-iam-rootcredentialusage_description"></a>

#### <a name="policy-iam-rootcredentialusage_severity"></a>

**Default severity: Low**

#### <a name="policy-iam-rootcredentialusage_full"></a>

This finding informs you that the root credentials of the listed AWS account in your environment are being used to make requests to AWS services\. It is recommended that users never use root credentials to access AWS services\. Instead, AWS services should be accessed using least privilege temporary credentials from AWS Security Token Service \(STS\)\. For situations where STS is not supported, IAM user credentials are recommended\. For more information, see [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

**Note**  
If S3 threat detection is enabled for the account this finding may be generated in response to attempts to run S3 data plane operations on S3 resources using the root credentials of the AWS account\. The API call used will be listed in the finding details\. If S3 threat detection is not enabled this finding can only be triggered by Event log APIs\. For more information on S3 threat detection see [S3 protection](https://docs.aws.amazon.com/guardduty/latest/ug/s3_detection.html)\.

#### <a name="policy-iam-rootcredentialusage_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## PrivilegeEscalation:IAMUser/AnomalousBehavior<a name="privilegeescalation-iam-anomalousbehavior"></a>

### An API commonly used to used to obtain high\-level permissions to an AWS environment was invoked in an anomalous way\.<a name="privilegeescalation-iam-anomalousbehavior_description"></a>

#### <a name="privilegeescalation-iam-anomalousbehavior_severity"></a>

**Default severity: Medium**

#### <a name="privilegeescalation-iam-anomalousbehavior_full"></a>

This finding informs you that an anomalous API request was observed in your account\. This finding may include a single API or a series of related API requests made in proximity by a single [CloudTrail user identity](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\. The API observed is commonly associated with privilege escalation tactics where an adversary is attempting to gain higher\-level permissions to an environment \. API’s in this category typically involve operations that change IAM policies, roles, and users, such as, `AssociateIamInstanceProfile`, `AddUserToGroup`, or `PutUserPolicy`\. 

This API request was identified as anomalous by GuardDuty's anomaly detection machine learning \(ML\) model\. The ML model evaluates all API requests in your account and identifies anomalous events that are associated with techniques used by adversaries\. The ML model tracks various factors of the API request, such as, the user that made the request, the location the request was made from, and the specific API that was requested\. Details on which factors of the API request are unusual for the user identity that invoked the request can be found in the [finding details](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_findings-summary.html#finding-anomalous)\.

#### <a name="privilegeescalation-iam-anomalousbehavior_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/MaliciousIPCaller<a name="recon-iam-maliciousipcaller"></a>

### An API was invoked from a known malicious IP address\.<a name="recon-iam-maliciousipcaller_description"></a>

#### <a name="recon-iam-maliciousipcaller_severity"></a>

**Default severity: Medium**

#### <a name="recon-iam-maliciousipcaller_full"></a>

This finding informs you that an API operation that can list or describe AWS resources in an account within your environment was invoked from an IP address that is included on a threat list\. An attacker may use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-maliciousipcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/MaliciousIPCaller\.Custom<a name="recon-iam-maliciousipcallercustom"></a>

### An API was invoked from a known malicious IP address\.<a name="recon-iam-maliciousipcallercustom_description"></a>

#### <a name="recon-iam-maliciousipcallercustom_severity"></a>

**Default severity: Medium**

#### <a name="recon-iam-maliciousipcallercustom_full"></a>

This finding informs you that an API operation that can list or describe AWS resources in an account within your environment was invoked from an IP address that is included on a custom threat list\. The threat list used will be listed in the finding's details\. An attacker might use stolen credentials to perform this type of reconnaissance of your AWS resources in order to find more valuable credentials or determine the capabilities of the credentials they already have\.

#### <a name="recon-iam-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Recon:IAMUser/TorIPCaller<a name="recon-iam-toripcaller"></a>

### An API was invoked from a Tor exit node IP address\.<a name="recon-iam-toripcaller_description"></a>

#### <a name="recon-iam-toripcaller_severity"></a>

**Default severity: Medium**

#### <a name="recon-iam-toripcaller_full"></a>

This finding informs you that an API operation that can list or describe AWS resources in an account within your environment was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. An attacker would use Tor to mask their true identity\.

#### <a name="recon-iam-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:IAMUser/CloudTrailLoggingDisabled<a name="stealth-iam-cloudtrailloggingdisabled"></a>

### AWS CloudTrail trail was disabled\.<a name="stealth-iam-cloudtrailloggingdisabled_description"></a>

#### <a name="stealth-iam-cloudtrailloggingdisabled_severity"></a>

**Default severity: Low**

#### <a name="stealth-iam-cloudtrailloggingdisabled_full"></a>

This finding informs you that a CloudTrail trail within your AWS environment was disabled\. This can be an attacker's attempt to disable logging to cover their tracks by eliminating any trace of their activity while gaining access to your AWS resources for malicious purposes\. This finding can be triggered by a successful deletion or update of a trail\. This finding can also be triggered by a successful deletion of an S3 bucket that stores the logs from a trail that is associated with GuardDuty\.

#### <a name="stealth-iam-cloudtrailloggingdisabled_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Stealth:IAMUser/PasswordPolicyChange<a name="stealth-iam-passwordpolicychange"></a>

### Account password policy was weakened\.<a name="stealth-iam-passwordpolicychange_description"></a>

#### <a name="stealth-iam-passwordpolicychange_severity"></a>

**Default severity: Low**

#### <a name="stealth-iam-passwordpolicychange_full"></a>

The AWS account password policy was weakened on the listed account within your AWS environment\. For example, it was deleted or updated to require fewer characters, not require symbols and numbers, or required to extend the password expiration period\. This finding can also be triggered by an attempt to update or delete your AWS account password policy\. The AWS account password policy defines the rules that govern what kinds of passwords can be set for your IAM users\. A weaker password policy permits the creation of passwords that are easy to remember and potentially easier to guess, thereby creating a security risk\.

#### <a name="stealth-iam-passwordpolicychange_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B<a name="unauthorizedaccess-iam-consoleloginsuccessb"></a>

### Multiple worldwide successful console logins were observed\.<a name="unauthorizedaccess-iam-consoleloginsuccessb_description"></a>

#### <a name="unauthorizedaccess-iam-consoleloginsuccessb_severity"></a>

**Default severity: Medium**

#### <a name="unauthorizedaccess-iam-consoleloginsuccessb_full"></a>

This finding informs you that multiple successful console logins for the same IAM user were observed around the same time in various geographical locations\. Such anomalous and risky access location patterns indicate potential unauthorized access to your AWS resources\. 

#### <a name="unauthorizedaccess-iam-consoleloginsuccessb_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration<a name="unauthorizedaccess-iam-instancecredentialexfiltration"></a>

### Credentials that were created exclusively for an EC2 instance through an Instance launch role are being used from an external IP address\.<a name="unauthorizedaccess-iam-instancecredentialexfiltration_description"></a>

#### <a name="unauthorizedaccess-iam-instancecredentialexfiltration_severity"></a>

**Default severity: High**

#### <a name="unauthorizedaccess-iam-instancecredentialexfiltration_full"></a>

This finding informs you of attempts to run AWS API operations from a host outside of EC2, using temporary AWS credentials that were created on an EC2 instance in your AWS environment\. The listed EC2 instance might be compromised, and the temporary credentials from this instance might have been exfiltrated to a remote host outside of AWS\. AWS does not recommend redistributing temporary credentials outside of the entity that created them \(for example, AWS applications, EC2, or Lambda\)\. However, authorized users can export credentials from their EC2 instances to make legitimate API calls\. To rule out a potential attack and verify the legitimacy of the activity, contact the IAM user to whom these credentials are assigned\.

**Note**  
If S3 threat detection is enabled for the account this finding may be generated in response to attempts to run S3 data plane operations on the S3 resources using EC2 credentials\. The API call used will be listed in the finding details\. If S3 threat detection is not enabled this finding can only be triggered by Event log APIs\. For more information on S3 threat detection see [S3 protection](https://docs.aws.amazon.com/guardduty/latest/ug/s3_detection.html?icmpid=docs_gd_help_panel)\.

#### <a name="unauthorizedaccess-iam-instancecredentialexfiltration_remediation"></a>

**Remediation recommendations:**

This finding is generated when networking is configured to route internet traffic such that it egresses from an on\-premises gateway rather than from a VPC Internet Gateway \(IGW\)\. Common configurations, such as using [AWS Outposts](https://docs.aws.amazon.com/outposts/latest/userguide/), or VPC VPN connections, can result in traffic routed this way\. If this is expected behavior, it's recommended that you use suppression rules in and create a rule that consists of two filter criteria\. The first criteria is **finding type**, which should be `UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration`\. The second filter criteria is **API caller IPv4 Address** with the IP address or CIDR range of your on\-premises internet gateway\. To learn more about creating suppression rules see [Suppression rules](https://docs.aws.amazon.com/guardduty/latest/ug/findings_suppression-rule.html?icmpid=docs_gd_help_panel)\. 

If this activity is unexpected your credentials may be compromised, see [Remediating compromised credentials](https://docs.aws.amazon.com/guardduty/latest/ug/guardduty_remediate.html#compromised-creds)\.

## UnauthorizedAccess:IAMUser/MaliciousIPCaller<a name="unauthorizedaccess-iam-maliciousipcaller"></a>

### An API was invoked from a known malicious IP address\.<a name="unauthorizedaccess-iam-maliciousipcaller_description"></a>

#### <a name="unauthorizedaccess-iam-maliciousipcaller_severity"></a>

**Default severity: Medium**

#### <a name="unauthorizedaccess-iam-maliciousipcaller_full"></a>

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges\) was invoked from a known malicious IP address\. This can indicate unauthorized access to AWS resources within your environment\.

#### <a name="unauthorizedaccess-iam-maliciousipcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom<a name="unauthorizedaccess-iam-maliciousipcallercustom"></a>

### An API was invoked from an IP address on a custom threat list\.<a name="unauthorizedaccess-iam-maliciousipcallercustom_description"></a>

#### <a name="unauthorizedaccess-iam-maliciousipcallercustom_severity"></a>

**Default severity: Medium**

#### <a name="unauthorizedaccess-iam-maliciousipcallercustom_full"></a>

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, modify AWS privileges\) was invoked from an IP address that is included on a threat list that you uploaded\. In , a threat list consists of known malicious IP addresses\. This can indicate unauthorized access to AWS resources within your environment\.

#### <a name="unauthorizedaccess-iam-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## UnauthorizedAccess:IAMUser/TorIPCaller<a name="unauthorizedaccess-iam-toripcaller"></a>

### An API was invoked from a Tor exit node IP address\.<a name="unauthorizedaccess-iam-toripcaller_description"></a>

#### <a name="unauthorizedaccess-iam-toripcaller_severity"></a>

**Default severity: Medium**

#### <a name="unauthorizedaccess-iam-toripcaller_full"></a>

This finding informs you that an API operation \(for example, an attempt to launch an EC2 instance, create a new IAM user, or modify your AWS privileges\) was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This can indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="unauthorizedaccess-iam-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected your credentials may be compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.