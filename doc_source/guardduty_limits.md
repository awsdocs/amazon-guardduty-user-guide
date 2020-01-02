# Limits<a name="guardduty_limits"></a>

The following are Amazon GuardDuty limits per AWS account per region:


| Resource | Default Limit | Comments | 
| --- | --- | --- | 
| Detectors | 1 | The maximum number of detector resources that can be created and activated per AWS account per region\. This is a hard limit\. You cannot request a limit increase of detectors\. | 
| GuardDuty filters | 100 | The maximum number of filters that can be saved per AWS account per region\.  | 
| Trusted IP sets | 1 | The maximum number of trusted IP sets that can be uploaded and activated per AWS account per region\. This is a hard limit\. You cannot request a limit increase of trusted IP sets\. | 
| IP addresses and CIDR ranges per Trusted IP List | 2,000 | The maximum number of IP addresses and CIDR ranges that you can include in a single Trusted IP List\. This is a hard limit\. You cannot request a limit increase for the number of IP address and CIDR ranges included in a single Trusted IP List\. | 
| Threat intel sets | 6 | The maximum number of threat intel sets that can be uploaded and activated per AWS account per region\.  | 
| IP addresses and CIDR ranges per Threat List | 250,000 | The maximum number of IP address and CIDR ranges that you can include in a Threat List\. This is a hard limit\. You cannot request a limit increase for the number of IP address and CIDR ranges included in a single Threat List\. | 
| Maximum file size for Trusted IP List or Threat List | 35 MB | The maximum file size for the file used to upload a list of IP addresses or CIDR ranges to include in a Trusted IP List or a Threat List\. This is a hard limit\. You cannot request a limit increase for the file size\. | 
| GuardDuty member accounts | 1000 | The maximum number of GuardDuty member accounts that can be added per AWS account \(GuardDuty master account\) per region\.  | 
| GuardDuty finding retention time | 90 days | The maximum number of days a GuardDuty\-generated finding is saved\. This is a hard limit\. You cannot request a limit increase of finding retention days\. | 