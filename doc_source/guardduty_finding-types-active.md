# Finding types<a name="guardduty_finding-types-active"></a>

For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document history for Amazon GuardDuty](doc-history.md)\.

For information about retired finding types see [Retired finding types](guardduty_finding-types-retired.md)\.

## Findings by resource type<a name="findings-by-resource"></a>

The following pages are broken down by each resource type GuardDuty currently generates findings for\. The pages contain detailed information on all finding types for that resources type\.
+ [EC2 finding types](guardduty_finding-types-ec2.md)
+ [IAM finding types](guardduty_finding-types-iam.md)
+ [S3 finding types](guardduty_finding-types-s3.md)

## Findings table<a name="findings-table"></a>

The following table lists all finding types by name, threat purpose, resource and severity\. A severity listed with an asterisk \(\*\) indicates the finding has variable severities depending the circumstances of the finding, which are described in the details for that finding\. Choose the finding name to open more info about that finding\. 


|  FINDING TYPE  |  THREAT PURPOSE  |  RESOURCE  |  SEVERITY  | 
| --- | --- | --- | --- | 
| [Backdoor:EC2/C&CActivity\.B\!DNS](guardduty_finding-types-ec2.md#backdoor-ec2-ccactivitybdns) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.Dns](guardduty_finding-types-ec2.md#backdoor-ec2-denialofservicedns) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.Tcp](guardduty_finding-types-ec2.md#backdoor-ec2-denialofservicetcp) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.Udp](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceudp) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.UdpOnTcpPorts](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceudpontcpports) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.UnusualProtocol](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceunusualprotocol) | Backdoor | EC2 | High | 
| [Backdoor:EC2/Spambot](guardduty_finding-types-ec2.md#backdoor-ec2-spambot) | Backdoor | EC2 | Medium | 
| [Behavior:EC2/NetworkPortUnusual](guardduty_finding-types-ec2.md#behavior-ec2-networkportunusual) | Behavior | EC2 | Medium | 
| [Behavior:EC2/TrafficVolumeUnusual](guardduty_finding-types-ec2.md#behavior-ec2-trafficvolumeunusual) | Behavior | EC2 | Medium | 
| [CryptoCurrency:EC2/BitcoinTool\.B](guardduty_finding-types-ec2.md#cryptocurrency-ec2-bitcointoolb) | CryptoCurrency | EC2 | High | 
| [CryptoCurrency:EC2/BitcoinTool\.B\!DNS](guardduty_finding-types-ec2.md#cryptocurrency-ec2-bitcointoolbdns) | CryptoCurrency | EC2 | High | 
| [Discovery:S3/BucketEnumeration\.Unusual](guardduty_finding-types-s3.md#discovery-s3-bucketenumerationunusual) | Discovery | S3 | Medium | 
| [Discovery:S3/MaliciousIPCaller\.Custom](guardduty_finding-types-s3.md#discovery-s3-maliciousipcallercustom) | Discovery | S3 | Medium | 
| [Discovery:S3/TorIPCaller](guardduty_finding-types-s3.md#discovery-s3-toripcaller) | Discovery | S3 | Medium | 
| [Exfiltration:S3/ObjectRead\.Unusual](guardduty_finding-types-s3.md#exfiltration-s3-objectreadunusual) | Exfiltration | S3 | Medium | 
| [Impact:S3/PermissionsModification\.Unusual](guardduty_finding-types-s3.md#impact-s3-permissionsmodificationunusual) | Impact | S3 | Medium | 
| [Impact:S3/ObjectDelete\.Unusual](guardduty_finding-types-s3.md#impact-s3-objectdeleteunusual) | Impact | S3 | Medium | 
| [PenTest:IAMUser/KaliLinux](guardduty_finding-types-iam.md#pentest-iam-kalilinux) | PenTest | IAM | Medium | 
| [PenTest:IAMUser/ParrotLinux](guardduty_finding-types-iam.md#pentest-iam-parrotlinux) | PenTest | IAM | Medium | 
| [PenTest:IAMUser/PentooLinux](guardduty_finding-types-iam.md#pentest-iam-pentoolinux) | PenTest | IAM | Medium | 
| [PenTest:S3/KaliLinux](guardduty_finding-types-s3.md#pentest-s3-kalilinux) | PenTest | S3 | Medium | 
| [PenTest:S3/ParrotLinux](guardduty_finding-types-s3.md#pentest-s3-parrotlinux) | PenTest | S3 | Medium | 
| [PenTest:S3/PentooLinux](guardduty_finding-types-s3.md#pentest-s3-pentoolinux) | PenTest | S3 | Medium | 
| [Persistence:IAMUser/NetworkPermissions](guardduty_finding-types-iam.md#persistence-iam-networkpermissions) | Persistence | IAM | Medium\* | 
| [Persistence:IAMUser/ResourcePermissions](guardduty_finding-types-iam.md#persistence-iam-resourcepermissions) | Persistence | IAM | Medium\* | 
| [Persistence:IAMUser/UserPermissions](guardduty_finding-types-iam.md#persistence-iam-userpermissions) | Persistence | IAM | Medium\* | 
| [Policy:IAMUser/RootCredentialUsage](guardduty_finding-types-iam.md#policy-iam-rootcredentialusage) | Policy | IAM | Low | 
| [Policy:S3/AccountBlockPublicAccessDisabled](guardduty_finding-types-s3.md#policy-s3-accountblockpublicaccessdisabled) | Policy | S3 | Low | 
| [Policy:S3/BucketBlockPublicAccessDisabled](guardduty_finding-types-s3.md#policy-s3-bucketblockpublicaccessdisabled) | Policy | S3 | Low | 
| [Policy:S3/BucketAnonymousAccessGranted](guardduty_finding-types-s3.md#policy-s3-bucketanonymousaccessgranted) | Policy | S3 | High | 
| [Policy:S3/BucketPublicAccessGranted](guardduty_finding-types-s3.md#policy-s3-bucketpublicaccessgranted) | Policy | S3 | High | 
| [PrivilegeEscalation:IAMUser/AdministrativePermissions](guardduty_finding-types-iam.md#privilegeescalation-iam-administrativepermissions) | PrivilegeEscalation | IAM | Low\* | 
| [Recon:EC2/PortProbeEMRUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeemrunprotectedport) | Recon | EC2 | High | 
| [Recon:EC2/PortProbeUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeunprotectedport) | Recon | EC2 | Low\* | 
| [Recon:EC2/Portscan](guardduty_finding-types-ec2.md#recon-ec2-portscan) | Recon | EC2 | Medium | 
| [Recon:IAMUser/MaliciousIPCaller](guardduty_finding-types-iam.md#recon-iam-maliciousipcaller) | Recon | IAM | Medium | 
| [Recon:IAMUser/MaliciousIPCaller\.Custom](guardduty_finding-types-iam.md#recon-iam-maliciousipcallercustom) | Recon | IAM | Medium | 
| [Recon:IAMUser/NetworkPermissions](guardduty_finding-types-iam.md#recon-iam-networkpermissions) | Recon | IAM | Medium\* | 
| [Recon:IAMUser/ResourcePermissions](guardduty_finding-types-iam.md#recon-iam-resourcepermissions) | Recon | IAM | Medium\* | 
| [Recon:IAMUser/TorIPCaller](guardduty_finding-types-iam.md#recon-iam-toripcaller) | Recon | IAM | Medium | 
| [Recon:IAMUser/UserPermissions](guardduty_finding-types-iam.md#recon-iam-userpermissions) | Recon | IAM | Medium\* | 
| [ResourceConsumption:IAMUser/ComputeResources](guardduty_finding-types-iam.md#resourceconsumption-iam-computeresources) | ResourceConsumption | IAM | Medium\* | 
| [Stealth:IAMUser/CloudTrailLoggingDisabled](guardduty_finding-types-iam.md#stealth-iam-cloudtrailloggingdisabled) | Stealth | IAM | Low | 
| [Stealth:IAMUser/LoggingConfigurationModified](guardduty_finding-types-iam.md#stealth-iam-loggingconfigurationmodified) | Stealth | IAM | Medium\* | 
| [Stealth:IAMUser/PasswordPolicyChange](guardduty_finding-types-iam.md#stealth-iam-passwordpolicychange) | Stealth | IAM | Low | 
| [Stealth:S3/ServerAccessLoggingDisabled](guardduty_finding-types-s3.md#stealth-s3-serveraccessloggingdisabled) | Stealth | S3 | Low | 
| [Trojan:EC2/BlackholeTraffic](guardduty_finding-types-ec2.md#trojan-ec2-blackholetraffic) | Trojan | EC2 | Medium | 
| [Trojan:EC2/BlackholeTraffic\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-blackholetrafficdns) | Trojan | EC2 | Medium | 
| [Trojan:EC2/DGADomainRequest\.B](guardduty_finding-types-ec2.md#trojan-ec2-dgadomainrequestb) | Trojan | EC2 | High | 
| [Trojan:EC2/DGADomainRequest\.C\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-dgadomainrequestcdns) | Trojan | EC2 | High | 
| [Trojan:EC2/DNSDataExfiltration](guardduty_finding-types-ec2.md#trojan-ec2-dnsdataexfiltration) | Trojan | EC2 | High | 
| [Trojan:EC2/DriveBySourceTraffic\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-drivebysourcetrafficdns) | Trojan | EC2 | Medium | 
| [Trojan:EC2/DropPoint](guardduty_finding-types-ec2.md#trojan-ec2-droppoint) | Trojan | EC2 | Medium | 
| [Trojan:EC2/DropPoint\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-droppointdns) | Trojan | EC2 | High | 
| [Trojan:EC2/PhishingDomainRequest\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-phishingdomainrequestdns) | Trojan | EC2 | High | 
| [UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-maliciousipcallercustom) | UnauthorizedAccess | EC2 | Medium | 
| [UnauthorizedAccess:EC2/MetadataDNSRebind](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-metadatadnsrebind) | UnauthorizedAccess | EC2 | High | 
| [UnauthorizedAccess:EC2/RDPBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-rdpbruteforce) | UnauthorizedAccess | EC2 | Low\* | 
| [UnauthorizedAccess:EC2/SSHBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-sshbruteforce) | UnauthorizedAccess | EC2 | Low\* | 
| [UnauthorizedAccess:EC2/TorClient](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-torclient) | UnauthorizedAccess | EC2 | High | 
| [UnauthorizedAccess:EC2/TorIPCaller](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-toripcaller) | UnauthorizedAccess | EC2 | Medium | 
| [UnauthorizedAccess:EC2/TorRelay](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-torrelay) | UnauthorizedAccess | EC2 | High | 
| [UnauthorizedAccess:IAMUser/ConsoleLogin](guardduty_finding-types-iam.md#unauthorizedaccess-iam-consolelogin) | UnauthorizedAccess | IAM | Medium\* | 
| [UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](guardduty_finding-types-iam.md#unauthorizedaccess-iam-consoleloginsuccessb) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](guardduty_finding-types-iam.md#unauthorizedaccess-iam-instancecredentialexfiltration) | UnauthorizedAccess | IAM | High | 
| [UnauthorizedAccess:IAMUser/MaliciousIPCaller](guardduty_finding-types-iam.md#unauthorizedaccess-iam-maliciousipcaller) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](guardduty_finding-types-iam.md#unauthorizedaccess-iam-maliciousipcallercustom) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:IAMUser/TorIPCaller](guardduty_finding-types-iam.md#unauthorizedaccess-iam-toripcaller) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:S3/TorIPCaller](guardduty_finding-types-s3.md#unauthorizedaccess-s3-toripcaller) | UnauthorizedAccess | S3 | High | 

