# DeleteThreatIntelSet<a name="delete-threat-intel-set"></a>

Deletes the ThreatIntelSet that is specified by the ThreatIntelSet ID\. 

**Important**  
Users from GuardDuty member accounts cannot run this API\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage ThreatIntelSets\. ThreatIntelSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="delete-threat-intel-request-syntax"></a>

```
DELETE https://<endpoint>/detector/{detectorId}/threatintelset/{threatIntelSetId}
```

**Body:**

```
detectorId : "string"
threatIntelSetId : "string"
```

## Path Parameters<a name="delete-threat-intel-path-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detector ID that specifies the GuardDuty service whose `ThreatIntelSet` you want to delete\.  
Type: String  
Required: Yes

**threatIntelSetId**  
The unique ID that specifies the `ThreatIntelSet` that you want to delete\.  
Type: String  
Required: Yes

## Response Syntax<a name="delete-threat-intel-response-syntax"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="delete-threat-intel-errors"></a>

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

**InvalidInputException**

The request is rejected\. Member accounts cannot manage IPSets or ThreatIntelSets\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. An invalid `threatIntelSetId` is specified\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. The caller is not authorized to call this API\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="delete-threat-intel-set-example"></a>

**Sample Request**

```
DELETE /detector/12abc34d567e8fa901bc2d34e56789f0/threatintelset/8cb094db7082fd0db09479755d215dba HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T212824Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Wed, 24 Jan 2018 21:28:26 GMT
x-amzn-RequestId: 8330e867-014d-11e8-b00e-f1d94214241f
X-Amzn-Trace-Id: sampled=0;root=1-5a68fa7a-6254473316398a8e7e769f64
X-Cache: Miss from cloudfront
Via: 1.1 85ddca57b96353e9e4cd2660cf65d9da.cloudfront.net (CloudFront)
X-Amz-Cf-Id: RntOBwBWFz8ljwXOrdnWfXXfJz12nRQHOiHngFq8fKrgW_b7K5iL4Q==
Connection: Keep-alive
```