# GuardDuty Behavior Finding Types<a name="guardduty_behavior"></a>

**Important**  
For information about important changes to the GuardDuty finding types, including newly added or retired finding types, see [Document History for Amazon GuardDuty](doc-history.md)\.

**Topics**
+ [Behavior:EC2/NetworkPortUnusual](#behavior3)
+ [Behavior:EC2/TrafficVolumeUnusual](#behavior4)

## Behavior:EC2/NetworkPortUnusual<a name="behavior3"></a>

### Finding description<a name="behavior3_description"></a>

**EC2 instance is communicating with a remote host on an unusual server port\.**

This finding informs you that an EC2 instance in your AWS environment is behaving in a way that deviates from the established baseline\. This EC2 instance has no prior history of communications on this remote port\. Your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.

## Behavior:EC2/TrafficVolumeUnusual<a name="behavior4"></a>

### Finding description<a name="behavior4_description"></a>

**EC2 instance is generating unusually large amounts of network traffic to a remote host\.**

This finding informs you that an EC2 instance in your AWS environment is behaving in a way that deviates from the established baseline\. This EC2 instance has no prior history of sending this much traffic to this remote host\. Your EC2 instance might be compromised\. For more information, see [Remediating a Compromised EC2 Instance](guardduty_remediate.md#compromised-ec2)\.