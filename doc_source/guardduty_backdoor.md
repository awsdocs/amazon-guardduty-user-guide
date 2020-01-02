# Backdoor Finding Types<a name="guardduty_backdoor"></a>

This section covers the active Backdoor threat purpose finding types\. For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\. 

**Important**  
The default severity value of a finding type is subject to change based on various criteria when the finding is generated\.

**Topics**
+ [Backdoor:EC2/Spambot](#backdoor6)
+ [Backdoor:EC2/C&CActivity\.B\!DNS](#backdoor7)
+ [Backdoor:EC2/DenialOfService\.Tcp](#backdoor8)
+ [Backdoor:EC2/DenialOfService\.Udp](#backdoor9)
+ [Backdoor:EC2/DenialOfService\.Dns](#backdoor10)
+ [Backdoor:EC2/DenialOfService\.UdpOnTcpPorts](#backdoor11)
+ [Backdoor:EC2/DenialOfService\.UnusualProtocol](#backdoor12)

## Backdoor:EC2/Spambot<a name="backdoor6"></a>

### Finding description<a name="backdoor6_description"></a>

**EC2 instance is exhibiting unusual behavior by communicating with a remote host on port 25\. **

This finding informs you that an EC2 instance in your AWS environment is communicating with a remote host on port 25\. This behavior is unusual because this EC2 instance has no prior history of communications on port 25\. Port 25 is traditionally used by mail servers for SMTP communications\. Your EC2 instance might be compromised and sending out spam\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\. 

### Default severity: Medium<a name="backdoor6_severity"></a>

## Backdoor:EC2/C&CActivity\.B\!DNS<a name="backdoor7"></a>

### Finding description<a name="backdoor7_description"></a>

**EC2 instance is querying a domain name that is associated with a known command and control server\.**

This finding informs you that there is an EC2 instance in your AWS environment that is querying a domain name associated with a known command and control \(C&C\) server\. Your EC2 instance might be compromised\. C&C servers are computers that issue commands to members of a botnet\. A botnet is a collection of internet\-connected devices \(which might include PCs, servers, mobile devices, and internet of things devices\) that are infected and controlled by a common type of malware\. Botnets are often used to distribute malware and gather misappropriated information, such as credit card numbers\. Depending on the purpose and structure of the botnet, the C&C server might also issue commands to begin a distributed denial of service \(DDoS\) attack\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

**Note**  
To test how GuardDuty's generates this finding type you can make a DNS request against a test domain `guarddutyc2activityb.com`\.

### Default severity: High<a name="backdoor7_severity"></a>

## Backdoor:EC2/DenialOfService\.Tcp<a name="backdoor8"></a>

### Finding description<a name="backdoor8_description"></a>

**An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using the TCP protocol\.**

This finding informs you that there is an EC2 instance in your AWS environment that is generating a large volume of outbound TCP traffic\. This may indicate that the instance is compromised and is being used to perform Denial\-of\-Service \(DoS\) attacks using TCP protocol\. This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="backdoor8_severity"></a>

## Backdoor:EC2/DenialOfService\.Udp<a name="backdoor9"></a>

### Finding description<a name="backdoor9_description"></a>

**An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using the UDP protocol\.**

This finding informs you that there is an EC2 instance in your AWS environment that is generating a large volume of outbound UDP traffic\. This may indicate that the instance is compromised and is being used to perform Denial\-of\-Service \(DoS\) attacks using UDP protocol\. This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="backdoor9_severity"></a>

## Backdoor:EC2/DenialOfService\.Dns<a name="backdoor10"></a>

### Finding description<a name="backdoor10_description"></a>

**An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using the DNS protocol\.**

This finding informs you that there is an EC2 instance in your AWS environment that is generating a large volume of outbound DNS traffic\. This may indicate that the instance is compromised and is being used to perform Denial\-of\-Service \(DoS\) attacks using DNS protocol\. This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="backdoor10_severity"></a>

## Backdoor:EC2/DenialOfService\.UdpOnTcpPorts<a name="backdoor11"></a>

### Finding description<a name="backdoor11_description"></a>

**An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using the UDP protocol on a TCP port\.**

This finding informs you that there is an EC2 instance in your AWS environment that is generating a large volume of outbound UDP traffic targeted to a port that is typically used for TCP communication\. This may indicate that the instance is compromised and is being used to perform a Denial\-of\-Service \(DoS\) attacks using UDP protocol on a TCP port\. This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="backdoor11_severity"></a>

## Backdoor:EC2/DenialOfService\.UnusualProtocol<a name="backdoor12"></a>

### Finding description<a name="backdoor12_description"></a>

**An EC2 instance is behaving in a manner that may indicate it is being used to perform a Denial of Service \(DoS\) attack using an unusual protocol\.**

This finding informs you that there is an EC2 instance in your AWS environment that is generating a large volume of outbound traffic of an unusual protocol type that is not typically used by EC2 instances \(for example, Internet Group Management Protocol\)\. This may indicate that the instance is compromised and is being used to perform Denial\-of\-Service \(DoS\) attacks using an unusual protocol\. This finding detects DoS attacks only against publicly routable IP addresses, which are primary targets of DoS attacks\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

### Default severity: High<a name="backdoor12_severity"></a>