# ListThreatIntelSets<a name="list-threat-intel-set"></a>

Lists the ThreatIntelSets of the GuardDuty service that are specified by the detector ID\. 

**Important**  
If a user from a member account runs this API, the response contains the ThreatIntelSets uploaded by the master account\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage ThreatIntelSets\. ThreatIntelSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="list-threat-intel-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/threatintelset
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Path Parameters<a name="list-threat-intel-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose ThreatIntelSets you want to list\.  
Type: String  
Required: Yes

## Request Parameters<a name="list-threat-intel-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
Indicates the maximum number of items that you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListThreatIntelSets` operation\. For subsequent calls to the action, fill `nextToken` in the request with the value of `NextToken` from the previous response to continue listing data\.  
Type: String  
Required: No

## Response Syntax<a name="list-threat-intel-response-syntax"></a>

If the action is successful, the service sends back an HTTP 200 response\.

```
{
    "threatIntelSetIds": [
        "string"
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-threat-intel-response-parameters"></a>

The following data is returned in JSON format by the service\.

**threatIntelSetIds**  
A list of IDs that specify the ThreatIntelSet objects of the specified GuardDuty service\.  
Type: array of Strings  
Constraints: Minimum number of 0 items\. Maximum number of 50 items\.

**nextToken**  
The token that is required for pagination\.  
Type: String

## Errors<a name="list-threat-intel-errors"></a>

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

The request is rejected\. The parameter `maxResults` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `maxResults` is out\-of\-bounds\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="list-threat-intel-sets-example"></a>

**Sample Request**

```
GET /detector/12abc34d567e8fa901bc2d34e56789f0/threatintelset HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T195513Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 75
Date: Wed, 24 Jan 2018 19:55:14 GMT
x-amzn-RequestId: 7e5a935c-0140-11e8-a9ab-51b1993e9c62
X-Amzn-Trace-Id: sampled=0;root=1-5a68e4a2-f59a246addd680e790b6c2e0
X-Cache: Miss from cloudfront
Via: 1.1 7cbd9c5a78702cfae1a7ed58e294736e.cloudfront.net (CloudFront)
X-Amz-Cf-Id: -LPBY0XNC0h0ifRWzhb9Lo4HLRJA2BxaFfLzzvVeAhXrPkuqlcnBpg==
Connection: Keep-alive
{  
   "threatIntelSetIds":[  
      "8cb094db7082fd0db09479755d215dba"
   ],
   "nextToken":null
}
```