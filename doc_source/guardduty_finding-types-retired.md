# Retired finding types<a name="guardduty_finding-types-retired"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document history for Amazon GuardDuty](doc-history.md)\.

In the current release of GuardDuty, the following finding types are retired \(no longer generated\)\. You CANNOT reactivate retired GuardDuty findings types\. 

**Topics**
+ [Backdoor:EC2/XORDDOS](#backdoor2)
+ [Behavior:IAMUser/InstanceLaunchUnusual](#behavior1)
+ [CryptoCurrency:EC2/BitcoinTool\.A](#crypto1)
+ [UnauthorizedAccess:IAMUser/UnusualASNCaller](#unauthorized6)

## Backdoor:EC2/XORDDOS<a name="backdoor2"></a>

### Default severity: High<a name="backdoor2_severity"></a>

### Finding description<a name="backdoor2_description"></a>

**An EC2 instance is attempting to communicate with an IP address that is associated with XorDDos malware\.**

This finding informs you that an EC2 instance in your AWS environment is attempting to communicate with an IP address that is associated with XorDDos malware\. This EC2 instance might be compromised\. XOR DDoS is Trojan malware that hijacks Linux systems\. To gain access to the system, it launches a brute force attack in order to discover the password to Secure Shell \(SSH\) services on Linux\. After SSH credentials are acquired and the login is successful, it uses root privileges to run a script that downloads and installs XOR DDoS\. This malware is then used as part of a botnet to launch distributed denial of service \(DDoS\) attacks against other targets\. For more information, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## Behavior:IAMUser/InstanceLaunchUnusual<a name="behavior1"></a>

### Finding description<a name="behavior1_description"></a>

**An IAM user launched an EC2 instance of an unusual type\.**

This finding informs you that a specific IAM user in your AWS environment is exhibiting behavior that is different from the established baseline\. This IAM user has no prior history of launching an EC2 instance of this type\. Your IAM user credentials might be compromised\. For more information, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)

## CryptoCurrency:EC2/BitcoinTool\.A<a name="crypto1"></a>

### Finding description<a name="crypto1_description"></a>

**EC2 instance is communicating with Bitcoin mining pools\.**

This finding informs you that an EC2 instance in your AWS environment is communicating with Bitcoin mining pools\. In the field of cryptocurrency mining, a mining pool is the pooling of resources by miners who share their processing power over a network to split the reward according to the amount of work they contributed to solving a block\. Unless you use this EC2 instance for Bitcoin mining, your EC2 instance might be compromised\. For more information, see [Remediating a compromised EC2 instance](guardduty_remediate.md#compromised-ec2)\.

## UnauthorizedAccess:IAMUser/UnusualASNCaller<a name="unauthorized6"></a>

### Finding description<a name="unauthorized6_description"></a>

**An API was invoked from an IP address of an unusual network\.**

This finding informs you that certain activity was invoked from an IP address of an unusual network\. This network was never observed throughout the AWS usage history of the described user\. This activity can include a console login, an attempt to launch an EC2 instance, create a new IAM user, modify your AWS privileges, etc\. This can indicate unauthorized access to your AWS resources\. For more information, see [Remediating compromised AWS credentials](guardduty_remediate.md#compromised-creds)\.

**Important**  
The UnauthorizedAccess:IAMUser/UnusualASNCaller finding type has been retired\. You will now be notified about activity invoked from unusual networks via one of the following active GuardDuty finding types, based on the category of the API that was invoked from an unusual network:   
Persistence:IAMUser/NetworkPermissions
Persistence:IAMUser/ResourcePermissions
Persistence:IAMUser/UserPermissions
Recon:IAMUser/NetworkPermissions
Recon:IAMUser/ResourcePermissions
Recon:IAMUser/UserPermissions
ResourceConsumption:IAMUser/ComputeResources
Stealth:IAMUser/LoggingConfigurationModified
UnauthorizedAccess:IAMUser/ConsoleLogin