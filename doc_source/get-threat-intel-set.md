# GetThreatIntelSet<a name="get-threat-intel-set"></a>

Returns the properties of the ThreatIntelSet that is specified by the ThreatIntelSet ID\. 

**Important**  
If a user from a member account runs this API, the response contains the ThreatIntelSets uploaded by the master account\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage ThreatIntelSets\. ThreatIntelSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="get-threat-intel-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/threatintelset/{threatIntelSetId}
```

**Body:**

```
detectorId : "string"
threatIntelSetId : "string"
```

## Path Parameters<a name="get-threat-intel-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose ThreatIntelSet properties you want to return\.  
Type: String  
Required: Yes

**threatIntelSetId**  
The unique ID that specifies the ThreatIntelSet whose properties you want to return\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-threat-intel-response-syntax"></a>

```
{
    "name": "string",
    "location": "string",
    "format": "[TXT | STIX | OTX_CSV | ALIEN_VAULT | PROOF_POINT | FIRE_EYE]",
    "status": "[INACTIVE | ACTIVATING | ACTIVE | DEACTIVATING | ERROR | DELETE_PENDING | DELETED]"
}
```

## Response Elements<a name="get-threat-intel-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**name**  
The name of the ThreatIntelSet\.  
Type: String

**location**  
The URI of the file that contains the ThreatIntelSet\.  
Type: String

**format**  
The format of the file that contains the ThreatIntelSet\.  
Type: String  
Valid values: `TXT` \| `STIX` \| `OTX_CSV` \| `ALIEN_VAULT` \| `PROOF_POINT` \| `FIRE_EYE`

**status**  
The current status of the `ThreatIntelSet`\.  
Type: String  
Valid values: `INACTIVE` \| `ACTIVATING` \| `ACTIVE` \| `DEACTIVATING` \| `ERROR` \| `DELETE_PENDING` \| `DELETED`

## Errors<a name="get-threat-intel-errors"></a>

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

The request is rejected\. An invalid `threatIntelSetId` is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. An invalid `threatIntelSetId` is specified\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-threat-intel-set-example"></a>

**Sample Request**

```
GET /detector/12abc34d567e8fa901bc2d34e56789f0/threatintelset/8cb094db7082fd0db09479755d215dba HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T200105Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 137
Date: Wed, 24 Jan 2018 20:01:06 GMT
x-amzn-RequestId: 5040403c-0141-11e8-a09c-f1d8e1e0b9aa
X-Amzn-Trace-Id: sampled=0;root=1-5a68e602-a127df9b53e8b229624cd03e
X-Cache: Miss from cloudfront
Via: 1.1 08f323eee70ddda7af34d5feb414ce27.cloudfront.net (CloudFront)
X-Amz-Cf-Id: njPvvQsAq4ShiJcvOx0wF6WMmxdqrMHTnzX7Utni7r2_EFFVmsfn6w==
Connection: Keep-alive
{  
   "name":"ThreatIntelSet",
   "location":"https://s3.amazonaws.com/guarddutylists/threatintelset.txt",
   "format":"TXT",
   "status":"ACTIVE"
}
```