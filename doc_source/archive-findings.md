# ArchiveFindings<a name="archive-findings"></a>

Archives Amazon GuardDuty findings that are specified by a list of finding IDs\.

**Important**  
Users from GuardDuty member accounts cannot run this API\. Currently in GuardDuty, users from member accounts CANNOT archive findings either in their own accounts, or in their master's account, or in other member accounts\. 

## Request Syntax<a name="archive-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/archive
```

**Body:**

```
{
    "findingIds": [
        "string"
    ]
}
```

## Path Parameters<a name="archive-findings-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose findings you want to archive\.  
Required: Yes  
Type: String

## Request Parameters<a name="archive-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**findingIds**  
The IDs of the findings that you want to archive\.  
Type: Array of strings\. Minimum number of 0 items\. Maximum number of 50 items\.  
Required: Yes

## Response Elements<a name="archive-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="archive-findings-errors"></a>

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

The request is rejected\. The number of requested finding IDs is out\-of\-bounds\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. The caller is not authorized to call this API\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="archive-findings-example"></a>

**Sample Request**

```
POST /detector/c6b0be64463ff852400d8ae5b2353866/findings/archive HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 52
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T231008Z
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
Content-Length: 0
Date: Fri, 09 Feb 2018 23:10:09 GMT
x-amzn-RequestId: 5fc7b08b-0dee-11e8-b559-79ec310d4e06
X-Amzn-Trace-Id: sampled=0;root=1-5a7e2a51-442c3de5468266edf3c048ca
X-Cache: Miss from cloudfront
Via: 1.1 51f2e50a0d2a5ee1d9c830bf417b2713.cloudfront.net (CloudFront)
X-Amz-Cf-Id: uEzj5jCFHxEGfKoTmB6Wgt8a3uM2JaXrEH0qzaT_JQ-rMDr-HdT9PA==
Connection: Keep-alive
```