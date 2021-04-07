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
| [Backdoor:EC2/C&CActivity\.B](guardduty_finding-types-ec2.md#backdoor-ec2-ccactivityb) | Backdoor | EC2 | High | 
| [Backdoor:EC2/C&CActivity\.B\!DNS](guardduty_finding-types-ec2.md#backdoor-ec2-ccactivitybdns) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.Dns](guardduty_finding-types-ec2.md#backdoor-ec2-denialofservicedns) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.Tcp](guardduty_finding-types-ec2.md#backdoor-ec2-denialofservicetcp) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.Udp](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceudp) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.UdpOnTcpPorts](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceudpontcpports) | Backdoor | EC2 | High | 
| [Backdoor:EC2/DenialOfService\.UnusualProtocol](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceunusualprotocol) | Backdoor | EC2 | High | 
| [Backdoor:EC2/Spambot](guardduty_finding-types-ec2.md#backdoor-ec2-spambot) | Backdoor | EC2 | Medium | 
| [Behavior:EC2/NetworkPortUnusual](guardduty_finding-types-ec2.md#behavior-ec2-networkportunusual) | Behavior | EC2 | Medium | 
| [Behavior:EC2/TrafficVolumeUnusual](guardduty_finding-types-ec2.md#behavior-ec2-trafficvolumeunusual) | Behavior | EC2 | Medium | 
| [CredentialAccess:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#credentialaccess-iam-anomalousbehavior) | CredentialAccess | IAM | Medium | 
| [CryptoCurrency:EC2/BitcoinTool\.B](guardduty_finding-types-ec2.md#cryptocurrency-ec2-bitcointoolb) | CryptoCurrency | EC2 | High | 
| [CryptoCurrency:EC2/BitcoinTool\.B\!DNS](guardduty_finding-types-ec2.md#cryptocurrency-ec2-bitcointoolbdns) | CryptoCurrency | EC2 | High | 
| [DefenseEvasion:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#defenseevasion-iam-anomalousbehavior) | DefenseEvasion | IAM | Medium | 
| [Discovery:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#discovery-iam-anomalousbehavior) | Discovery | IAM | Low | 
| [Discovery:S3/MaliciousIPCaller](guardduty_finding-types-s3.md#discovery-s3-maliciousipcaller) | Discovery | S3 | High | 
| [Discovery:S3/MaliciousIPCaller\.Custom](guardduty_finding-types-s3.md#discovery-s3-maliciousipcallercustom) | Discovery | S3 | High | 
| [Discovery:S3/TorIPCaller](guardduty_finding-types-s3.md#discovery-s3-toripcaller) | Discovery | S3 | Medium | 
| [Exfiltration:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#exfiltration-iam-anomalousbehavior) | Exfiltration | IAM | High | 
| [Exfiltration:S3/MaliciousIPCaller](guardduty_finding-types-s3.md#exfiltration-s3-maliciousipcaller) | Exfiltration | S3 | High | 
| [Exfiltration:S3/ObjectRead\.Unusual](guardduty_finding-types-s3.md#exfiltration-s3-objectreadunusual) | Exfiltration | S3 | Medium\* | 
| [Impact:EC2/AbusedDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-abuseddomainrequestreputation) | Impact | EC2 | Medium | 
| [Impact:EC2/BitcoinDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-bitcoindomainrequestreputation) | Impact | EC2 | High | 
| [Impact:EC2/MaliciousDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-maliciousdomainrequestreputation) | Impact | EC2 | High | 
| [Impact:EC2/PortSweep](guardduty_finding-types-ec2.md#impact-ec2-portsweep) | Impact | EC2 | High | 
| [Impact:EC2/SuspiciousDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-suspiciousdomainrequestreputation) | Impact | EC2 | Low | 
| [Impact:EC2/WinRMBruteForce](guardduty_finding-types-ec2.md#impact-ec2-winrmbruteforce) | Impact | EC2 | Low\* | 
| [Impact:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#impact-iam-anomalousbehavior) | Impact | IAM | High | 
| [Impact:S3/MaliciousIPCaller](guardduty_finding-types-s3.md#impact-s3-maliciousipcaller) | Impact | S3 | High | 
| [InitialAccess:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#initialaccess-iam-anomalousbehavior) | InitialAccess | IAM | Medium | 
| [PenTest:IAMUser/KaliLinux](guardduty_finding-types-iam.md#pentest-iam-kalilinux) | PenTest | IAM | Medium | 
| [PenTest:IAMUser/ParrotLinux](guardduty_finding-types-iam.md#pentest-iam-parrotlinux) | PenTest | IAM | Medium | 
| [PenTest:IAMUser/PentooLinux](guardduty_finding-types-iam.md#pentest-iam-pentoolinux) | PenTest | IAM | Medium | 
| [PenTest:S3/KaliLinux](guardduty_finding-types-s3.md#pentest-s3-kalilinux) | PenTest | S3 | Medium | 
| [PenTest:S3/ParrotLinux](guardduty_finding-types-s3.md#pentest-s3-parrotlinux) | PenTest | S3 | Medium | 
| [PenTest:S3/PentooLinux](guardduty_finding-types-s3.md#pentest-s3-pentoolinux) | PenTest | S3 | Medium | 
| [Persistence:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#persistence-iam-anomalousbehavior) | Persistence | IAM | Medium | 
| [Policy:IAMUser/RootCredentialUsage](guardduty_finding-types-iam.md#policy-iam-rootcredentialusage) | Policy | IAM | Low | 
| [Policy:S3/AccountBlockPublicAccessDisabled](guardduty_finding-types-s3.md#policy-s3-accountblockpublicaccessdisabled) | Policy | S3 | Low | 
| [Policy:S3/BucketAnonymousAccessGranted](guardduty_finding-types-s3.md#policy-s3-bucketanonymousaccessgranted) | Policy | S3 | High | 
| [Policy:S3/BucketBlockPublicAccessDisabled](guardduty_finding-types-s3.md#policy-s3-bucketblockpublicaccessdisabled) | Policy | S3 | Low | 
| [Policy:S3/BucketPublicAccessGranted](guardduty_finding-types-s3.md#policy-s3-bucketpublicaccessgranted) | Policy | S3 | High | 
| [PrivilegeEscalation:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#privilegeescalation-iam-anomalousbehavior) | PrivilegeEscalation | IAM | Medium | 
| [Recon:EC2/PortProbeEMRUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeemrunprotectedport) | Recon | EC2 | High | 
| [Recon:EC2/PortProbeUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeunprotectedport) | Recon | EC2 | Low\* | 
| [Recon:EC2/Portscan](guardduty_finding-types-ec2.md#recon-ec2-portscan) | Recon | EC2 | Medium | 
| [Recon:IAMUser/MaliciousIPCaller](guardduty_finding-types-iam.md#recon-iam-maliciousipcaller) | Recon | IAM | Medium | 
| [Recon:IAMUser/MaliciousIPCaller\.Custom](guardduty_finding-types-iam.md#recon-iam-maliciousipcallercustom) | Recon | IAM | Medium | 
| [Recon:IAMUser/TorIPCaller](guardduty_finding-types-iam.md#recon-iam-toripcaller) | Recon | IAM | Medium | 
| [Stealth:IAMUser/CloudTrailLoggingDisabled](guardduty_finding-types-iam.md#stealth-iam-cloudtrailloggingdisabled) | Stealth | IAM | Low | 
| [Stealth:IAMUser/PasswordPolicyChange](guardduty_finding-types-iam.md#stealth-iam-passwordpolicychange) | Stealth | IAM | Low | 
| [Stealth:S3/ServerAccessLoggingDisabled](guardduty_finding-types-s3.md#stealth-s3-serveraccessloggingdisabled) | Stealth | S3 | Low | 
| [Trojan:EC2/BlackholeTraffic](guardduty_finding-types-ec2.md#trojan-ec2-blackholetraffic) | Trojan | EC2 | Medium | 
| [Trojan:EC2/BlackholeTraffic\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-blackholetrafficdns) | Trojan | EC2 | Medium | 
| [Trojan:EC2/DGADomainRequest\.B](guardduty_finding-types-ec2.md#trojan-ec2-dgadomainrequestb) | Trojan | EC2 | High | 
| [Trojan:EC2/DGADomainRequest\.C\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-dgadomainrequestcdns) | Trojan | EC2 | High | 
| [Trojan:EC2/DNSDataExfiltration](guardduty_finding-types-ec2.md#trojan-ec2-dnsdataexfiltration) | Trojan | EC2 | High | 
| [Trojan:EC2/DriveBySourceTraffic\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-drivebysourcetrafficdns) | Trojan | EC2 | Medium | 
| [Trojan:EC2/DropPoint](guardduty_finding-types-ec2.md#trojan-ec2-droppoint) | Trojan | EC2 | Medium | 
| [Trojan:EC2/DropPoint\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-droppointdns) | Trojan | EC2 | Medium | 
| [Trojan:EC2/PhishingDomainRequest\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-phishingdomainrequestdns) | Trojan | EC2 | High | 
| [UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-maliciousipcallercustom) | UnauthorizedAccess | EC2 | Medium | 
| [UnauthorizedAccess:EC2/MetadataDNSRebind](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-metadatadnsrebind) | UnauthorizedAccess | EC2 | High | 
| [UnauthorizedAccess:EC2/RDPBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-rdpbruteforce) | UnauthorizedAccess | EC2 | Low\* | 
| [UnauthorizedAccess:EC2/SSHBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-sshbruteforce) | UnauthorizedAccess | EC2 | Low\* | 
| [UnauthorizedAccess:EC2/TorClient](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-torclient) | UnauthorizedAccess | EC2 | High | 
| [UnauthorizedAccess:EC2/TorRelay](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-torrelay) | UnauthorizedAccess | EC2 | High | 
| [UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](guardduty_finding-types-iam.md#unauthorizedaccess-iam-consoleloginsuccessb) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration](guardduty_finding-types-iam.md#unauthorizedaccess-iam-instancecredentialexfiltration) | UnauthorizedAccess | IAM | High | 
| [UnauthorizedAccess:IAMUser/MaliciousIPCaller](guardduty_finding-types-iam.md#unauthorizedaccess-iam-maliciousipcaller) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](guardduty_finding-types-iam.md#unauthorizedaccess-iam-maliciousipcallercustom) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:IAMUser/TorIPCaller](guardduty_finding-types-iam.md#unauthorizedaccess-iam-toripcaller) | UnauthorizedAccess | IAM | Medium | 
| [UnauthorizedAccess:S3/MaliciousIPCaller\.Custom](guardduty_finding-types-s3.md#unauthorizedaccess-s3-maliciousipcallercustom) | UnauthorizedAccess | S3 | High | 
| [UnauthorizedAccess:S3/TorIPCaller](guardduty_finding-types-s3.md#unauthorizedaccess-s3-toripcaller) | UnauthorizedAccess | S3 | High | 