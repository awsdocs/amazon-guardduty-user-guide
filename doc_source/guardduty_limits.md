# Quotas for Amazon GuardDuty<a name="guardduty_limits"></a>

Your AWS account has default quotas, formerly referred to as limits, for each AWS service\. Unless otherwise noted, each quota is Region\-specific\. You can request increases for some quotas, and other quotas cannot be increased\.

To view the quotas for GuardDuty, open the [Service Quotas console](https://console.aws.amazon.com/servicequotas/home)\. In the navigation pane, choose **AWS services** and select **Amazon GuardDuty**\.

To request a quota increase, see [Requesting a quota increase](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) in the *Service Quotas User Guide*\.

Your AWS account has the following quotas for Amazon GuardDuty per Region\.


| Resource | Default | Comments | 
| --- | --- | --- | 
| Detectors | 1 | The maximum number of detector resources that you can create per AWS account per Region\. You cannot request a quota increase\. | 
| Filters | 100 | The maximum number of saved filters per AWS account per Region\. | 
| Finding retention period | 90 days | The maximum number of days a finding is retained\. You cannot request a quota increase\. | 
| IP addresses and CIDR ranges per Trusted IP List | 2,000 | The maximum number of IP addresses and CIDR ranges that you can include in a single Trusted IP List\. You cannot request a quota increase\. | 
| IP addresses and CIDR ranges per Threat List | 250,000 | The maximum number of IP address and CIDR ranges that you can include in a Threat List\. You cannot request a quota increase\. | 
| Maximum file size | 35 MB | The maximum file size for the file used to upload a list of IP addresses or CIDR ranges to include in a Trusted IP List or a Threat List\. You cannot request a quota increase\. | 
| Member accounts | 5000 | The maximum number of member accounts associated with a master account\. You can have one master account per detector\. | 
| Threat intel sets | 6 | The maximum number of Threat intel sets that you can add per AWS account per Region\. | 
| Trusted IP sets | 1 | The maximum number of trusted IP sets that can be uploaded and activated per AWS account per Region\. You cannot request a quota increase\. | 