# Filtering Findings<a name="guardduty_filter-findings"></a>

using the Amazon GuardDuty console you can easily create finding filters\. A finding filter allows you to view findings matching the criteria you specify, while filtering out any unmatched findings\. The easiest way to create filters is through the GuardDuty console, but you can also create them with the [CreateFilter](https://docs.aws.amazon.com/guardduty/latest/APIReference/API_CreateFilter.html) API using JSON\. Review the following sections to understand how to create a filter in the console\. To use these filters to automatically archive, or suppress, incoming findings see [Suppression Rules](suppression_rule.md)\.

## Create Filters in the GuardDuty Console<a name="filter_console"></a>

Finding filters can be created and tested through the GuardDuty UI\. Filters created through the UI can be saved for use in suppression rules or future filter operations\.

**To filter findings \(console\)**

1. Choose the **Add filter criteria** bar above the displayed list of your GuardDuty findings\.

1. In the expanded list of criteria, select the attribute that you want to specify as the criteria for your filter\. For example, **Account ID** and/or **Action type**\. When creating filters be aware of the following:
   + Filters do not accept wild cards\. 
   + You can specify a minimum of one attribute up to a maximum of 50 attributes as the criteria for a particular filter\. 
   + When you use the 'equal to' or 'not equal to' condition to filter on an attribute value, such as Account ID, you can specify a maximum of 50 values\.
   + Each filter criteria attribute is evaluated as an `AND` operator, multiple values for the same attribute are evaluated as `AND/OR`\.
**Note**  
For the a list of attributes that you can specify as filter criteria, see the Filter Criteria table on this page\.

1. In the displayed text field, specify a value for each selected attribute and then select **Apply**\.
**Note**  
 After you apply a filter, you can convert the filter to exclude findings that match the filter by choosing the black dot to the left side of the filter name\. This effectively creates a "not equals" filter for the selected attribute\.

1. To save the specified attributes and their values \(filter criteria\) as a filter, select **Save**\. Provide the filter name and description, and then choose **Done**\.

## Filter Criteria<a name="filter_criteria"></a>

 When creating filters or sorting findings using the API operations you must specify filter criteria in JSON\. These filter criteria correlate to a finding's details JSON\. The following table contains a list of the console display names for filter criteria matched to their equivalent JSON field name\.


| Console field name | JSON field name | 
| --- | --- | 
| Account ID | accountId | 
| Confidence | confidence | 
| Finding ID | id | 
| Region | region | 
| Access Key ID | resource\.accessKeyDetails\.accessKeyId | 
| Principal ID | resource\.accessKeyDetails\.principalId | 
| Username | resource\.accessKeyDetails\.userName | 
| User type | resource\.accessKeyDetails\.userType | 
| IAM instance profile ID | resource\.instanceDetails\.iamInstanceProfile\.id | 
| Instance ID | resource\.instanceDetails\.instanceId | 
| Instance Type | resource\.instanceDetails\.instanceType | 
| Launch Time | resource\.instanceDetails\.launchTime | 
| Instance image ID | resource\.instanceDetails\.networkInterfaces\.imageID | 
| IPv6 address | resource\.instanceDetails\.networkInterfaces\.ipv6Addresses | 
| Private IPv4 address | resource\.instanceDetails\.networkInterfaces\.privateIpAddresses\.privateIpAddress | 
| Public DNS name | resource\.instanceDetails\.networkInterfaces\.publicDnsName | 
| Public IP | resource\.instanceDetails\.networkInterfaces\.publicIp | 
| Security group ID | resource\.instanceDetails\.networkInterfaces\.securityGroups\.groupId | 
| Security group name | resource\.instanceDetails\.networkInterfaces\.securityGroups\.groupName | 
| Subnet ID | resource\.instanceDetails\.networkInterfaces\.subnetId | 
| VPC ID | resource\.instanceDetails\.networkInterfaces\.vpcId | 
| Outpost ARN | resource\.instanceDetails\.outpostARN | 
| Tag key | resource\.instanceDetails\.tags\.key | 
| Tag value | resource\.instanceDetails\.tags\.value | 
| Resource type | resource\.resourceType | 
| Bucket permissions | resource\.s3BucketDetails\.publicAccess\.effectivePermissions | 
| Bucket name  | resource\.s3BucketDetails\.name | 
| Bucket tag key | resource\.s3BucketDetails\.tags\.key | 
| Bucket tag value | resource\.s3BucketDetails\.tags\.value | 
| Bucket type | resource\.s3BucketDetails\.type | 
| Action type | service\.action\.actionType | 
| API called | service\.action\.awsApiCallAction\.api | 
| API caller type | service\.action\.awsApiCallAction\.callerType | 
| API caller city | service\.action\.awsApiCallAction\.remoteIpDetails\.city\.cityName | 
| API caller country | service\.action\.awsApiCallAction\.remoteIpDetails\.country\.countryName | 
| API caller IPv4 address | service\.action\.awsApiCallAction\.remoteIpDetails\.ipAddressV4 | 
| API caller ASN ID | service\.action\.awsApiCallAction\.remoteIpDetails\.organization\.asn | 
| API caller ASN name | service\.action\.awsApiCallAction\.remoteIpDetails\.organization\.asnOrg | 
| API caller service name | service\.action\.awsApiCallAction\.serviceName | 
| DNS request domain | service\.action\.dnsRequestAction\.domain | 
| Network connection blocked | service\.action\.networkConnectionAction\.blocked | 
| Network connection direction | service\.action\.networkConnectionAction\.connectionDirection | 
| Network connection local port | service\.action\.networkConnectionAction\.localPortDetails\.port | 
| Network connection protocol | service\.action\.networkConnectionAction\.protocol | 
| Network connection city | service\.action\.networkConnectionAction\.remoteIpDetails\.city\.cityName | 
| Network connection country | service\.action\.networkConnectionAction\.remoteIpDetails\.country\.countryName | 
| Network connection remote IPv4 address | service\.action\.networkConnectionAction\.remoteIpDetails\.ipAddressV4 | 
| Network connection remote IP ASN ID | service\.action\.networkConnectionAction\.remoteIpDetails\.organization\.asn | 
| Network connection remote IP ASN name | service\.action\.networkConnectionAction\.remoteIpDetails\.organization\.asnOrg | 
| Network connection remote port | service\.action\.networkConnectionAction\.remotePortDetails\.port | 
| Threat list name | service\.additionalInfo\.threatListName | 
| Archived | service\.archived | 
| Local IP | service\.localIpDetails\.ipAddressV4 | 
| Resource role | service\.resourceRole | 
| Severity | severity | 
| Finding type | type | 
| Updated at | updatedAt | 