# UpdateThreatIntelSet<a name="update-threat-intel-set"></a>

Updates the ThreatIntelSet that is specified by the ThreatIntelSet ID\. 

**Important**  
Users from GuardDuty member accounts cannot run this API\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage ThreatIntelSets\. ThreatIntelSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="update-threat-intel-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/threatintelset/{threatIntelSetId}
```

**Body:**

```
{
    "name": "string",
    "location": "string",
    "activate": "boolean"
}
```

## Path Parameters<a name="update-threat-intel-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose ThreatIntelSet you want to update\.  
Type: String  
Required: Yes

**threatIntelSetId**  
The unique ID that specifies the ThreatIntelSet that you want to update\.  
Type: String  
Required: Yes

## Request Parameters<a name="update-threat-intel-request-parameters"></a>

The request accepts the following data in JSON format\.

**name**  
The updated friendly name for the ThreatIntelSet\.  
Type: String  
Required: No

**location**  
The updated URI of the file that contains the ThreatIntelSet\.  
Type: String  
Required: No

**activate**  
Specifies whether the ThreateIntelSet is active or not\.  
Required: No  
Type: Boolean

## Response Syntax<a name="update-threat-intel-response-syntax"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="update-threat-intel-errors"></a>

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

The request is rejected\. An invalid `ipSetId` is specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. Member accounts cannot manage IPSets or ThreatIntelSets\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. An invalid `ipSetId` is specified\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. The caller is not authorized to call this API\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. No role was found\.

HTTP Status Code: 400 

**BadRequestException**

The request is rejected\. The service can't assume the service role\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. You do not have the required `iam:PutRolePolicy` permission\.

HTTP Status Code: 400 

**BadRequestException**

The request is rejected\. The specified service role is not a service\-linked role\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="update-threat-intel-set-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/threatintelset/8cb094db7082fd0db09479755d215dba HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 19
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T212506Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "activate":false
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Wed, 24 Jan 2018 21:25:09 GMT
x-amzn-RequestId: 0d3e8284-014d-11e8-beb7-958380c0c8da
X-Amzn-Trace-Id: sampled=0;root=1-5a68f9b4-00718037918ec6f8abaacddd
X-Cache: Miss from cloudfront
Via: 1.1 7a06af51e583997d8673ab89482dd45a.cloudfront.net (CloudFront)
X-Amz-Cf-Id: 1YgXeOCWt1SC7nBaB2s8unBvIfhp45JRVJxXL3B-KHRWByGMCAyNRA==
Connection: Keep-alive
```