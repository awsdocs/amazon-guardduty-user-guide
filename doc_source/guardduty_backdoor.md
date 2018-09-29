# GuardDuty Backdoor Finding Types<a name="guardduty_backdoor"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\.

**Topics**
+ [Backdoor:EC2/XORDDOS](#backdoor2)
+ [Backdoor:EC2/Spambot](#backdoor6)
+ [Backdoor:EC2/C&CActivity\.B\!DNS](#backdoor7)

## Backdoor:EC2/XORDDOS<a name="backdoor2"></a>

### Finding description<a name="backdoor2_description"></a>

**An EC2 instance is attempting to communicate with an IP address that is associated with XorDDos malware\.**

This finding informs you that an EC2 instance in your AWS environment is attempting to communicate with an IP address that is associated with XorDDos malware\. This EC2 instance might be compromised\. XOR DDoS is Trojan malware that hijacks Linux systems\. To gain access to the system, it launches a brute force attack in order to discover the password to Secure Shell \(SSH\) services on Linux\. After SSH credentials are acquired and the login is successful, it uses root privileges to run a script that downloads and installs XOR DDoS\. This malware is then used as part of a botnet to launch distributed denial of service \(DDoS\) attacks against other targets\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## Backdoor:EC2/Spambot<a name="backdoor6"></a>

### Finding description<a name="backdoor6_description"></a>

**EC2 instance is exhibiting unusual behavior by communicating with a remote host on port 25\. **

This finding informs you that an EC2 instance in your AWS environment is communicating with a remote host on port 25\. This behavior is unusual because this EC2 instance has no prior history of communications on port 25\. Port 25 is traditionally used by mail servers for SMTP communications\. Your EC2 instance might be compromised and sending out spam\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\. 

## Backdoor:EC2/C&CActivity\.B\!DNS<a name="backdoor7"></a>

### Finding description<a name="backdoor7_description"></a>

**EC2 instance is querying a domain name that is associated with a known command and control server\.**

This finding informs you that there is an EC2 instance in your AWS environment that is querying a domain name associated with a known command and control \(C&C\) server\. Your EC2 instance might be compromised\. C&C servers are computers that issue commands to members of a botnet\. A botnet is a collection of internet\-connected devices \(which might include PCs, servers, mobile devices, and internet of things devices\) that are infected and controlled by a common type of malware\. Botnets are often used to distribute malware and gather misappropriated information, such as credit card numbers\. Depending on the purpose and structure of the botnet, the C&C server might also issue commands to begin a distributed denial of service \(DDoS\) attack\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

**Note**  
To test how GuardDuty's generates this finding type you can make a DNS request against a test domain `guarddutyc2activityb.com`\.