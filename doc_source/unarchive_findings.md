# UnarchiveFindings<a name="unarchive_findings"></a>

Unarchives Amazon GuardDuty findings that are specified by the list of finding IDs\.

## Request Syntax<a name="unarchive-findings-request-syntax"></a>

**Path parameters:**

```
POST https://<endpoint>/detector/{detectorId}/findings/unarchive
```

**Body:**

```
{
    "findingIds": [
        "string"
    ]
}
```

## Path Parameters<a name="unarchive-findings-path-parameters"></a>

**detectorId**  
The ID of the detector that specifies the GuardDuty service whose findings you want to unarchive\.  
Required: Yes

## Request Parameters<a name="unarchive-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**findingIds**  
The IDs of the findings that you want to unarchive\.  
Type: Array of strings\. Minimum number of 0 items\. Maximum number of 50 items\.  
Required: Yes

## Response Elements<a name="unarchive-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="unarchive-findings-errors"></a>

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

## Example<a name="unarchive-findings-example"></a>

**Sample Request**

```
POST /detector/c6b0be64463ff852400d8ae5b2353866/findings/unarchive HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 52
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T231331Z
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
Date: Fri, 09 Feb 2018 23:13:32 GMT
x-amzn-RequestId: d8d7831e-0dee-11e8-b703-ab81f2419585
X-Amzn-Trace-Id: sampled=0;root=1-5a7e2b1c-5d5292523c568f02a266c57b
X-Cache: Miss from cloudfront
Via: 1.1 8a4a49fefe26d51023ff83ac514d5779.cloudfront.net (CloudFront)
X-Amz-Cf-Id: WWIYv0gEFz8k9cuPE_FT54T1aDL80Nrpfn3bDVLW7s1AbuQzWcMhkg==
Connection: Keep-alive
```