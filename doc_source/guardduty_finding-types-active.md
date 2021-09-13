# Finding types<a name="guardduty_finding-types-active"></a>

For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document history for Amazon GuardDuty](doc-history.md)\.

For information about retired finding types see [Retired finding types](guardduty_finding-types-retired.md)\.

## Findings by resource type<a name="findings-by-resource"></a>

The following pages are broken down by each resource type GuardDuty currently generates findings for\. The pages contain detailed information on all finding types for that resources type\.
+ [EC2 finding types](guardduty_finding-types-ec2.md)
+ [IAM finding types](guardduty_finding-types-iam.md)
+ [S3 finding types](guardduty_finding-types-s3.md)

## Findings table<a name="findings-table"></a>

The following table lists all finding types by name, resource, data source and severity\. A severity listed with an asterisk \(\*\) indicates the finding has variable severities depending the circumstances of the finding, which are described in the details for that finding\. Choose the finding name to open more info about that finding\. 


|  FINDING TYPE  |  RESOURCE  |  DATA SOURCE  |  SEVERITY  | 
| --- | --- | --- | --- | 
| **[Backdoor:EC2/C&CActivity\.B](guardduty_finding-types-ec2.md#backdoor-ec2-ccactivityb)** | EC2 | VPC Flow Logs | High | 
| **[Backdoor:EC2/C&CActivity\.B\!DNS](guardduty_finding-types-ec2.md#backdoor-ec2-ccactivitybdns)** | EC2 | DNS logs | High | 
| **[Backdoor:EC2/DenialOfService\.Dns](guardduty_finding-types-ec2.md#backdoor-ec2-denialofservicedns)** | EC2 | VPC Flow Logs | High | 
| **[Backdoor:EC2/DenialOfService\.Tcp](guardduty_finding-types-ec2.md#backdoor-ec2-denialofservicetcp)** | EC2 | VPC Flow Logs | High | 
| **[Backdoor:EC2/DenialOfService\.Udp](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceudp)** | EC2 | VPC Flow Logs | High | 
| **[Backdoor:EC2/DenialOfService\.UdpOnTcpPorts](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceudpontcpports)** | EC2 | VPC Flow Logs | High | 
| **[Backdoor:EC2/DenialOfService\.UnusualProtocol](guardduty_finding-types-ec2.md#backdoor-ec2-denialofserviceunusualprotocol)** | EC2 | VPC Flow Logs | High | 
| **[Backdoor:EC2/Spambot](guardduty_finding-types-ec2.md#backdoor-ec2-spambot)** | EC2 | VPC Flow Logs | Medium | 
| **[Behavior:EC2/NetworkPortUnusual](guardduty_finding-types-ec2.md#behavior-ec2-networkportunusual)** | EC2 | VPC Flow Logs | Medium | 
| **[Behavior:EC2/TrafficVolumeUnusual](guardduty_finding-types-ec2.md#behavior-ec2-trafficvolumeunusual)** | EC2 | VPC Flow Logs | Medium | 
| **[CredentialAccess:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#credentialaccess-iam-anomalousbehavior)** | IAM | CloudTrail management event | Medium | 
| **[CryptoCurrency:EC2/BitcoinTool\.B](guardduty_finding-types-ec2.md#cryptocurrency-ec2-bitcointoolb)** | EC2 | VPC Flow Logs | High | 
| **[CryptoCurrency:EC2/BitcoinTool\.B\!DNS](guardduty_finding-types-ec2.md#cryptocurrency-ec2-bitcointoolbdns)** | EC2 | DNS logs | High | 
| **[DefenseEvasion:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#defenseevasion-iam-anomalousbehavior)** | IAM | CloudTrail management event | Medium | 
| **[Discovery:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#discovery-iam-anomalousbehavior)** | IAM | CloudTrail management event | Low | 
| **[Discovery:S3/MaliciousIPCaller](guardduty_finding-types-s3.md#discovery-s3-maliciousipcaller)** | S3 | CloudTrail S3 data event | High | 
| **[Discovery:S3/MaliciousIPCaller\.Custom](guardduty_finding-types-s3.md#discovery-s3-maliciousipcallercustom)** | S3 | CloudTrail S3 data event | High | 
| **[Discovery:S3/TorIPCaller](guardduty_finding-types-s3.md#discovery-s3-toripcaller)** | S3 | CloudTrail S3 data event | Medium | 
| **[Exfiltration:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#exfiltration-iam-anomalousbehavior)** | IAM | CloudTrail management event | High | 
| **[Exfiltration:S3/MaliciousIPCaller](guardduty_finding-types-s3.md#exfiltration-s3-maliciousipcaller)** | S3 | CloudTrail S3 data event | High | 
| **[Exfiltration:S3/ObjectRead\.Unusual](guardduty_finding-types-s3.md#exfiltration-s3-objectreadunusual)** | S3 | S3 CloudTrail data event | Medium\* | 
| **[Impact:EC2/AbusedDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-abuseddomainrequestreputation)** | EC2 | DNS logs | Medium | 
| **[Impact:EC2/BitcoinDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-bitcoindomainrequestreputation)** | EC2 | DNS logs | High | 
| **[Impact:EC2/MaliciousDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-maliciousdomainrequestreputation)** | EC2 | DNS logs | High | 
| **[Impact:EC2/PortSweep](guardduty_finding-types-ec2.md#impact-ec2-portsweep)** | EC2 | VPC Flow Logs | High | 
| **[Impact:EC2/SuspiciousDomainRequest\.Reputation](guardduty_finding-types-ec2.md#impact-ec2-suspiciousdomainrequestreputation)** | EC2 | DNS logs | Low | 
| **[Impact:EC2/WinRMBruteForce](guardduty_finding-types-ec2.md#impact-ec2-winrmbruteforce)** | EC2 | VPC Flow Logs | Low\* | 
| **[Impact:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#impact-iam-anomalousbehavior)** | IAM | CloudTrail management event | High | 
| **[Impact:S3/MaliciousIPCaller](guardduty_finding-types-s3.md#impact-s3-maliciousipcaller)** | S3 | CloudTrail S3 data event | High | 
| **[InitialAccess:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#initialaccess-iam-anomalousbehavior)** | IAM | CloudTrail management event | Medium | 
| **[PenTest:IAMUser/KaliLinux](guardduty_finding-types-iam.md#pentest-iam-kalilinux)** | IAM | CloudTrail management event | Medium | 
| **[PenTest:IAMUser/ParrotLinux](guardduty_finding-types-iam.md#pentest-iam-parrotlinux)** | IAM | CloudTrail management event | Medium | 
| **[PenTest:IAMUser/PentooLinux](guardduty_finding-types-iam.md#pentest-iam-pentoolinux)** | IAM | CloudTrail management event | Medium | 
| **[PenTest:S3/KaliLinux](guardduty_finding-types-s3.md#pentest-s3-kalilinux)** | S3 | CloudTrail S3 data event | Medium | 
| **[PenTest:S3/ParrotLinux](guardduty_finding-types-s3.md#pentest-s3-parrotlinux)** | S3 | CloudTrail S3 data event | Medium | 
| **[PenTest:S3/PentooLinux](guardduty_finding-types-s3.md#pentest-s3-pentoolinux)** | S3 | CloudTrail S3 data event | Medium | 
| **[Persistence:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#persistence-iam-anomalousbehavior)** | IAM | CloudTrail management event | Medium | 
| **[Policy:IAMUser/RootCredentialUsage](guardduty_finding-types-iam.md#policy-iam-rootcredentialusage)** | IAM | CloudTrail management event or CloudTrail data event | Low | 
| **[Policy:S3/AccountBlockPublicAccessDisabled](guardduty_finding-types-s3.md#policy-s3-accountblockpublicaccessdisabled)** | S3 | CloudTrail management event | Low | 
| **[Policy:S3/BucketAnonymousAccessGranted](guardduty_finding-types-s3.md#policy-s3-bucketanonymousaccessgranted)** | S3 | CloudTrail management event | High | 
| **[Policy:S3/BucketBlockPublicAccessDisabled](guardduty_finding-types-s3.md#policy-s3-bucketblockpublicaccessdisabled)** | S3 | CloudTrail management event | Low | 
| **[Policy:S3/BucketPublicAccessGranted](guardduty_finding-types-s3.md#policy-s3-bucketpublicaccessgranted)** | S3 | CloudTrail management event | High | 
| **[PrivilegeEscalation:IAMUser/AnomalousBehavior](guardduty_finding-types-iam.md#privilegeescalation-iam-anomalousbehavior)** | IAM | CloudTrail management event | Medium | 
| **[Recon:EC2/PortProbeEMRUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeemrunprotectedport)** | EC2 | VPC Flow Logs | High | 
| **[Recon:EC2/PortProbeUnprotectedPort](guardduty_finding-types-ec2.md#recon-ec2-portprobeunprotectedport)** | EC2 | VPC Flow Logs | Low\* | 
| **[Recon:EC2/Portscan](guardduty_finding-types-ec2.md#recon-ec2-portscan)** | EC2 | VPC Flow Logs | Medium | 
| **[Recon:IAMUser/MaliciousIPCaller](guardduty_finding-types-iam.md#recon-iam-maliciousipcaller)** | IAM | CloudTrail management event | Medium | 
| **[Recon:IAMUser/MaliciousIPCaller\.Custom](guardduty_finding-types-iam.md#recon-iam-maliciousipcallercustom)** | IAM | CloudTrail management event | Medium | 
| **[Recon:IAMUser/TorIPCaller](guardduty_finding-types-iam.md#recon-iam-toripcaller)** | IAM | CloudTrail management event | Medium | 
| **[Stealth:IAMUser/CloudTrailLoggingDisabled](guardduty_finding-types-iam.md#stealth-iam-cloudtrailloggingdisabled)** | IAM | CloudTrail management event | Low | 
| **[Stealth:IAMUser/PasswordPolicyChange](guardduty_finding-types-iam.md#stealth-iam-passwordpolicychange)** | IAM | CloudTrail management event | Low | 
| **[Stealth:S3/ServerAccessLoggingDisabled](guardduty_finding-types-s3.md#stealth-s3-serveraccessloggingdisabled)** | S3 | CloudTrail management event | Low | 
| **[Trojan:EC2/BlackholeTraffic](guardduty_finding-types-ec2.md#trojan-ec2-blackholetraffic)** | EC2 | VPC Flow Logs | Medium | 
| **[Trojan:EC2/BlackholeTraffic\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-blackholetrafficdns)** | EC2 | DNS logs | Medium | 
| **[Trojan:EC2/DGADomainRequest\.B](guardduty_finding-types-ec2.md#trojan-ec2-dgadomainrequestb)** | EC2 | DNS logs | High | 
| **[Trojan:EC2/DGADomainRequest\.C\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-dgadomainrequestcdns)** | EC2 | DNS logs | High | 
| **[Trojan:EC2/DNSDataExfiltration](guardduty_finding-types-ec2.md#trojan-ec2-dnsdataexfiltration)** | EC2 | DNS logs | High | 
| **[Trojan:EC2/DriveBySourceTraffic\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-drivebysourcetrafficdns)** | EC2 | DNS logs | High | 
| **[Trojan:EC2/DropPoint](guardduty_finding-types-ec2.md#trojan-ec2-droppoint)** | EC2 | VPC Flow Logs | Medium | 
| **[Trojan:EC2/DropPoint\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-droppointdns)** | EC2 | DNS logs | Medium | 
| **[Trojan:EC2/PhishingDomainRequest\!DNS](guardduty_finding-types-ec2.md#trojan-ec2-phishingdomainrequestdns)** | EC2 | DNS logs | High | 
| **[UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-maliciousipcallercustom)** | EC2 | VPC Flow Logs | Medium | 
| **[UnauthorizedAccess:EC2/MetadataDNSRebind](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-metadatadnsrebind)** | EC2 | DNS logs | High | 
| **[UnauthorizedAccess:EC2/RDPBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-rdpbruteforce)** | EC2 | VPC Flow Logs | Low\* | 
| **[UnauthorizedAccess:EC2/SSHBruteForce](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-sshbruteforce)** | EC2 | VPC Flow Logs | Low\* | 
| **[UnauthorizedAccess:EC2/TorClient](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-torclient)** | EC2 | VPC Flow Logs | High | 
| **[UnauthorizedAccess:EC2/TorRelay](guardduty_finding-types-ec2.md#unauthorizedaccess-ec2-torrelay)** | EC2 | VPC Flow Logs | High | 
| **[UnauthorizedAccess:IAMUser/ConsoleLoginSuccess\.B](guardduty_finding-types-iam.md#unauthorizedaccess-iam-consoleloginsuccessb)** | IAM | CloudTrail management event | Medium | 
| **[UnauthorizedAccess:IAMUser/InstanceCredentialExfiltration\.OutsideAWS](guardduty_finding-types-iam.md#unauthorizedaccess-iam-instancecredentialexfiltrationoutsideaws)** | IAM | CloudTrail management event | High | 
| **[UnauthorizedAccess:IAMUser/MaliciousIPCaller](guardduty_finding-types-iam.md#unauthorizedaccess-iam-maliciousipcaller)** | IAM | CloudTrail management event | Medium | 
| **[UnauthorizedAccess:IAMUser/MaliciousIPCaller\.Custom](guardduty_finding-types-iam.md#unauthorizedaccess-iam-maliciousipcallercustom)** | IAM | CloudTrail management event | Medium | 
| **[UnauthorizedAccess:IAMUser/TorIPCaller](guardduty_finding-types-iam.md#unauthorizedaccess-iam-toripcaller)** | IAM | CloudTrail management event | Medium | 
| **[UnauthorizedAccess:S3/MaliciousIPCaller\.Custom](guardduty_finding-types-s3.md#unauthorizedaccess-s3-maliciousipcallercustom)** | S3 | CloudTrail S3 data event | High | 
| **[UnauthorizedAccess:S3/TorIPCaller](guardduty_finding-types-s3.md#unauthorizedaccess-s3-toripcaller)** | S3 | CloudTrail S3 data event | High | 