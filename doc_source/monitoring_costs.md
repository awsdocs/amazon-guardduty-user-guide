# Estimating GuardDuty costs in GuardDuty<a name="monitoring_costs"></a>

You can use the GuardDuty console and API operations to estimate how much GuardDuty will cost you per month\. During the 30\-day free trial period, the cost estimation projects what your estimated costs will be after the free trial period\. If you are operating in a multi\-account environment, your GuardDuty master account can monitor cost metrics for all of your member accounts\.

**You can view cost estimation based on the following metrics:**
+ **Account ID** \- Lists the estimated cost for your account, or for your member accounts if you are operating as a GuardDuty master account\. 
+ **Data source** \- Lists the estimated cost on the specified data source for the following GuardDuty data source types: VPC Flow Logs, CloudTrail Management logs, S3 Data Event logs, or DNS logs\. 
+ **S3 buckets** \- Lists the estimated cost for S3 data events on a specified bucket or the most expensive buckets for accounts in your environment\. 
**Note**  
S3 bucket statistics are only available if S3 Protection is enabled for the account\. For more information see [Amazon S3 protection in Amazon GuardDuty](s3_detection.md)\.

## Understanding how usage costs are calculated<a name="usage-calculations"></a>

When you use the cost monitoring feature of GuardDuty, it is important to understand how the estimates are calculated\. The estimates displayed in GuardDuty may differ slightly from those in your Billing and Cost Management console\. Note the following about how GuardDuty cost estimates are calculated\.
+ The GuardDuty usage estimate is for the current Region only\.
+ The GuardDuty usage estimate is an average daily cost based on the past 7 to 30 days of usage\. 
**Note**  
For newly enabled detectors or data sources with fewer than seven days of usage, the cost is listed as **Pending**\.
+ The free trial estimate reflects only those data sources currently in a free trial period\.
+ The GuardDuty usage estimate includes GuardDuty volume pricing discounts per Region, as detailed on the [Amazon GuardDuty Pricing](http://aws.amazon.com/guardduty/pricing/) page, but only for individual accounts meeting the volume pricing tiers\. Volume pricing discounts are not included in estimates for combined total usage between accounts within an Organization\. For information about combined usage volume discount pricing, see [AWS Billing: Volume Discounts](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/useconsolidatedbilling-discounts.html)\.

## Review GuardDuty usage statistics \(Console\)<a name="usage_stats_thru_console"></a>

1. Log into the [https://console\.aws\.amazon\.com/guardduty/](https://console.aws.amazon.com/guardduty/) console using the GuardDuty master account\.

1. In the navigation pane, choose **Usage**\.

1. GuardDuty master accounts with members see a list of all managed accounts\. Single accounts see a breakdown by data source\.

   If you have member accounts, you can view statistics for an individual account by selecting that account in the Accounts table\. If S3 protection is enabled for the selected account, the top S3 buckets by usage cost are displayed in the **By data source** panel\.
**Note**  
A green dot indicates that a free trial period is active\.

## Review GuardDuty usage statistics \(API\)<a name="usage_stats_thru_api"></a>

To view cost metrics, run the [getUsageStatistics](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_getUsageStatistics.html) API operation using the credentials of the AWS account of the Organizations master\. Supply the following information to run the command:
+ \(Required\) Specify the Regional GuardDuty detector ID of the account you want to retrieve statistics for\.
+ \(Required\) Specify the type of statistics to retrieve: `SUM_BY_ACCOUNT | SUM_BY_DATA_SOURCE | SUM_BY_RESOURCE | TOP_RESOURCES`\.
+ \(Required\) Specify at least one data source to query from the following options: `FLOW_LOGS | CLOUD_TRAIL | DNS_LOGS | S3_LOGS`\.
+ \(Optional\) Specify a list of account IDs to retrieve usage statistics for\.

You can also use the AWS Command Line\. Run the command below, replacing the example detector ID with your own, to get the sum of usage for all data sources\. For single accounts, this command returns the cost over the past 30 days for your account only\. If you are a GuardDuty master with member accounts, you see costs listed by account for all members\.

```
aws guardduty get-usage-statistics --detector-id 12abc34d567e8fa901bc2d34e56789f0 --usage-statistic-type SUM_BY_ACCOUNT --usage-criteria '{"DataSources":["S3_LOGS","CLOUD_TRAIL","DNS_LOGS","FLOW_LOGS"]}'
```