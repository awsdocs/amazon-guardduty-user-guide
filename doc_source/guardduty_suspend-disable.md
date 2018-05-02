# Suspending or Disabling Amazon GuardDuty<a name="guardduty_suspend-disable"></a>

You can use the GuardDuty console to suspend or disable GuardDuty\. 
+ If you suspend GuardDuty, it no longer monitors the security of your AWS environment or generates new findings\. Your existing findings remain intact and are not affected by the GuardDuty suspension\. You can choose to re\-enable GuardDuty later\. 
**Important**  
You are not charged for using GuardDuty when the service is suspended\.
+ If you disable GuardDuty, your existing findings and the GuardDuty configuration are lost and can't be recovered\. If you want to save your existing findings, you must export them before you disable GuardDuty\.

**To suspend or disable GuardDuty \(console\)**

1. Open the GuardDuty console at [https://console\.aws\.amazon\.com/guardduty](https://console.aws.amazon.com/guardduty)\. 

1. In the navigation pane, under **Settings**, choose **General**\.

1. Choose either **Suspend GuardDuty** or **Disable GuardDuty**\. Then choose **Save settings**\.