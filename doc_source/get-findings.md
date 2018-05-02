# GetFindings<a name="get-findings"></a>

Describes Amazon GuardDuty findings that are specified by finding IDs\.

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

## Path Parameters<a name="get-findings-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose findings you want to describe\.  
Type: String  
Required: Yes

## Request Parameters<a name="get-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**findingIds**  
The IDs of the findings that you want to describe\.  
Type: array of Strings\. Minimum number of 0 items\. Maximum number of 50 items\.  
Required: Yes

**sortCriteria**  
Represents the criteria used to query for sorting\.  
Type: sortCriteria  
Required: No    
**attributeName**  
An attribute in a finding that can be queried\.  
You can only use the following attributes to sort findings:  
+ accountId
+ severity
+ confidence
+ type
+ service\.eventFirstSeen
+ service\.eventLastSeen
+ createdAt

  Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.
+ updatedAt

  Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.
+ service\.action\.networkConnectionAction\.remoteIpDetails\.ipAddressV4
+ resource\.instanceDetails\.instanceId
+ service\.action\.networkConnectionAction\.localPortDetails\.port
+ service\.action\.networkConnectionAction\.remotePortDetails\.port
+ service\.action\.networkConnectionAction\.remoteIpDetails\.country\.countryName
+ service\.action\.networkConnectionAction\.protocol, service\.action\.awsApiCallAction\.api
+ service\.action\.awsApiCallAction\.serviceName
+ service\.action\.networkConnectionAction\.blocked
+ service\.count
Type: String  
**orderBy**  
The order of the sorting request\.  
Type: String\. Valid values: \[`ASC` \| `DESC`\]

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
A finding's schema version\.  
Type: String  
**accountId**  
The AWS account ID where the activity occurred that prompted GuardDuty to generate a finding\.  
Type: String  
**region**  
The AWS Region where the activity occurred that prompted GuardDuty to generate a finding\.  
Type: String  
**partition**  
The AWS resource partition where the activity occurred that prompted GuardDuty to generate a finding\.  
Type: String  
**id**  
The finding ID\.  
Type: String  
**arn**  
The finding ARN\.  
Type: String  
**type**  
The finding type\.  
Type: String  
**resource**  
The AWS resource that is associated with the activity that prompted GuardDuty to generate a finding\.  
Type: Resource    
**type**  
The type of the AWS resource\.  
Type: String  
**instanceDetails**  
The information about the EC2 instance that is associated with the activity that prompted GuardDuty to generate a finding\.  
Type: InstanceDetails    
**iamInstanceProfile**  
The profile information of the EC2 instance\.   
Type: IamInstanceProfile    
**arn**  
The AWS EC2 instance profile ARN\.  
Type: String  
**id**  
The AWS EC2 instance profile ID\.  
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
The public DNS name of the EC2 instance\.  
Type: String  
**publicIp**  
The public IP address of the EC2 instance\.  
Type: String  
**securityGroups**  
The security groups that are associated with the EC2 instance\.  
Type: SecurityGroups    
**groupName**  
The security group name of the EC2 instance\.  
Type: String  
**groupId**  
The security group ID of the EC2 instance\.   
Type: String  
**Ipv6Addresses**  
The IpV6 address information of the EC2 instance\.  
Type: Array of strings  
**privateDnsName**  
The private DNS name of the EC2 instance\.  
Type: String  
**privateIpAddress**  
The private IP address of the EC2 instance\.  
Type: String  
**privateIpAddresses**  
Other private IP address information of the EC2 instance\.  
Type: PrivateIPAddresses    
**privateDnsName**  
The private DNS name information that corresponds to the private IP address\.  
Type: String  
**privateIpAddress**  
The Inet private IP address\.  
Type: String  
**subnetId**  
The subnet ID\.  
Type: String  
**vpcId**  
The VPC ID\.  
Type: String  
**availabilityZone**  
The Availability Zone of the EC2 instance\.  
Type: String  
**platform**  
The platform of the EC2 instance\.  
Type: String  
**productCodes**  
The product code of the EC2 instance\.  
Type: List of ProductCodes    
**code**  
The product code information\.  
Type: String  
**productType**  
The product code type\.  
Type: String  
**tags**  
The tags of the EC2 instance\.  
Type: Tags    
**key**  
The EC2 instance tag key\.  
Type: String  
**value**  
The EC2 instance tag value\.  
Type: String  
**accessKeyDetails**  
The IAM access key details \(IAM user information\) of a user that engaged in the activity that prompted GuardDuty to generate a finding\.  
Type: AccessKeyDetails    
**accessKeyId**  
The access key ID of the user\.  
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
The detector ID for the GuardDuty service\.  
Type: String  
**action**  
Information about the activity that is described in a finding\.  
Type: Action    
**actionType**  
The activity type of the GuardDuty finding\.  
Type: String  
**networkConnectionAction**  
Information about the `NETWORK_CONNECTION` action that is described in this finding\.  
Type: NetworkConnectionAction    
**connectionDirection**  
The network connection direction\.  
Type: String  
**remoteIpDetails**  
The remote IP information of the connection\.  
Type: RemoteIpDetails    
**ipAddressV4**  
The IPV4 remote address of the connection\.  
Type: String  
**organization**  
The ISP organization information of the remote IP address\.  
Type: Organization    
**asn**  
The autonomous system number of the internet provider of the remote IP address\.  
Type: String  
**asnOrg**  
The organization that registered this ASN\.  
Type: String  
**isp**  
The ISP information for the internet provider\.  
Type: String  
**org**  
The name of the internet provider\.  
Type: String  
**country**  
The country information of the remote IP address\.  
Type: Country    
**countryName**  
The city name of the remote IP address\.  
Type: String  
**countryCode**  
The country code of the remote IP address\.  
Type: String  
**city**  
The city information of the remote IP address\.  
Type: City    
**cityName**  
The city name of the remote IP address\.  
Type: String  
**geoLocation**  
The location information of the remote IP address\.  
Type: GeoLocation    
**lon**  
The longitude information of the remote IP address\.  
Type: Double  
**lat**  
The latitude information of the remote IP address\.  
Type: Double  
**remotePortDetails**  
The remote port information of the connection\.  
Type: RemotePortDetails    
**port**  
The port number of the remote connection\.  
Type: Integer  
**portName**  
The port name of the remote connection\.  
Type: String  
**localPortDetails**  
The local port information of the connection\.  
Type: LocalPortDetails    
**port**  
The port number of the local connection\.  
Type: Integer  
**portName**  
The port name of the local connection\.  
Type: String  
**protocol**  
The network connection protocol\.  
Type: String  
**blocked**  
The network connection blocked information\.  
Type: Boolean  
**awsApiCallAction**  
Information about the `AWS_API_CALL` action that is described in this finding\.  
Type: AwsApiCallAction    
**api**  
The AWS API name\.  
Type: String  
**serviceName**  
The AWS service name whose API was invoked\.  
Type: String  
**callerType**  
The AWS API caller type\.  
Type: String  
**remoteIpDetails**  
The remote IP information of the connection\.  
Type: RemoteIpDetails    
**ipAddressV4**  
The IPV4 remote address of the connection\.  
Type: String  
**organization**  
The ISP organization information of the remote IP address\.  
Type: Organization    
**asn**  
The autonomous system number of the internet provider\.  
Type: String  
**asnOrg**  
The organization that registered this ASN\.  
Type: String  
**isp**  
The ISP information for the internet provider\.  
Type: String  
**org**  
The name of the internet provider\.  
Type: String  
**country**  
The country information of the remote IP address\.  
Type: Country    
**countryName**  
The city name of the remote IP address\.  
Type: String  
**countryCode**  
The country code of the remote IP address\.  
Type: String  
**city**  
The city information of the remote IP address\.  
Type: City    
**cityName**  
The city name of the remote IP address\.  
Type: String  
**geoLocation**  
The location information of the remote IP address\.  
Type: GeoLocation    
**lon**  
The longitude information of the remote IP address\.  
Type: Double  
**lat**  
The latitude information of the remote IP address\.  
Type: Double  
**domainDetails**  
The domain information for the AWS API call\.  
Type: DomainDetails    
**domain**  
The domain information for the AWS API call\.  
Type: String  
**dnsRequestAction**  
Information about the `DNS_REQUEST` action that is described in this finding\.  
Type: DnsRequestAction    
**domain**  
Domain information for the DNS request\.  
Type: String  
**resourceRole**  
Resource role information for this finding\.  
Type: String  
**additionalInfo**  
The list of additional information for this finding\.  
**eventFirstSeen**  
The first seen timestamp of the activity that prompted GuardDuty to generate this finding\.  
Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.  
**eventLastSeen**  
The last seen timestamp of the activity that prompted GuardDuty to generate this finding\.  
Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.  
**userFeedback**  
Feedback provided by a user about the finding\.  
Type: String  
**archived**  
Specifies whether this finding is archived\.  
Type: Boolean  
**count**  
The total count of the occurrences of this finding type\.  
Type: String  
**title**  
The title of a finding\.  
Type: String  
**description**  
The description of a finding\.  
Type: String  
**severity**  
The severity of a finding\.  
Type: float  
**confidence**  
The confidence level of a finding\.  
Type: float  
**createdAt**  
The time stamp at which a finding was generated\.  
Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.  
**updatedAt**  
The time stamp at which a finding was last updated\.  
Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.

## Errors<a name="get-findings-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. One or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `detectorId` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `findingCriteria` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. An invalid finding statistic type is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-findings-example"></a>

**Sample Request**

```
POST /detector/c6b0be64463ff852400d8ae5b2353866/findings/get HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 52
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T232830Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "findingIds":[  
      "9cb0be64df8ba1df249c45eb8a0bf584"
   ]
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 3290
Date: Fri, 09 Feb 2018 23:28:31 GMT
x-amzn-RequestId: f0876f86-0df0-11e8-900a-559d93fe6c5b
X-Amzn-Trace-Id: sampled=0;root=1-5a7e2e9f-d77815a82381c4f592d527bd
X-Cache: Miss from cloudfront
Via: 1.1 39f9e0f028321e95b5ebd1cd55661fd6.cloudfront.net (CloudFront)
X-Amz-Cf-Id: FWbQHHuN2DoUqO9CxoJfxv0MhjH9v2t9uPRf_d_uIBRD7tEXvhmINg==
Connection: Keep-alive
{
   "findings":[
      {
         "schemaVersion":"2.0",
         "accountId":"123456789012",
         "region":"us-west-2",
         "partition":"aws",
         "id":"9cb0be64df8ba1df249c45eb8a0bf584",
         "arn":"arn:aws:guardduty:us-west-2:123456789012:detector/c6b0be64463ff852400d8ae5b2353866/finding/9cb0be64df8ba1df249c45eb8a0bf584",
         "type":"UnauthorizedAccess:EC2/RDPBruteForce",
         "resource":{
            "resourceType":"Instance",
            "instanceDetails":{
               "instanceId":"i-99999999",
               "instanceType":"m3.xlarge",
               "launchTime":"2016-08-02T02:05:06Z",
               "platform":null,
               "productCodes":[
                  {
                     "productCodeId":"GeneratedFindingProductCodeId",
                     "productCodeType":"GeneratedFindingProductCodeType"
                  }
               ],
               "iamInstanceProfile":{
                  "arn":"GeneratedFindingInstanceProfileArn",
                  "id":"GeneratedFindingInstanceProfileId"
               },
               "networkInterfaces":[
                  {
                     "ipv6Addresses":[

                     ],
                     "privateDnsName":"GeneratedFindingPrivateDnsName",
                     "privateIpAddress":"10.0.0.1",
                     "privateIpAddresses":[
                        {
                           "privateDnsName":"GeneratedFindingPrivateName",
                           "privateIpAddress":"10.0.0.1"
                        }
                     ],
                     "subnetId":"GeneratedFindingSubnetId",
                     "vpcId":"GeneratedFindingVPCId",
                     "securityGroups":[
                        {
                           "groupName":"GeneratedFindingSecurityGroupName",
                           "groupId":"GeneratedFindingSecurityId"
                        }
                     ],
                     "publicDnsName":"GeneratedFindingPublicDNSName",
                     "publicIp":"198.51.100.0"
                  }
               ],
               "tags":[
                  {
                     "key":"GeneratedFindingInstaceTag1",
                     "value":"GeneratedFindingInstaceValue1"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag2",
                     "value":"GeneratedFindingInstaceTagValue2"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag3",
                     "value":"GeneratedFindingInstaceTagValue3"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag4",
                     "value":"GeneratedFindingInstaceTagValue4"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag5",
                     "value":"GeneratedFindingInstaceTagValue5"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag6",
                     "value":"GeneratedFindingInstaceTagValue6"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag7",
                     "value":"GeneratedFindingInstaceTagValue7"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag8",
                     "value":"GeneratedFindingInstaceTagValue8"
                  },
                  {
                     "key":"GeneratedFindingInstaceTag9",
                     "value":"GeneratedFindingInstaceTagValue9"
                  }
               ],
               "instanceState":"running",
               "availabilityZone":"GeneratedFindingInstaceAvailabilityZone",
               "imageId":"ami-99999999",
               "imageDescription":"GeneratedFindingInstaceImageDescription"
            }
         },
         "service":{
            "serviceName":"guardduty",
            "detectorId":"c6b0be64463ff852400d8ae5b2353866",
            "action":{
               "actionType":"NETWORK_CONNECTION",
               "networkConnectionAction":{
                  "connectionDirection":"INBOUND",
                  "remoteIpDetails":{
                     "ipAddressV4":"198.51.100.0",
                     "organization":{
                        "asn":"-1",
                        "asnOrg":"GeneratedFindingASNOrg",
                        "isp":"GeneratedFindingISP",
                        "org":"GeneratedFindingORG"
                     },
                     "country":{
                        "countryName":"GeneratedFindingCountryName"
                     },
                     "city":{
                        "cityName":"GeneratedFindingCityName"
                     },
                     "geoLocation":{
                        "lat":0,
                        "lon":0
                     }
                  },
                  "remotePortDetails":{
                     "port":1067,
                     "portName":"Unknown"
                  },
                  "localPortDetails":{
                     "port":3389,
                     "portName":"RDP"
                  },
                  "protocol":"TCP",
                  "blocked":false
               }
            },
            "resourceRole":"TARGET",
            "additionalInfo":{
               "sample":true
            },
            "eventFirstSeen":"2018-02-09T22:57:31.927Z",
            "eventLastSeen":"2018-02-09T22:57:31.927Z",
            "archived":false,
            "count":1,
            "userFeedback":"NOT_USEFUL"
         },
         "severity":2,
         "createdAt":"2018-02-09T22:57:31.927Z",
         "updatedAt":"2018-02-09T22:57:31.927Z",
         "title":"198.51.100.0 is performing RDP brute force attacks against i-99999999.",
         "description":"198.51.100.0 is performing RDP brute force attacks against i-99999999. Brute force attacks are used to gain unauthorized access to your instance by guessing the RDP password."
      }
   ]
}
```