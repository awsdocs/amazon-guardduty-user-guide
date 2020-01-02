# Trojan Finding Types<a name="guardduty_trojan"></a>

This section covers the active Trojan threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Trojan:EC2/BlackholeTraffic](#trojan4)
+ [Trojan:EC2/DropPoint](#trojan5)
+ [Trojan:EC2/BlackholeTraffic\!DNS](#trojan6)
+ [Trojan:EC2/DriveBySourceTraffic\!DNS](#trojan7)
+ [Trojan:EC2/DropPoint\!DNS](#trojan8)
+ [Trojan:EC2/DGADomainRequest\.B](#trojan9)
+ [Trojan:EC2/DGADomainRequest\.C\!DNS](#trojan95)
+ [Trojan:EC2/DNSDataExfiltration](#trojan10)
+ [Trojan:EC2/PhishingDomainRequest\!DNS](#trojan11)

## Trojan:EC2/BlackholeTraffic<a name="trojan4"></a>

### Finding description<a name="trojan4_description"></a>

**EC2 instance is attempting to communicate with an IP address of a remote host that is a known black hole\.**

This finding informs you that an EC2 instance in your AWS environment might be compromised because it is trying to communicate with an IP address of a black hole \(or sink hole\)\. Black holes refer to places in the network where incoming or outgoing traffic is silently discarded without informing the source that the data didn't reach its intended recipient\. A black hole IP address specifies a host machine that is not running or an address to which no host has been assigned\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Medium<a name="trojan4_severity"></a>

## Trojan:EC2/DropPoint<a name="trojan5"></a>

### Finding description<a name="trojan5_description"></a>

**An EC2 instance is attempting to communicate with an IP address of a remote host that is known to hold credentials and other stolen data captured by malware\.**

This finding informs you that an EC2 instance in your AWS environment is trying communicate with an IP address of a remote host that is known to hold credentials and other stolen data captured by malware\. Your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Medium<a name="trojan5_severity"></a>

## Trojan:EC2/BlackholeTraffic\!DNS<a name="trojan6"></a>

### Finding description<a name="trojan6_description"></a>

**EC2 instance is querying a domain name that is being redirected to a black hole IP address\.**

This finding informs you that an EC2 instance in your AWS environment might be compromised because it is querying a domain name that is being redirected to a black hole IP address\. Black holes refer to places in the network where incoming or outgoing traffic is silently discarded without informing the source that the data didn't reach its intended recipient\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: Medium<a name="trojan6_severity"></a>

## Trojan:EC2/DriveBySourceTraffic\!DNS<a name="trojan7"></a>

### Finding description<a name="trojan7_description"></a>

**EC2 instance is querying a domain name of a remote host that is a known source of Drive\-By download attacks\.**

This finding informs you that an EC2 instance in your AWS environment might be compromised because it is querying a domain name of a remote host that is a known source of Drive\-By download attacks\. These are unintended downloads of computer software from the internet that can trigger an automatic install of a virus, spyware, or malware\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="trojan7_severity"></a>

## Trojan:EC2/DropPoint\!DNS<a name="trojan8"></a>

### Finding description<a name="trojan8_description"></a>

**An EC2 instance is querying a domain name of a remote host that is known to hold credentials and other stolen data captured by malware\.**

This finding informs you that an EC2 instance in your AWS environment is querying a domain name of a remote host that is known to hold credentials and other stolen data captured by malware\. Your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="trojan8_severity"></a>

## Trojan:EC2/DGADomainRequest\.B<a name="trojan9"></a>

### Finding description<a name="trojan9_description"></a>

**EC2 instance is querying algorithmically generated domains\. Such domains are commonly used by malware and could be an indication of a compromised EC2 instance\.**

This finding informs you that there is an EC2 instance in your AWS environment that is trying to query domain generation algorithms \(DGA\) domains\. Your EC2 instance might be compromised\. 

**Note**  
This finding is based on analysis of domain names using advanced heuristics, and hence may identify new DGA domains that are not present in Threat Intelligence feeds\.

DGAs are used to periodically generate a large number of domain names that can be used as rendezvous points with their command and control \(C&C\) servers\. C&C servers are computers that issue commands to members of a botnet, which is a collection of internet\-connected devices that are infected and controlled by a common type of malware\. The large number of potential rendezvous points makes it difficult to effectively shut down botnets because infected computers attempt to contact some of these domain names every day to receive updates or commands\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="trojan9_severity"></a>

## Trojan:EC2/DGADomainRequest\.C\!DNS<a name="trojan95"></a>

### Finding description<a name="trojan95_description"></a>

**EC2 instance is querying algorithmically generated domains\. Such domains are commonly used by malware and could be an indication of a compromised EC2 instance\.**

This finding informs you that there is an EC2 instance in your AWS environment that is trying to query domain generation algorithms \(DGA\) domains\. Your EC2 instance might be compromised\.

**Note**  
This finding is based on "known" DGA domains from GuardDuty's threat intelligence feeds\.

DGAs are used to periodically generate a large number of domain names that can be used as rendezvous points with their command and control \(C&C\) servers\. C&C servers are computers that issue commands to members of a botnet, which is a collection of internet\-connected devices that are infected and controlled by a common type of malware\. The large number of potential rendezvous points makes it difficult to effectively shut down botnets because infected computers attempt to contact some of these domain names every day to receive updates or commands\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="trojan95_severity"></a>

## Trojan:EC2/DNSDataExfiltration<a name="trojan10"></a>

### Finding description<a name="trojan10_description"></a>

**EC2 instance is exfiltrating data through DNS queries\.**

This finding informs you that there is an EC2 instance in your AWS environment with malware that uses DNS queries for outbound data transfers\. The result is the exfiltration of data\. Your EC2 instance might be compromised\. DNS traffic is not typically blocked by firewalls\. For example, malware in a compromised EC2 instance can encode data, \(such as your credit card number\), into a DNS query and send it to a remote DNS server that is controlled by an attacker\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="trojan10_severity"></a>

## Trojan:EC2/PhishingDomainRequest\!DNS<a name="trojan11"></a>

### Finding description<a name="trojan11_description"></a>

**EC2 instance is querying domains involved in phishing attacks\. Your EC2 instance might be compromised\.**

This finding informs you that there is an EC2 instance in your AWS environment that is trying to query a domain involved in phishing attacks\. Phishing domains are set up by someone posing as a legitimate institution in order to induce individuals into providing sensitive data such as personally identifiable information, banking and credit card details, and passwords\. Your EC2 instance is potentially trying to retrieve sensitive data stored on a phishing website\. Or your EC2 instance is attempting to setup a phishing website\. Your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="trojan11_severity"></a>