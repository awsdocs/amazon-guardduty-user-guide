# UpdateFindingsFeedback<a name="update-findings-feedback"></a>

Marks specified Amazon GuardDuty findings as useful or not useful\.

## Request Syntax<a name="update-findings-feedback-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/feedback
```

**Body:**

```
{
    "findingIds": [
        "string"
    ],
    "feedback": "[USEFUL|NOT_USEFUL]",
    "comments": "string"
}
```

## Request Parameters<a name="update-findings-feedback-path-parameters"></a>

**detectorId**  
The detector ID of the GuardDuty service whose findings you want to mark as useful or not useful\.  
Type: String

## Request Parameters<a name="update-findings-feedback-request-parameters"></a>

The request accepts the following data in JSON format\.

**findingIds**  
The IDs of the findings that you want to mark as useful or not useful\.  
Type: Array of strings\. Minimum number of 0 items\. Maximum number of 50\.  
Required: Yes

**feedback**  
Type: String  
Required: Yes  
Valid values: `USEFUL` \| `NOT_USEFUL`

**comments**  
Additional feedback about the GuardDuty findings\.  
Type: String  
Required: No  
Limits: maximum of 160 characters\. Supported characters include only a\-z, A\-Z, 0\-9, and single and double quotes\.

## Response Elements<a name="update-findings-feedback-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="update-findings-feedback-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. The required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. One or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `detectorId` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter comment has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The number of requested finding IDs is out\-of\-bounds\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="update-findings-feedback-example"></a>

**Sample Request**

```
POST /detector/c6b0be64463ff852400d8ae5b2353866/findings/feedback HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 78
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T230429Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "findingIds":[  
      "9cb0be64df8ba1df249c45eb8a0bf584"
   ],
   "feedback":"NOT_USEFUL"
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Fri, 09 Feb 2018 23:04:30 GMT
x-amzn-RequestId: 9599e105-0ded-11e8-a294-df0cbca23ced
X-Amzn-Trace-Id: sampled=0;root=1-5a7e28fe-885816710d8ec164f83ae38d
X-Cache: Miss from cloudfront
Via: 1.1 33cfbeb7154bbef1432b207659c6dac5.cloudfront.net (CloudFront)
X-Amz-Cf-Id: Z6_YLuTs4hTxC5OUgUUVwoqhEALPrE9HyelAd-6qxmRViJO0L6bjcA==
Connection: Keep-alive
```