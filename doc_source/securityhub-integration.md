# Integration with AWS Security Hub<a name="securityhub-integration"></a>

[AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html) provides you with a comprehensive view of your security state in AWS and helps you to check your environment against security industry standards and best practices\. Security Hub collects security data from across AWS accounts, services, and supported third\-party partner products and helps you to analyze your security trends and identify the highest priority security issues\.

The Amazon GuardDuty integration with Security Hub enables you to send findings from GuardDuty to Security Hub\. Security Hub can then include those findings in its analysis of your security posture\.

**Contents**
+ [How Amazon GuardDuty sends findings to AWS Security Hub](#securityhub-integration-sending-findings)
  + [Types of findings that GuardDuty sends](#securityhub-integration-finding-types)
  + [Latency for sending findings](#securityhub-integration-finding-latency)
  + [Retrying when Security Hub is not available](#securityhub-integration-retry-send)
  + [Updating existing findings in Security Hub](#securityhub-integration-finding-updates)
+ [Viewing GuardDuty findings in AWS Security Hub](#findings-in-securityhub)
  + [Interpreting GuardDuty finding names in AWS Security Hub](#interpreting-findings-in-securityhub)
+ [Typical finding from GuardDuty](#securityhub-integration-finding-example)
+ [Enabling and configuring the integration](#securityhub-integration-enable)
+ [How to stop sending findings](#securityhub-integration-disable)

## How Amazon GuardDuty sends findings to AWS Security Hub<a name="securityhub-integration-sending-findings"></a>

In AWS Security Hub, security issues are tracked as findings\. Some findings come from issues that are detected by other AWS services or by third\-party partners\. Security Hub also has a set of rules that it uses to detect security issues and generate findings\.

Security Hub provides tools to manage findings from across all of these sources\. You can view and filter lists of findings and view details for a finding\. See [Viewing findings](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-viewing.html) in the *AWS Security Hub User Guide*\. You can also track the status of an investigation into a finding\. See [Taking action on findings](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-taking-action.html) in the *AWS Security Hub User Guide*\.

All findings in Security Hub use a standard JSON format called the AWS Security Finding Format \(ASFF\)\. The ASFF includes details about the source of the issue, the affected resources, and the current status of the finding\. See [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.htm) in the *AWS Security Hub User Guide*\.

Amazon GuardDuty is one of the AWS services that sends findings to Security Hub\.

### Types of findings that GuardDuty sends<a name="securityhub-integration-finding-types"></a>

GuardDuty sends all of the findings it generates to Security Hub\.

GuardDuty sends the findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)\. In ASFF, the `Types` field provides the finding type\.

### Latency for sending findings<a name="securityhub-integration-finding-latency"></a>

When GuardDuty creates a new finding, it is usually sent to Security Hub within five minutes\.

### Retrying when Security Hub is not available<a name="securityhub-integration-retry-send"></a>

If Security Hub is not available, GuardDuty retries sending the findings until they are received\.

### Updating existing findings in Security Hub<a name="securityhub-integration-finding-updates"></a>

After it sends a finding to Security Hub, GuardDuty sends updates to reflect additional observations of the finding activity to Security Hub\. The rate at which aggregated findings are updated is based on the [](guardduty_exportfindings.md#guardduty_exportfindings-frequency) specified\.

Archiving or unarchiving a GuardDuty finding will not update the finding in Security Hub\. This means that manually unarchived findings that become active in GuardDuty will not be sent to Security Hub 

## Viewing GuardDuty findings in AWS Security Hub<a name="findings-in-securityhub"></a>

To view your GuardDuty Findings in Security Hub select **See Findings** under **Amazon GuardDuty** from the summary page\. Alternatively you can select **Findings** from the navigation panel and filter the findings to display only GuardDuty findings by selecting the **Product name:** field with a value of `GuardDuty`\.

### Interpreting GuardDuty finding names in AWS Security Hub<a name="interpreting-findings-in-securityhub"></a>

GuardDuty sends the findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)\. In ASFF, the `Types` field provides the finding type\. ASFF types use a different naming scheme than GuardDuty types\. The table below details all the GuardDuty finding types with their ASFF counterpart as they appear in Security Hub\. 

**Note**  
For some GuardDuty finding types Security Hub assigns different ASFF finding names depending on whether the finding detail's **Resource Role** was **ACTOR** or **TARGET**\. For more information see [Finding details](guardduty_findings-summary.md)\.


|  GuardDuty finding type  |  ASFF finding type  | 
| --- | --- | 
|  Backdoor:EC2/C&CActivity\.B\!DNS  |  TTPs/Command and Control/Backdoor:EC2\-C&CActivity\.B\!DNS  | 
|  Backdoor:EC2/DenialOfService\.Dns  |  Effects/Denial of Service/Backdoor:EC2\-DenialOfService\.Tcp  | 
|  Backdoor:EC2/DenialOfService\.Tcp  |  Effects/Denial of Service/Backdoor:EC2\-DenialOfService\.Udp  | 
|  Backdoor:EC2/DenialOfService\.Udp  |  Effects/Denial of Service/Backdoor:EC2\-DenialOfService\.Dns  | 
|  Backdoor:EC2/DenialOfService\.UdpOnTcpPorts  |  Effects/Denial of Service/Backdoor:EC2\-DenialOfService\.UdpOnTcpPorts  | 
|  Backdoor:EC2/DenialOfService\.UnusualProtocol  |  Effects/Denial of Service/Backdoor:EC2\-DenialOfService\.UnusualProtocol  | 
|  Backdoor:EC2/Spambot  |  TTPs/Command and Control/Backdoor:EC2\-Spambot,  Unusual Behaviors/ VM/Backdoor:EC2\-Spambot  | 
|  Behavior:EC2/NetworkPortUnusual  |  Unusual Behaviors/VM/Behavior:EC2\-NetworkPortUnusual  | 
|  Behavior:EC2/TrafficVolumeUnusual  |  Unusual Behaviors/VM/Behavior:EC2\-TrafficVolumeUnusual  | 
|  CryptoCurrency:EC2/BitcoinTool\.B  |  TTPs/Command and Control/CryptoCurrency:EC2\-BitcoinTool\.B,  Effects/Resource Consumption/CryptoCurrency:EC2\-BitcoinTool\.B   | 
|  CryptoCurrency:EC2/BitcoinTool\.B\!DNS  |  TTPs/Command and Control/CryptoCurrency:EC2\-BitcoinTool\.B\!DNS,  Effects/Resource Consumption/CryptoCurrency:EC2\-BitcoinTool\.B\!DNS  | 
|  Recon:EC2/PortProbeEMRUnprotectedPort  |  TTPs/Initial Access/Recon:EC2\-PortProbeEMRUnprotectedPort,  Software and Configuration Checks/Network Reachability/Recon:EC2\-PortProbeEMRUnprotectedPort  | 
|  Recon:EC2/PortProbeUnprotectedPort  |  TTPs/Discovery/Recon:EC2\-PortProbeUnprotectedPort  | 
|  Recon:EC2/Portscan  |  TTPs/Discovery/Recon:EC2\-Portscan  | 
|  Trojan:EC2/BlackholeTraffic  |  TTPs/Command and Control/Trojan:EC2\-BlackholeTraffic  | 
|  Trojan:EC2/BlackholeTraffic\!DNS  |  TTPs/Command and Control/Trojan:EC2\-BlackholeTraffic\!DNS  | 
|  Trojan:EC2/DGADomainRequest\.B  |  TTPs/Command and Control/Trojan:EC2\-DGADomainRequest\.B  | 
|  Trojan:EC2/DGADomainRequest\.C\!DNS  |  TTPs/Command and Control/Trojan:EC2\-DGADomainRequest\.C\!DNS  | 
|  Trojan:EC2/DNSDataExfiltration  |  Effects/Data Exfiltration/Trojan:EC2\-DNSDataExfiltration  | 
|  Trojan:EC2/DriveBySourceTraffic\!DNS  |  TTPs/Command and Control/Trojan:EC2\-PhishingDomainRequest\!DNS  | 
|  Trojan:EC2/DropPoint  |  Effects/Data Exfiltration/Trojan:EC2\-DropPoint  | 
|  Trojan:EC2/DropPoint\!DNS  |  TTPs/Command and Control/Trojan:EC2\-BlackholeTraffic\!DNS  | 
|  Trojan:EC2/PhishingDomainRequest\!DNS  |  TTPs/Command and Control/Trojan:EC2\-PhishingDomainRequest\!DNS  | 
|  UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom  |  TTPs/Command and Control/UnauthorizedAccess:EC2\-MaliciousIPCaller\.Custom  | 
|  UnauthorizedAccess:EC2/MetadataDNSRebind  |  Software and Configuration Checks/AWS Security Best Practices/UnauthorizedAccess:EC2\-MetadataDNSRebind  | 
|  UnauthorizedAccess:EC2/RDPBruteForce  |  TTPs/Initial Access/UnauthorizedAccess:EC2\-RDPBruteForce  | 
|  UnauthorizedAccess:EC2/SSHBruteForce  |  TTPs/Initial Access/UnauthorizedAccess:EC2\-SSHBruteForce  | 
|  UnauthorizedAccess:EC2/TorClient  |  Effects/Data Exfiltration/UnauthorizedAccess:EC2\-TorClient,  TTPs/Command and Control/UnauthorizedAccess:EC2\-TorClient  | 
|  UnauthorizedAccess:EC2/TorIPCaller  |  TTPs/Command and Control/UnauthorizedAccess:EC2\-TorIPCaller  | 
|  UnauthorizedAccess:EC2/TorRelay  |   Effects/Resource Consumption/UnauthorizedAccess:EC2\-TorRelay  | 
|  PenTest:IAMUser/KaliLinux  |  TTPs/Discovery/PenTest:IAMUser\-KaliLinux  | 
|  PenTest:IAMUser/ParrotLinux  |  TTPs/Discovery/PenTest:IAMUser\-ParrotLinux  | 
|  PenTest:IAMUser/PentooLinux  |  TTPs/Discovery/PenTest:IAMUser\-PenTooLinux  | 
|  Persistence:IAMUser/NetworkPermissions  |  TTPs/Persistence/Persistence:IAMUser\-NetworkPermissions,  Unusual Behaviors/User/Persistence:IAMUser\-NetworkPermissions  | 
|  Persistence:IAMUser/ResourcePermissions  |  TTPs/Persistence/Persistence:IAMUser\-ResourcePermissions,  Unusual Behaviors/User/Persistence:IAMUser\-ResourcePermissions  | 
|  Persistence:IAMUser/UserPermissions  |  TTPs/Persistence/Persistence:IAMUser\-UserPermissions,  Unusual Behaviors/User/Recon:IAMUser\-UserPermissions  | 
|  Policy:IAMUser/RootCredentialUsage  |  Software and Configuration Checks/AWS Security Best Practices/Policy:IAMUser\-RootCredentialUsage  | 
|  PrivilegeEscalation:IAMUser/AdministrativePermissions  |  TTPs/PrivilegeEscalation/PrivilegeEscalation:IAMUser\-AdministrativePermissions  | 
|  Recon:IAMUser/MaliciousIPCaller  |  TTPs/Discovery/Recon:IAMUser\-MaliciousIPCaller  | 
|  Recon:IAMUser/MaliciousIPCaller\.Custom  |  TTPs/Discovery/Recon:IAMUser\-MaliciousIPCaller\.Custom  | 
|  Recon:IAMUser/NetworkPermissions  |  TTPs/Discovery/Recon:IAMUser\-NetworkPermissions,  Unusual Behaviors/User/Recon:IAMUser\-NetworkPermissions  | 
|  Recon:IAMUser/ResourcePermissions  |  TTPs/Discovery/Recon:IAMUser\-ResourcePermissions,  Unusual Behaviors/User/Recon:IAMUser\-ResourcePermissions  | 
|  Recon:IAMUser/TorIPCaller  |  TTPs/Discovery/Recon:IAMUser\-TorIPCaller  | 
|  Recon:IAMUser/UserPermissions  |  TTPs/Discovery/Recon:IAMUser\-UserPermissions, Unusual Behaviors/User/Recon:IAMUser\-UserPermissions  | 
|  ResourceConsumption:IAMUser/ComputeResources  |  Unusual Behaviors/User/ResourceConsumption:IAMUser\-ComputeResources,  Effects/Resource Consumption/ResourceConsumption:IAMUser\-ComputeResources  | 
|  Stealth:IAMUser/CloudTrailLoggingDisabled  |  TTPs/Defense Evasion/Stealth:IAMUser\-CloudTrailLoggingDisabled  | 
|  Stealth:IAMUser/LoggingConfigurationModified  |  TTPs/Defense Evasion/Stealth:IAMUser\-LoggingConfigurationModified,  Unusual Behaviors/User/Stealth:IAMUser\-LoggingConfigurationModified  | 
|  Stealth:IAMUser/PasswordPolicyChange  |  TTPs/Defense Evasion/Stealth:IAMUser\-PasswordPolicyChange  | 
|  UnauthorizedAccess:IAMUser/ConsoleLogin  |  Unusual Behaviors/User/UnauthorizedAccess:IAMUser\-ConsoleLogin  | 
|  UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B  |  TTPs//UnauthorizedAccess:IAMUser\-ConsoleLoginSuccess\.B  | 
|  UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration  |  Effects/Data Exfiltration/UnauthorizedAccess:IAMUser\-InstanceCredentialExfiltration  | 
|  UnauthorizedAccess:IAMUser/MaliciousIPCaller  |  TTPs//UnauthorizedAccess:IAMUser\-MaliciousIPCaller  | 
|  UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom  |  TTPs//UnauthorizedAccess:IAMUser\-MaliciousIPCaller\.Custom  | 
|  UnauthorizedAccess:IAMUser/TorIPCaller  |  TTPs/Command and Control/UnauthorizedAccess:IAMUser\-TorIPCaller  | 
|  Discovery:S3/BucketEnumeration\.Unusual  |  TTPs/Discovery/Recon:S3\-BucketEnumeration, Unusual Behaviours/User/Recon:S3\-BucketEnumeration  | 
|  Discovery:S3/MaliciousIPCaller\.Custom  |  TTPs/Discovery/Recon:S3\-MaliciousIPCaller\.Custom  | 
|  Discovery:S3/TorIPCaller  |  TTPs/Discovery/Recon:S3\-TorIpCaller  | 
|  Exfiltration:S3/ObjectRead\.Unusual  |  Effects/Data Exfiltration/UnauthorizedAccess:S3\-ObjectRead,Unusual Behaviours/User/Data Exfiltration/UnauthorizedAccess:S3\-ObjectRead | 
|  Impact:S3/PermissionsModification\.Unusual  |  TTPs/Permission Escalation/Impact:S3\-PermissionsModification, Unusual Behaviours/User/Permission Escalation/Impact:S3\-PermissionsModification  | 
|  Impact:S3/ObjectDelete\.Unusual  |  Effects/Data Destruction/Impact:S3\-ObjectDelete, Unusual Behaviours/User/Data Destruction/Impact:S3\-ObjectDelete  | 
|  PenTest:S3/KaliLinux  | TTPs/PenTest:S3/KaliLinux | 
|  PenTest:S3/ParrotLinux  |  TTPs/PenTest:S3/ParrotLinux  | 
|  PenTest:S3/PentooLinux  |  TTPs/PenTest:S3/PentoolLinux  | 
|  Policy:S3/AccountBlockPublicAccessDisabled  |  Effects/Data Exposure/Policy:IAMUser\-S3BlockPublicAccessDisabled  | 
|  Policy:S3/BucketBlockPublicAccessDisabled  |  Effects/Data Exposure/Policy:S3\-BucketBlockPublicAccessDisabled  | 
|  Policy:S3/BucketAnonymousAccessGranted  |  Effects/Data Exposure/Policy:S3\-BucketAnonymousAccessGranted  | 
|  Policy:S3/BucketPublicAccessGranted  |  Effects/Data Exposure/Policy:S3\-BucketPublicAccessGranted  | 
|  Stealth:S3/ServerAccessLoggingDisabled  |  Software and Configuration Checks/AWS Security Best Practices/Stealth:IAMUser\-S3ServerAccessLoggingDisabled  | 
|  UnauthorizedAccess:S3/MaliciousIPCaller\.Custom  |  TTPs/UnauthorizedAccess:S3\-MaliciousIPCaller\.Custom  | 
|  UnauthorizedAccess:S3/TorIPCaller  |  TTPs/Command and Control/UnauthorizedAccess:S3\-TorIPCaller  | 

## Typical finding from GuardDuty<a name="securityhub-integration-finding-example"></a>

GuardDuty sends findings to Security Hub using the [AWS Security Finding Format \(ASFF\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html)\.

Here is an example of a typical finding from GuardDuty\.

```
  {
  "SchemaVersion": "2018-10-08",
  "Id": "arn:aws:guardduty:us-east-1:193043430472:detector/d4b040365221be2b54a6264dc9a4bc64/finding/46ba0ac2845071e23ccdeb2ae03bfdea",
  "ProductArn": "arn:aws:securityhub:us-east-1::product/aws/guardduty",
  "GeneratorId": "arn:aws:guardduty:us-east-1:193043430472:detector/d4b040365221be2b54a6264dc9a4bc64",
  "AwsAccountId": "193043430472",
  "Types": [
    "TTPs/Initial Access/UnauthorizedAccess:EC2-SSHBruteForce"
  ],
  "FirstObservedAt": "2020-08-22T09:15:57Z",
  "LastObservedAt": "2020-09-30T11:56:49Z",
  "CreatedAt": "2020-08-22T09:34:34.146Z",
  "UpdatedAt": "2020-09-30T12:14:00.206Z",
  "Severity": {
    "Product": 2,
    "Label": "MEDIUM",
    "Normalized": 40
  },
  "Title": "199.241.229.197 is performing SSH brute force attacks against i-0c10c2c7863d1a356.",
  "Description": "199.241.229.197 is performing SSH brute force attacks against i-0c10c2c7863d1a356. Brute force attacks are used to gain unauthorized access to your instance by guessing the SSH password.",
  "SourceUrl": "https://us-east-1.console.aws.amazon.com/guardduty/home?region=us-east-1#/findings?macros=current&fId=46ba0ac2845071e23ccdeb2ae03bfdea",
  "ProductFields": {
    "aws/guardduty/service/action/networkConnectionAction/remotePortDetails/portName": "Unknown",
    "aws/guardduty/service/archived": "false",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/organization/asnOrg": "CENTURYLINK-US-LEGACY-QWEST",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/geoLocation/lat": "42.5122",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/ipAddressV4": "199.241.229.197",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/geoLocation/lon": "-90.7384",
    "aws/guardduty/service/action/networkConnectionAction/blocked": "false",
    "aws/guardduty/service/action/networkConnectionAction/remotePortDetails/port": "46717",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/country/countryName": "United States",
    "aws/guardduty/service/serviceName": "guardduty",
    "aws/guardduty/service/evidence": "",
    "aws/guardduty/service/action/networkConnectionAction/localIpDetails/ipAddressV4": "172.31.43.6",
    "aws/guardduty/service/detectorId": "d4b040365221be2b54a6264dc9a4bc64",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/organization/org": "CenturyLink",
    "aws/guardduty/service/action/networkConnectionAction/connectionDirection": "INBOUND",
    "aws/guardduty/service/eventFirstSeen": "2020-08-22T09:15:57Z",
    "aws/guardduty/service/eventLastSeen": "2020-09-30T11:56:49Z",
    "aws/guardduty/service/action/networkConnectionAction/localPortDetails/portName": "SSH",
    "aws/guardduty/service/action/actionType": "NETWORK_CONNECTION",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/city/cityName": "Dubuque",
    "aws/guardduty/service/additionalInfo": "",
    "aws/guardduty/service/resourceRole": "TARGET",
    "aws/guardduty/service/action/networkConnectionAction/localPortDetails/port": "22",
    "aws/guardduty/service/action/networkConnectionAction/protocol": "TCP",
    "aws/guardduty/service/count": "74",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/organization/asn": "209",
    "aws/guardduty/service/action/networkConnectionAction/remoteIpDetails/organization/isp": "CenturyLink",
    "aws/securityhub/FindingId": "arn:aws:securityhub:us-east-1::product/aws/guardduty/arn:aws:guardduty:us-east-1:193043430472:detector/d4b040365221be2b54a6264dc9a4bc64/finding/46ba0ac2845071e23ccdeb2ae03bfdea",
    "aws/securityhub/ProductName": "GuardDuty",
    "aws/securityhub/CompanyName": "Amazon"
  },
  "Resources": [
    {
      "Type": "AwsEc2Instance",
      "Id": "arn:aws:ec2:us-east-1:193043430472:instance/i-0c10c2c7863d1a356",
      "Partition": "aws",
      "Region": "us-east-1",
      "Tags": {
        "Name": "kubectl"
      },
      "Details": {
        "AwsEc2Instance": {
          "Type": "t2.micro",
          "ImageId": "ami-02354e95b39ca8dec",
          "IpV4Addresses": [
            "18.234.130.16",
            "172.31.43.6"
          ],
          "VpcId": "vpc-a0c2d7c7",
          "SubnetId": "subnet-4975b475",
          "LaunchedAt": "2020-08-03T23:21:57Z"
        }
      }
    }
  ],
  "WorkflowState": "NEW",
  "Workflow": {
    "Status": "NEW"
  },
  "RecordState": "ACTIVE"
}
```

## Enabling and configuring the integration<a name="securityhub-integration-enable"></a>

To use the integration with AWS Security Hub, you must enable Security Hub\. For information on how to enable Security Hub, see [Setting up Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html) in the *AWS Security Hub User Guide*\.

When you enable both GuardDuty and Security Hub, the integration is enabled automatically\. GuardDuty immediately begins to send findings to Security Hub\.

## How to stop sending findings<a name="securityhub-integration-disable"></a>

To stop sending findings to Security Hub, you can use either the Security Hub console or the API\.

See [Disabling and enabling the flow of findings from an integration \(console\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-integrations-managing.html#securityhub-integration-findings-flow-console) or [Disabling the flow of findings from an integration \(Security Hub API, AWS CLI\)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-integrations-managing.html#securityhub-integration-findings-flow-disable-api) in the *AWS Security Hub User Guide*\.