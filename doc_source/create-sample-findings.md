# CreateSampleFindings<a name="create-sample-findings"></a>

Creates sample findings of the types that are specified by a list of Amazon GuardDuty finding types\. If NULL is specified for `findingTypes`, the operation creates sample findings of all supported GuardDuty finding types\. 

## Request Syntax<a name="create-sample-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/create
```

**Body:**

```
{
    "findingTypes": [
        {
            "findingType": "string",
        }
     ]
}
```

## Path Parameters<a name="create-sample-findings-path-parameters"></a>

**detectorId**  
The ID of the GuardDuty service where you want to create sample findings\.  
Required: Yes  
Type: String

## Request Parameters<a name="create-sample-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**findingTypes**  
The list of GuardDuty finding types that specifies what types of sample findings that you want to create\.  
Required: Yes  
Type: Array of strings  
Constraints: Minimum length of 0\. Maximum length of 50\.    
**findingType**  
The type of the GuardDuty finding\.  
Type: String

## Response Elements<a name="create-sample-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="create-sample-findings-errors"></a>

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

The request is rejected\. An invalid finding type is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="create-sample-findings-statistics-example"></a>

**Sample Request**

```
POST /detector/c6b0be64463ff852400d8ae5b2353866/findings/create HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T225730Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Fri, 09 Feb 2018 22:57:32 GMT
x-amzn-RequestId: 9c2bd04f-0dec-11e8-9ce5-1d60637acb70
X-Amzn-Trace-Id: sampled=0;root=1-5a7e275b-e03cf47efbf2e2aea8199ebf
X-Cache: Miss from cloudfront
Via: 1.1 27a783405519f49942e72a6ed75f783f.cloudfront.net (CloudFront)
X-Amz-Cf-Id: eat7We8tGOkIFZ9TQ6UEcGQQZI17OTIMUcRSR6GrcjbLmHEJWszspQ==
Connection: Keep-alive
```