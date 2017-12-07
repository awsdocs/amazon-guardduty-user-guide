# GetFindings<a name="get-findings"></a>

Describes Amazon GuardDuty findings specified by finding IDs\.

## Request Syntax<a name="get-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/get
```

```
{
    "findingIds": [
        "string"
    ],
    "sortCriteria": {
        "attributeName": "string",
        "orderBy": "[ASC|DESC]"
    }
}
```

## Request Parameters<a name="get-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detector ID that specifies the GuardDuty service whose findings you want to describe\.  
Type: String  
Required: Yes

**findingIds**  
IDs of the findings that you want to describe\.  
Type: array of Strings\. Minimum number of 0 items\. Maximum number of 50 items\.  
Required: Yes

**sortCriteria**  
Represents the criteria used to query for sorting\.  
Type: sortCriteria  
Required: No    
**attributeName**  
An attribute in a finding that can be queried\.  
Type: String  
**orderBy**  
The order of the sorting request\.  
Type: String\. Valid values: \[ASC | DESC\]

## Response Syntax<a name="get-findings-response-syntax"></a>

```
{
    "findings": [
        {
            "schemaVersion": "string",
            "accountId": "string",
            "region": "string",
            "partition": "string",
            "id": "string",
            "arn": "string",
            "type": "string",
            "resource": {
                "resourceType": "string",
                "instanceDetails": {
                    "iamInstanceProfile": {
                        "arn": "string",
                        "id": "string"
                    },
                    "imageId": "string",
                    "instanceId": "string",
                    "instanceState": "string",
                    "instanceType": "string",
                    "launchTime": "string",
                    "networkInterfaces": [
                        {
                            "publicDnsName": "string",
                            "publicIp": "string",
                            "securityGroups": [
                                {
                                    "groupName": "string",
                                    "groupId": "string"
                                }
                            ],
                            "ipv6Addresses": [
                                "string"
                            ],
                            "privateDnsName": "string",
                            "privateIpAddress": "string",
                            "privateIpAddresses": [
                                {
                                    "privateDnsName": "string",
                                    "privateIpAddress": "string"
                                }
                            ],
                            "subnetId": "string",
                            "vpcId": "string"
                        }
                    ],
                    "availabilityZone": "string",
                    "platform": "string",
                    "productCodes": [
                        {
                            "code": "string",
                            "productType": "string"
                        }
                    ],
                    "tags": [
                        {
                            "key": "string",
                            "value": "string"
                        }
                    ]
                },
                "accessKeyDetails": {
                    "accessKeyId": "string",
                    "principalId": "string",
                    "userType": "string",
                    "userName": "string"
                }
            },
            "service": {
                "serviceName": "string",
                "detectorId": "string",
                "action": {
                    "actionType": "string",
                    "networkConnectionAction": {
                        "connectionDirection": "string",
                        "remoteIpDetails": {
                            "ipAddressV4": "string",
                            "organization": {
                                "asn": "string",
                                "asnOrg": "string",
                                "isp": "string",
                                "org": "string"
                            },
                            "country": {
                                "countryCode": "string",
                                "countryName": "string"
                            },
                            "city": {
                                "cityName": "string"
                            },
                            "geoLocation": {
                                "lat": "double",
                                "lon": "double"
                            }
                        },
                        "remotePortDetails": {
                            "port": "integer",
                            "portName": "string"
                        },
                        "localPortDetails": {
                            "port": "integer",
                            "portName": "string"
                        },
                        "protocol": "string",
                        "blocked": "boolean"
                    },
                    "awsApiCallAction": {
                        "api": "string",
                        "serviceName": "string",
                        "callerType": "string",
                        "remoteIpDetails": {
                            "ipAddressV4": "string",
                            "organization": {
                                "asn": "string",
                                "asnOrg": "string",
                                "isp": "string",
                                "org": "string"
                            },
                            "country": {
                                "countryCode": "string",
                                "countryName": "string"
                            },
                            "city": {
                                "cityName": "string"
                            },
                            "geoLocation": {
                                "lat": "double",
                                "lon": "double"
                            }
                        },
                        "domainDetails": {
                            "domain": "string"
                        }
                    },
                    "dnsRequestAction": {
                        "domain": "string"
                    }
                },
                "resourceRole": "string",
                "additionalInfo": {},
                "eventFirstSeen": "string",
                "eventLastSeen": "string",
                "userFeedback": "string",
                "archived": "boolean",
                "count": "string"
            },
            "title": "string",
            "description": "string",
            "severity": "float",
            "confidence": "float",
            "createdAt": "string",
            "updatedAt": "string"
        }
    ]
}
```

## Response Elements<a name="get-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**findings**  
A list of returned findings\.  
Type: Array    
**schemaVersion**  
Finding's schema version\.  
Type: String  
**accountId**  
The AWS account ID where the activity occurred that prompted GuardDuty to generate a finding\.  
Type: String  
**region**  
The AWS region where the activity occurred that prompted GuardDuty to generate a finding\.  
Type: String  
**partition**  
The AWS resource partition where the activity occurred that prompted GuardDuty to generate a finding\.  
Type: String  
**id**  
Finding ID\.  
Type: String  
**arn**  
Finding ARN\.  
Type: String  
**type**  
Finding type\.  
Type: String  
**resource**  
The AWS resource associated with the activity that prompted GuardDuty to generate a finding\.  
Type: Resource    
**type**  
The type of the AWS resource\.  
Type: String  
**instanceDetails**  
The information about the EC2 instance associated with the activity that prompted GuardDuty to generate a finding\.  
Type: InstanceDetails    
**iamInstanceProfile**  
The profile information of the EC2 instance\.   
Type: IamInstanceProfile    
**arn**  
AWS EC2 instance profile ARN\.  
Type: String  
**id**  
AWS EC2 instance profile ID\.  
Type: String  
**imageId**  
The image ID of the EC2 instance\.   
Type: String  
**instanceId**  
The ID of the EC2 instance\.  
Type: String  
**instanceState**  
The state of the EC2 instance\.  
Type: String  
**instanceType**  
The type of the EC2 instance\.  
Type: String  
**launchTime**  
The launch time of the EC2 instance\.  
Type: String  
**networkInterfaces**  
The network interface information of the EC2 instance\.  
Type: NetworkInterfaces    
**publicDnsName**  
Public DNS name of the EC2 instance\.  
Type: String  
**publicIp**  
Public IP address of the EC2 instance\.  
Type: String  
**securityGroups**  
Security groups associated with the EC2 instance\.  
Type: SecurityGroups    
**groupName**  
EC2 instance's security group name\.  
Type: String  
**groupId**  
EC2 instance's security group ID\.  
Type: String  
**Ipv6Addresses**  
IpV6 address information of the EC2 instance\.  
Type: Array of strings  
**privateDnsName**  
Private DNS name of the EC2 instance\.  
Type: String  
**privateIpAddress**  
Private IP address of the EC2 instance\.  
Type: String  
**privateIpAddresses**  
Other private IP address information of the EC2 instance\.  
Type: PrivateIPAddresses    
**privateDnsName**  
Private DNS name information corresponding to the private IP address\.  
Type: String  
**privateIpAddress**  
Inet private IP address\.  
Type: String  
**subnetId**  
Subnet ID\.  
Type: String  
**vpcId**  
VPC ID\.  
Type: String  
**availabilityZone**  
The availability zone of the EC2 instance\.  
Type: String  
**platform**  
The platform of the EC2 instance\.  
Type: String  
**productCodes**  
The product code of the EC2 instance\.\.  
Type: List of ProductCodes    
**code**  
Product code information\.  
Type: String  
**productType**  
Product code type\.  
Type: String  
**tags**  
The tags of the EC2 instance\.  
Type: Tags    
**key**  
EC2 instance tag key\.  
Type: String  
**value**  
EC2 instance tag value\.  
Type: String  
**accessKeyDetails**  
The IAM access key details \(IAM user information\) of a user that engaged in the activity that prompted GuardDuty to generate a finding\.  
Type: AccessKeyDetails    
**accessKeyId**  
Access key ID of the user\.  
Type: String  
**principalId**  
The principal ID of the user\.  
Type: String  
**userType**  
The type of the user\.  
Type: String  
**userName**  
The name of the user\.  
Type: String  
**service**  
Additional information assigned to the generated finding by GuardDuty\.  
Type: Service    
**serviceName**  
The name of the AWS service \(GuardDuty\) that generated a finding\.  
Type: String  
**detectorId**  
Detector ID for the GuardDuty service\.  
Type: String  
**action**  
Information about the activity described in a finding\.  
Type: Action    
**actionType**  
GuardDuty Finding activity type\.  
Type: String  
**networkConnectionAction**  
Information about the NETWORK\_CONNECTION action described in this finding\.  
Type: NetworkConnectionAction    
**connectionDirection**  
Network connection direction\.  
Type: String  
**remoteIpDetails**  
Remote IP information of the connection\.  
Type: RemoteIpDetails    
**ipAddressV4**  
IPV4 remote address of the connection\.  
Type: String  
**organization**  
ISP Organization information of the remote IP address\.  
Type: Organization    
**asn**  
Autonomous system number of the internet provider of the remote IP address\.  
Type: String  
**asnOrg**  
Organization that registered this ASN\.  
Type: String  
**isp**  
ISP information for the internet provider\.  
Type: String  
**org**  
Name of the internet provider\.  
Type: String  
**country**  
Country information of the remote IP address\.  
Type: Country    
**countryName**  
City name of the remote IP address\.  
Type: String  
**countryCode**  
Country code of the remote IP address\.  
Type: String  
**city**  
City information of the remote IP address\.  
Type: City    
**cityName**  
City name of the remote IP address\.  
Type: String  
**geoLocation**  
Location information of the remote IP address\.  
Type: GeoLocation    
**lon**  
Longitude information of remote IP address\.  
Type: Double  
**lat**  
Latitude information of remote IP address\.  
Type: Double  
**remotePortDetails**  
Remote port information of the connection\.  
Type: RemotePortDetails    
**port**  
Port number of the remote connection\.  
Type: Integer  
**portName**  
Port name of the remote connection\.  
Type: String  
**localPortDetails**  
Local port information of the connection\.  
Type: LocalPortDetails    
**port**  
Port number of the local connection\.  
Type: Integer  
**portName**  
Port name of the local connection\.  
Type: String  
**protocol**  
Network connection protocol\.  
Type: String  
**blocked**  
Network connection blocked information\.  
Type: Boolean  
**awsApiCallAction**  
Information about the AWS\_API\_CALL action described in this finding\.  
Type: AwsApiCallAction    
**api**  
AWS API name\.  
Type: String  
**serviceName**  
AWS service name whose API was invoked\.  
Type: String  
**callerType**  
AWS API caller type\.  
Type: String  
**remoteIpDetails**  
Remote IP information of the connection\.\.  
Type: RemoteIpDetails    
**ipAddressV4**  
IPV4 remote address of the connection\.  
Type: String  
**organization**  
ISP Organization information of the remote IP address\.  
Type: Organization    
**asn**  
Autonomous system number of the internet provider\.  
Type: String  
**asnOrg**  
Organization that registered this ASN\.  
Type: String  
**isp**  
ISP information for the internet provider\.  
Type: String  
**org**  
Name of the internet provider\.  
Type: String  
**country**  
Country information of the remote IP address\.  
Type: Country    
**countryName**  
City name of the remote IP address\.  
Type: String  
**countryCode**  
Country code of the remote IP address\.  
Type: String  
**city**  
City information of the remote IP address\.  
Type: City    
**cityName**  
City name of the remote IP address\.  
Type: String  
**geoLocation**  
Location information of the remote IP address\.  
Type: GeoLocation    
**lon**  
Longitude information of remote IP address\.  
Type: Double  
**lat**  
Latitude information of remote IP address\.  
Type: Double  
**domainDetails**  
Domain information for the AWS API call\.  
Type: DomainDetails    
**domain**  
Domain information for the AWS API call\.  
Type: String  
**dnsRequestAction**  
Information about the DNS\_REQUEST action described in this finding\.  
Type: DnsRequestAction    
**domain**  
Domain information for the DNS request\.  
Type: String  
**resourceRole**  
Resource role information for this finding\.  
Type: String  
**additionalInfo**  
List of additional information for this finding\.  
**eventFirstSeen**  
First seen timestamp of the activity that prompted GuardDuty to generate this finding\.  
Type: String  
**eventLastSeen**  
Last seen timestamp of the activity that prompted GuardDuty to generate this finding\.  
Type: String  
**userFeedback**  
Feedback left about the finding\.  
Type: String  
**archived**  
Indicates whether this finding is archived\.  
Type: Boolean  
**count**  
Total count of the occurrences of this finding type\.  
Type: String  
**title**  
The title of a finding\.  
Type: String  
**description**  
The description of a finding\.\.  
Type: String  
**severity**  
The severity of a finding\.  
Type: float  
**confidence**  
The confidence level of a finding\.  
Type: float  
**createdAt**  
The time stamp at which a finding was generated\.  
Type: string  
**updatedAt**  
The time stamp at which a finding was last updated\.  
Type: string

## Errors<a name="get-findings-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information

**InvalidInputException**

The request is rejected because an invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because one or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter detectorId has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request was rejected because the parameter findingCriteria has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because of invalid finding statistic type is specified\.

HTTP Status Code: 400 

**NoSuchEntityheException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 