# GuardDuty EC2 finding types<a name="guardduty_finding-types-ec2"></a>

The following findings are specific to Amazon EC2 resources and always have a Resource Type of `Instance`\. The severity and details of the findings differ based on the Resource Role, which indicates whether the EC2 instance was the target of suspicious activity or the actor performing the activity\.

For all instance type findings, it is recommended that you examine the resource in question to determine if it is behaving in an expected manner\. If the activity is authorized, you can use Suppression Rules or Trusted IP lists to prevent false positive notifications for that resource\. If the activity is unexpected, the security best practice is to assume the instance has been compromised and take the actions detailed in [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

**Topics**
+ [Backdoor:EC2/C&CActivity\.B\!DNS](#backdoor-ec2-ccactivitybdns)
+ [Backdoor:EC2/DenialOfService\.Dns](#backdoor-ec2-denialofservicedns)
+ [Backdoor:EC2/DenialOfService\.Tcp](#backdoor-ec2-denialofservicetcp)
+ [Backdoor:EC2/DenialOfService\.Udp](#backdoor-ec2-denialofserviceudp)
+ [Backdoor:EC2/DenialOfService\.UdpOnTcpPorts](#backdoor-ec2-denialofserviceudpontcpports)
+ [Backdoor:EC2/DenialOfService\.UnusualProtocol](#backdoor-ec2-denialofserviceunusualprotocol)
+ [Backdoor:EC2/Spambot](#backdoor-ec2-spambot)
+ [Behavior:EC2/NetworkPortUnusual](#behavior-ec2-networkportunusual)
+ [Behavior:EC2/TrafficVolumeUnusual](#behavior-ec2-trafficvolumeunusual)
+ [CryptoCurrency:EC2/BitcoinTool\.B](#cryptocurrency-ec2-bitcointoolb)
+ [CryptoCurrency:EC2/BitcoinTool\.B\!DNS](#cryptocurrency-ec2-bitcointoolbdns)
+ [Recon:EC2/PortProbeEMRUnprotectedPort](#recon-ec2-portprobeemrunprotectedport)
+ [Recon:EC2/PortProbeUnprotectedPort](#recon-ec2-portprobeunprotectedport)
+ [Recon:EC2/Portscan](#recon-ec2-portscan)
+ [Trojan:EC2/BlackholeTraffic](#trojan-ec2-blackholetraffic)
+ [Trojan:EC2/BlackholeTraffic\!DNS](#trojan-ec2-blackholetrafficdns)
+ [Trojan:EC2/DGADomainRequest\.B](#trojan-ec2-dgadomainrequestb)
+ [Trojan:EC2/DGADomainRequest\.C\!DNS](#trojan-ec2-dgadomainrequestcdns)
+ [Trojan:EC2/DNSDataExfiltration](#trojan-ec2-dnsdataexfiltration)
+ [Trojan:EC2/DriveBySourceTraffic\!DNS](#trojan-ec2-drivebysourcetrafficdns)
+ [Trojan:EC2/DropPoint](#trojan-ec2-droppoint)
+ [Trojan:EC2/DropPoint\!DNS](#trojan-ec2-droppointdns)
+ [Trojan:EC2/PhishingDomainRequest\!DNS](#trojan-ec2-phishingdomainrequestdns)
+ [UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom](#unauthorizedaccess-ec2-maliciousipcallercustom)
+ [UnauthorizedAccess:EC2/MetadataDNSRebind](#unauthorizedaccess-ec2-metadatadnsrebind)
+ [UnauthorizedAccess:EC2/RDPBruteForce](#unauthorizedaccess-ec2-rdpbruteforce)
+ [UnauthorizedAccess:EC2/SSHBruteForce](#unauthorizedaccess-ec2-sshbruteforce)
+ [UnauthorizedAccess:EC2/TorClient](#unauthorizedaccess-ec2-torclient)
+ [UnauthorizedAccess:EC2/TorIPCaller](#unauthorizedaccess-ec2-toripcaller)
+ [UnauthorizedAccess:EC2/TorRelay](#unauthorizedaccess-ec2-torrelay)

## Backdoor:EC2/C&CActivity\.B\!DNS<a name="backdoor-ec2-ccactivitybdns"></a>

### An EC2 instance is querying a domain name that is associated with a known command and control server\.<a name="backdoor-ec2-ccactivitybdns_description"></a>

#### <a name="backdoor-ec2-ccactivitybdns_severity"></a>

**Default severity: High**

This finding informs you that the listed Amazon EC2 instance within your AWS environment is querying a domain name associated with a known command and control \(C&C\) server\. The listed Amazon EC2 instance might be compromised\. Command and control servers are computers that issue commands to members of a botnet\. A botnet is a collection of internet\-connected devices which might include PCs, servers, mobile devices, and Internet of Things devices, that are infected and controlled by a common type of malware\. Botnets are often used to distribute malware and gather misappropriated information, such as credit card numbers\. Depending on the purpose and structure of the botnet, the C&C server might also issue commands to begin a distributed denial\-of\-service \(DDoS\) attack\.

**Note**  
To test how GuardDuty generates this finding type, you can make a DNS request from your instance \(using `dig` for Linux or `nslookup` for Windows\) against a test domain `guarddutyc2activityb.com`\.

#### <a name="backdoor-ec2-ccactivitybdns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

## Backdoor:EC2/DenialOfService\.Dns<a name="backdoor-ec2-denialofservicedns"></a>

### An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using the DNS protocol\.<a name="backdoor-ec2-denialofservicedns_description"></a>

#### <a name="backdoor-ec2-denialofservicedns_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance within your AWS environment is generating a large volume of outbound DNS traffic\. This may indicate that the listed instance is compromised and being used to perform denial\-of\-service \(DoS\) attacks using DNS protocol\.

**Note**  
This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\.

#### <a name="backdoor-ec2-denialofservicedns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/DenialOfService\.Tcp<a name="backdoor-ec2-denialofservicetcp"></a>

### An EC2 instance is behaving in a manner indicating it is being used to perform a Denial of Service \(DoS\) attack using the TCP protocol\.<a name="backdoor-ec2-denialofservicetcp_description"></a>

#### <a name="backdoor-ec2-denialofservicetcp_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance within your AWS environment is generating a large volume of outbound TCP traffic\. This may indicate that the instance is compromised and being used to perform denial\-of\-service \(DoS\) attacks using TCP protocol\. 

**Note**  
This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\.

#### <a name="backdoor-ec2-denialofservicetcp_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/DenialOfService\.Udp<a name="backdoor-ec2-denialofserviceudp"></a>

### An EC2 instance is behaving in a manner indicating it is being used to perform a Denial of Service \(DoS\) attack using the UDP protocol\.<a name="backdoor-ec2-denialofserviceudp_description"></a>

#### <a name="backdoor-ec2-denialofserviceudp_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance within your AWS environment is generating a large volume of outbound UDP traffic\. This may indicate that the listed instance is compromised and being used to perform denial\-of\-service \(DoS\) attacks using UDP protocol\. 

**Note**  
This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\.

#### <a name="backdoor-ec2-denialofserviceudp_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/DenialOfService\.UdpOnTcpPorts<a name="backdoor-ec2-denialofserviceudpontcpports"></a>

### An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using the UDP protocol on a TCP port\.<a name="backdoor-ec2-denialofserviceudpontcpports_description"></a>

#### <a name="backdoor-ec2-denialofserviceudpontcpports_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance within your AWS environment is generating a large volume of outbound UDP traffic targeted to a port that is typically used for TCP communication\. This may indicate that the listed instance is compromised and being used to perform a denial\-of\-service \(DoS\) attacks using UDP protocol on a TCP port\. 

**Note**  
This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\.

#### <a name="backdoor-ec2-denialofserviceudpontcpports_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/DenialOfService\.UnusualProtocol<a name="backdoor-ec2-denialofserviceunusualprotocol"></a>

### An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using an unusual protocol\.<a name="backdoor-ec2-denialofserviceunusualprotocol_description"></a>

#### <a name="backdoor-ec2-denialofserviceunusualprotocol_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance in your AWS environment is generating a large volume of outbound traffic from an unusual protocol type that is not typically used by EC2 instances, such as Internet Group Management Protocol\. This may indicate that the instance is compromised and is being used to perform denial\-of\-service \(DoS\) attacks using an unusual protocol\. This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\.

#### <a name="backdoor-ec2-denialofserviceunusualprotocol_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/Spambot<a name="backdoor-ec2-spambot"></a>

### An EC2 instance is exhibiting unusual behavior by communicating with a remote host on port 25\.<a name="backdoor-ec2-spambot_description"></a>

#### <a name="backdoor-ec2-spambot_severity"></a>

**Default severity: Medium**

This finding informs you that the listed EC2 instance in your AWS environment is communicating with a remote host on port 25\. This behavior is unusual because this EC2 instance has no prior history of communications on port 25\. Port 25 is traditionally used by mail servers for SMTP communications\. This finding indicates your EC2 instance might be compromised for use in sending out spam\.

#### <a name="backdoor-ec2-spambot_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Behavior:EC2/NetworkPortUnusual<a name="behavior-ec2-networkportunusual"></a>

### An EC2 instance is communicating with a remote host on an unusual server port\.<a name="behavior-ec2-networkportunusual_description"></a>

#### <a name="behavior-ec2-networkportunusual_severity"></a>

**Default severity: Medium**

This finding informs you that the listed EC2 instance in your AWS environment is behaving in a way that deviates from the established baseline\. This EC2 instance has no prior history of communications on this remote port\.

#### <a name="behavior-ec2-networkportunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Behavior:EC2/TrafficVolumeUnusual<a name="behavior-ec2-trafficvolumeunusual"></a>

### An EC2 instance is generating unusually large amounts of network traffic to a remote host\.<a name="behavior-ec2-trafficvolumeunusual_description"></a>

#### <a name="behavior-ec2-trafficvolumeunusual_severity"></a>

**Default severity: Medium**

This finding informs you that the listed EC2 instance in your AWS environment is behaving in a way that deviates from the established baseline\. This EC2 instance has no prior history of sending this much traffic to this remote host\.

#### <a name="behavior-ec2-trafficvolumeunusual_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## CryptoCurrency:EC2/BitcoinTool\.B<a name="cryptocurrency-ec2-bitcointoolb"></a>

### An EC2 instance is querying an IP address that is associated with cryptocurrency\-related activity\.<a name="cryptocurrency-ec2-bitcointoolb_description"></a>

#### <a name="cryptocurrency-ec2-bitcointoolb_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance in your AWS environment is querying an IP Address that is associated with Bitcoin or other cryptocurrency\-related activity\. Bitcoin is a worldwide cryptocurrency and digital payment system\. Besides being used as a reward for Bitcoin mining, Bitcoin can be exchanged for other currencies, products, and services\. 

#### <a name="cryptocurrency-ec2-bitcointoolb_remediation"></a>

**Remediation recommendations:**

If you use this EC2 instance to mine or manage cryptocurrency, or this instance is otherwise involved in blockchain activity, this finding could represented expected activity for your environment\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `CryptoCurrency:EC2/BitcoinTool.B!DNS`\. The second filter criteria should be the **Instance ID** of the instance involved in blockchain activity\. To learn more about creating suppression rules see [Suppression rules](findings_suppression-rule.md)\.

## CryptoCurrency:EC2/BitcoinTool\.B\!DNS<a name="cryptocurrency-ec2-bitcointoolbdns"></a>

### An EC2 instance is querying a domain name that is associated with cryptocurrency\-related activity\.<a name="cryptocurrency-ec2-bitcointoolbdns_description"></a>

#### <a name="cryptocurrency-ec2-bitcointoolbdns_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance in your AWS environment is querying a domain name that is associated with Bitcoin or other cryptocurrency\-related activity\. Bitcoin is a worldwide cryptocurrency and digital payment system\. Besides being used as a reward for Bitcoin mining, Bitcoin can be exchanged for other currencies, products, and services\.

#### <a name="cryptocurrency-ec2-bitcointoolbdns_remediation"></a>

**Remediation recommendations:**

If you use this EC2 instance to mine or manage cryptocurrency, or this instance is otherwise involved in blockchain activity, this finding could represented expected activity for your environment\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `CryptoCurrency:EC2/BitcoinTool.B!DNS`\. The second filter criteria should be the **Instance ID** of the instance involved in blockchain activity\. To learn more about creating suppression rules see [Suppression rules](findings_suppression-rule.md)\.

## Recon:EC2/PortProbeEMRUnprotectedPort<a name="recon-ec2-portprobeemrunprotectedport"></a>

### An EC2 instance has an unprotected EMR related port which is being probed by a known malicious host\.<a name="recon-ec2-portprobeemrunprotectedport_description"></a>

#### <a name="recon-ec2-portprobeemrunprotectedport_severity"></a>

**Default severity: High**

This finding informs you that an Amazon EMR related sensitive port on the listed EC2 instance that is part of an Amazon EMR cluster in your AWS environment is not blocked by a security group, an access control list \(ACL\), or an on\-host firewall such as Linux IPTables, and that known scanners on the internet are actively probing it\. Ports that can trigger this finding, such as port 8088 \(YARN Web UI port\), could potentially be used for remote code execution\. 

#### <a name="recon-ec2-portprobeemrunprotectedport_remediation"></a>

**Remediation recommendations:**

You should block open access to ports on Amazon EMR clusters from the internet and restrict access only to specific IP addresses that require access to these ports\. For more information see, [Security Groups for EMR Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-security-groups.html)\.

## Recon:EC2/PortProbeUnprotectedPort<a name="recon-ec2-portprobeunprotectedport"></a>

### An EC2 instance has an unprotected port that is being probed by a known malicious host\.<a name="recon-ec2-portprobeunprotectedport_description"></a>

#### <a name="recon-ec2-portprobeunprotectedport_severity"></a>

**Default severity: Low\***

**Note**  
This finding's default severity is Low\. However, if the port being probed is used by Amazon Elasticsearch Service \(9200 or 9300\), the finding's severity is High\.

This finding informs you that a port on the listed EC2 instance in your AWS environment is not blocked by a security group, access control list \(ACL\), or an on\-host firewall such as Linux IPTables, and that known scanners on the internet are actively probing it\. 

 If the identified unprotected port is 22 or 3389 and you are using these ports to connect to your instance, you can still limit exposure by allowing access to these ports only to the IP addresses from your corporate network IP address space\. To restrict access to port 22 on Linux, see [Authorizing Inbound Traffic for Your Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/authorizing-access-to-an-instance.html)\. To restrict access to port 3389 on Windows, see [Authorizing Inbound Traffic for Your Windows Instances](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/authorizing-access-to-an-instance.html)\.

#### <a name="recon-ec2-portprobeunprotectedport_remediation"></a>

**Remediation recommendations:**

There may be cases in which instances are intentionally exposed, for example if they are hosting web servers\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `Recon:EC2/PortProbeUnprotectedPort`\. The second filter criteria should match the instance or instances that serve as a bastion host\. You can use either the **Instance image ID** attribute or the **Tag** value attribute, depending on which criteria is identifiable with the instances that host these tools\. For more information about creating suppression rules see [Suppression rules](findings_suppression-rule.md)\.

## Recon:EC2/Portscan<a name="recon-ec2-portscan"></a>

### An EC2 instance is performing outbound port scans to a remote host\.<a name="recon-ec2-portscan_description"></a>

#### <a name="recon-ec2-portscan_severity"></a>

**Default severity: Medium**

This finding informs you that the listed EC2 instance in your AWS environment is engaged in a possible port scan attack because it is trying to connect to multiple ports over a short period of time\. The purpose of a port scan attack is to locate open ports to discover which services the machine is running and to identify its operating system\.

#### <a name="recon-ec2-portscan_remediation"></a>

**Remediation recommendations:**

This finding is can be a false positive when vulnerability assessment applications are deployed on EC2 instances in your environment because these applications conduct portscans to alert you about misconfigured open ports\. If this is the case in your AWS environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `Recon:EC2/Portscan`\. The second filter criteria should match the instance or instances that host these vulnerability assessment tools\. You can use either the **Instance image ID** attribute or the **Tag** value attribute depending on which criteria are identifiable with the instances that host these tools\. For more information about creating suppression rules see [Suppression rules](findings_suppression-rule.md)\.

## Trojan:EC2/BlackholeTraffic<a name="trojan-ec2-blackholetraffic"></a>

### An EC2 instance is attempting to communicate with an IP address of a remote host that is a known black hole\.<a name="trojan-ec2-blackholetraffic_description"></a>

#### <a name="trojan-ec2-blackholetraffic_severity"></a>

**Default severity: Medium**

This finding informs you the listed EC2 instance in your AWS environment might be compromised because it is trying to communicate with an IP address of a black hole \(or sink hole\)\. Black holes are places in the network where incoming or outgoing traffic is silently discarded without informing the source that the data didn't reach its intended recipient\. A black hole IP address specifies a host machine that is not running or an address to which no host has been assigned\.

#### <a name="trojan-ec2-blackholetraffic_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/BlackholeTraffic\!DNS<a name="trojan-ec2-blackholetrafficdns"></a>

### An EC2 instance is querying a domain name that is being redirected to a black hole IP address\.<a name="trojan-ec2-blackholetrafficdns_description"></a>

#### <a name="trojan-ec2-blackholetrafficdns_severity"></a>

**Default severity: Medium**

This finding informs you the listed EC2 instance in your AWS environment might be compromised because it is querying a domain name that is being redirected to a black hole IP address\. Black holes are places in the network where incoming or outgoing traffic is silently discarded without informing the source that the data didn't reach its intended recipient\.

#### <a name="trojan-ec2-blackholetrafficdns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/DGADomainRequest\.B<a name="trojan-ec2-dgadomainrequestb"></a>

### An EC2 instance is querying algorithmically generated domains\. Such domains are commonly used by malware and could be an indication of a compromised EC2 instance\.<a name="trojan-ec2-dgadomainrequestb_description"></a>

#### <a name="trojan-ec2-dgadomainrequestb_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance in your AWS environment is trying to query domain generation algorithm \(DGA\) domains\. Your EC2 instance might be compromised\.

DGAs are used to periodically generate a large number of domain names that can be used as rendezvous points with their command and control \(C&C\) servers\. Command and control servers are computers that issue commands to members of a botnet, which is a collection of internet\-connected devices that are infected and controlled by a common type of malware\. The large number of potential rendezvous points makes it difficult to effectively shut down botnets because infected computers attempt to contact some of these domain names every day to receive updates or commands\.

**Note**  
This finding is based on analysis of domain names using advanced heuristics and may identify new DGA domains that are not present in threat intelligence feeds\.

#### <a name="trojan-ec2-dgadomainrequestb_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/DGADomainRequest\.C\!DNS<a name="trojan-ec2-dgadomainrequestcdns"></a>

### An EC2 instance is querying algorithmically generated domains\. Such domains are commonly used by malware and could be an indication of a compromised EC2 instance\.<a name="trojan-ec2-dgadomainrequestcdns_description"></a>

#### <a name="trojan-ec2-dgadomainrequestcdns_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance in your AWS environment is trying to query domain generation algorithm \(DGA\) domains\. Your EC2 instance might be compromised\.

DGAs are used to periodically generate a large number of domain names that can be used as rendezvous points with their command and control \(C&C\) servers\. Command and control servers are computers that issue commands to members of a botnet, which is a collection of internet\-connected devices that are infected and controlled by a common type of malware\. The large number of potential rendezvous points makes it difficult to effectively shut down botnets because infected computers attempt to contact some of these domain names every day to receive updates or commands\.

**Note**  
This finding is based on known DGA domains from GuardDuty's threat intelligence feeds\.

#### <a name="trojan-ec2-dgadomainrequestcdns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/DNSDataExfiltration<a name="trojan-ec2-dnsdataexfiltration"></a>

### An EC2 instance is exfiltrating data through DNS queries\.<a name="trojan-ec2-dnsdataexfiltration_description"></a>

#### <a name="trojan-ec2-dnsdataexfiltration_severity"></a>

**Default severity: High**

This finding informs you that the listed EC2 instance in your AWS environment is running malware that uses DNS queries for outbound data transfers\. This type of data transfer is indicative of a compromised instance and could result in the exfiltration of data\. DNS traffic is not typically blocked by firewalls\. For example, malware in a compromised EC2 instance can encode data, \(such as your credit card number\), into a DNS query and send it to a remote DNS server that is controlled by an attacker\.

#### <a name="trojan-ec2-dnsdataexfiltration_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/DriveBySourceTraffic\!DNS<a name="trojan-ec2-drivebysourcetrafficdns"></a>

### An EC2 instance is querying a domain name of a remote host that is a known source of Drive\-By download attacks\.<a name="trojan-ec2-drivebysourcetrafficdns_description"></a>

#### <a name="trojan-ec2-drivebysourcetrafficdns_severity"></a>

**Default severity: Medium**

This finding informs you that the listed EC2 instance in your AWS environment might be compromised because it is querying a domain name of a remote host that is a known source of drive\-by download attacks\. These are unintended downloads of computer software from the internet that can trigger an automatic installation of a virus, spyware, or malware\.

#### <a name="trojan-ec2-drivebysourcetrafficdns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/DropPoint<a name="trojan-ec2-droppoint"></a>

### An EC2 instance is attempting to communicate with an IP address of a remote host that is known to hold credentials and other stolen data captured by malware\.<a name="trojan-ec2-droppoint_description"></a>

#### <a name="trojan-ec2-droppoint_severity"></a>

**Default severity: Medium**

This finding informs you that an EC2 instance in your AWS environment is trying to communicate with an IP address of a remote host that is known to hold credentials and other stolen data captured by malware\.

#### <a name="trojan-ec2-droppoint_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/DropPoint\!DNS<a name="trojan-ec2-droppointdns"></a>

### An EC2 instance is querying a domain name of a remote host that is known to hold credentials and other stolen data captured by malware\.<a name="trojan-ec2-droppointdns_description"></a>

#### <a name="trojan-ec2-droppointdns_severity"></a>

**Default severity: High**

This finding informs you that an EC2 instance in your AWS environment is querying a domain name of a remote host that is known to hold credentials and other stolen data captured by malware\.

#### <a name="trojan-ec2-droppointdns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Trojan:EC2/PhishingDomainRequest\!DNS<a name="trojan-ec2-phishingdomainrequestdns"></a>

### An EC2 instance is querying domains involved in phishing attacks\. Your EC2 instance might be compromised\.<a name="trojan-ec2-phishingdomainrequestdns_description"></a>

#### <a name="trojan-ec2-phishingdomainrequestdns_severity"></a>

**Default severity: High**

This finding informs you that there is an EC2 instance in your AWS environment that is trying to query a domain involved in phishing attacks\. Phishing domains are set up by someone posing as a legitimate institution in order to induce individuals to provide sensitive data, such as personally identifiable information, banking and credit card details, and passwords\. Your EC2 instance may be trying to retrieve sensitive data stored on a phishing website, or it may be attempting to set up a phishing website\. Your EC2 instance might be compromised\.

#### <a name="trojan-ec2-phishingdomainrequestdns_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/MaliciousIPCaller\.Custom<a name="unauthorizedaccess-ec2-maliciousipcallercustom"></a>

### An EC2 instance is making outbound connections to an IP address on a custom threat list\.<a name="unauthorizedaccess-ec2-maliciousipcallercustom_description"></a>

#### <a name="unauthorizedaccess-ec2-maliciousipcallercustom_severity"></a>

**Default severity: Medium**

This finding informs you that an EC2 instance in your AWS environment is communicating on an outbound port with an IP address included on a threat list that you uploaded\. In GuardDuty, a threat list consists of known malicious IP addresses\. GuardDuty generates findings based on uploaded threat lists\. This can indicate unauthorized access to your AWS resources\.

#### <a name="unauthorizedaccess-ec2-maliciousipcallercustom_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/MetadataDNSRebind<a name="unauthorizedaccess-ec2-metadatadnsrebind"></a>

### An EC2 instance is performing DNS lookups that resolve to the instance metadata service\.<a name="unauthorizedaccess-ec2-metadatadnsrebind_description"></a>

#### <a name="unauthorizedaccess-ec2-metadatadnsrebind_severity"></a>

**Default severity: High**

This finding informs you that an EC2 instance in your AWS environment is querying a domain that resolves to the EC2 metadata IP address \(169\.254\.169\.254\)\. A DNS query of this kind may indicate that the instance is a target of a DNS rebinding technique\. This technique can be used to obtain metadata from an EC2 instance, including the IAM credentials associated with the instance\.

DNS rebinding involves tricking an application running on the EC2 instance to load return data from a URL, where the domain name in the URL resolves to the EC2 metadata IP address \(169\.254\.169\.254\)\. This causes the application to access EC2 metadata and possibly make it available to the attacker\. 

It is possible to access EC2 metadata using DNS rebinding only if the EC2 instance is running a vulnerable application that allows injection of URLs, or if someone accesses the URL in a web browser running on the EC2 instance\.

#### <a name="unauthorizedaccess-ec2-metadatadnsrebind_remediation"></a>

**Remediation recommendations:**

In response to this finding, you should evaluate if there is a vulnerable application running on the EC2 instance, or if someone used a browser to access the domain identified in the finding\. If the root cause is a vulnerable application, you should fix the vulnerability\. If someone browsed the identified domain, you should block the domain or prevent users from accessing it\. If you determine this finding was related to either case above, you should [revoke the session associated with the EC2 instance](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_revoke-sessions.html)\.

Some AWS customers intentionally map the metadata IP address to a domain name on their authoritative DNS servers\. If this is the case in your environment, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `UnauthorizedAccess:EC2/MetaDataDNSRebind`\. The second filter criteria should be **DNS request domain** and the value should match the domain you have mapped to the metadata IP address \(169\.254\.169\.254\)\. For more information on creating suppression rules see [Suppression rules](findings_suppression-rule.md)\.

## UnauthorizedAccess:EC2/RDPBruteForce<a name="unauthorizedaccess-ec2-rdpbruteforce"></a>

### An EC2 instance has been involved in RDP brute force attacks\.<a name="unauthorizedaccess-ec2-rdpbruteforce_description"></a>

#### <a name="unauthorizedaccess-ec2-rdpbruteforce_severity"></a>

**Default severity: Low\***

**Note**  
This finding's severity is low if your EC2 instance was the target of a brute force attack\. This finding's severity is high if your EC2 instance is the actor being used to perform the brute force attack\.

This finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to RDP services on Windows\-based systems\. This can indicate unauthorized access to your AWS resources\.

#### <a name="unauthorizedaccess-ec2-rdpbruteforce_remediation"></a>

**Remediation recommendations:**

If your instance's **Resource Role** is `ACTOR`, this indicates your instance has been used to perform RDP brute force attacks\. Unless this instance has a legitimate reason to be contacting the IP address listed as the `Target`, it is recommended that you assume your instance has been compromised and take the actions listed in [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\. 

If your instance's **Resource Role** is `TARGET`, this finding can be remediated by securing your RDP port to only trusted IPs through Security Groups, ACLs, or firewalls\. For more information see [Tips for securing your EC2 instances \(Linux\)](http://aws.amazon.com/articles/tips-for-securing-your-ec2-instance/)\.

## UnauthorizedAccess:EC2/SSHBruteForce<a name="unauthorizedaccess-ec2-sshbruteforce"></a>

### An EC2 instance has been involved in SSH brute force attacks\.<a name="unauthorizedaccess-ec2-sshbruteforce_description"></a>

#### <a name="unauthorizedaccess-ec2-sshbruteforce_severity"></a>

**Default severity: Low\***

**Note**  
This finding's severity is low if a brute force attack is aimed at one of your EC2 instances\. This finding's severity is high if your EC2 instance is being used to perform the brute force attack\.

This finding informs you that an EC2 instance in your AWS environment was involved in a brute force attack aimed at obtaining passwords to SSH services on Linux\-based systems\. This can indicate unauthorized access to your AWS resources\. 

**Note**  
This finding is generated only through GuardDuty monitoring traffic on port 22\. If your SSH services are configured to use other ports, this finding is not generated\.

#### <a name="unauthorizedaccess-ec2-sshbruteforce_remediation"></a>

**Remediation recommendations:**

If the target of the brute force attempt is a bastion host, this may represent expected behavior for your AWS environment\. If this is the case, we recommend that you set up a suppression rule for this finding\. The suppression rule should consist of two filter criteria\. The first criteria should use the **Finding type** attribute with a value of `UnauthorizedAccess:EC2/SSHBruteForce`\. The second filter criteria should match the instance or instances that serve as a bastion host\. You can use either the **Instance image ID** attribute or the **Tag** value attribute depending on which criteria is identifiable with the instances that host these tools\. For more information about creating suppression rules see [Suppression rules](findings_suppression-rule.md)\.

If this activity is not expected for your environment and your instance's **Resource Role** is `TARGET`, this finding can be remediated by securing your SSH port to only trusted IPs through Security Groups, ACLs, or firewalls\. For more information, see [Tips for securing your EC2 instances \(Linux\)](http://aws.amazon.com/articles/tips-for-securing-your-ec2-instance/)\. If your instance's **Resource Role** is `ACTOR`, this indicates the instance has been used to perform SSH brute force attacks\. Unless this instance has a legitimate reason to be contacting the IP address listed as the `Target`, it is recommended that you assume your instance has been compromised and take the actions listed in [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/TorClient<a name="unauthorizedaccess-ec2-torclient"></a>

### Your EC2 instance is making connections to a Tor Guard or an Authority node\.<a name="unauthorizedaccess-ec2-torclient_description"></a>

#### <a name="unauthorizedaccess-ec2-torclient_severity"></a>

**Default severity: High**

This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor Guard or an Authority node\. Tor is software for enabling anonymous communication\. Tor Guards and Authority nodes act as initial gateways into a Tor network\. This traffic can indicate that this EC2 instance has been compromised and is acting as a client on a Tor network\. This finding may indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="unauthorizedaccess-ec2-torclient_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/TorIPCaller<a name="unauthorizedaccess-ec2-toripcaller"></a>

### Your EC2 instance is receiving inbound connections from a Tor exit node\.<a name="unauthorizedaccess-ec2-toripcaller_description"></a>

#### <a name="unauthorizedaccess-ec2-toripcaller_severity"></a>

**Default severity: Medium**

This finding informs you that an API operation, such as an attempt to launch an EC2 instance, create a new IAM user, or modify your AWS privileges, was invoked from a Tor exit node IP address\. Tor is software for enabling anonymous communication\. It encrypts and randomly bounces communications through relays between a series of network nodes\. The last Tor node is called the exit node\. This finding can indicate unauthorized access to your AWS resources with the intent of hiding the attacker's true identity\.

#### <a name="unauthorizedaccess-ec2-toripcaller_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:EC2/TorRelay<a name="unauthorizedaccess-ec2-torrelay"></a>

### Your EC2 instance is making connections to a Tor network as a Tor relay\.<a name="unauthorizedaccess-ec2-torrelay_description"></a>

#### <a name="unauthorizedaccess-ec2-torrelay_severity"></a>

**Default severity: High**

This finding informs you that an EC2 instance in your AWS environment is making connections to a Tor network in a manner that suggests that it's acting as a Tor relay\. Tor is software for enabling anonymous communication\. Tor increases anonymity of communication by forwarding the client's possibly illicit traffic from one Tor relay to another\.

#### <a name="unauthorizedaccess-ec2-torrelay_remediation"></a>

**Remediation recommendations:**

If this activity is unexpected, your instance is likely compromised, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.