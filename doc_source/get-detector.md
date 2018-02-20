# GetDetector<a name="get-detector"></a>

Returns the properties of the Amazon GuardDuty detector that is specified by the detector ID\.

## Request Syntax<a name="get-detector-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}
```

## Path Parameters<a name="get-detector-path-parameters"></a>

**detectorId**  
The unique ID of the detector that you want to describe\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-detector-response-syntax"></a>

```
{
    "serviceRole": "string",
    "status": "string",
    "createdAt": "string",
    "updatedAt": "string"
}
```

## Response Elements<a name="get-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

 The response is the following data in JSON format\.

**serviceRole**  
The service\-linked role that grants GuardDuty access to the resources in the AWS account\.   
Type: String

**status**  
The current status of the detector\.  
Type: String\. Valid Values: `ENABLED` | `DISABLED`

**createdAt**  
The time at which the detector was created\.  
Type: String

**updatedAt**  
The time at which detector was last updated\.  
Type: String

## Errors<a name="get-detector-errors"></a>

If the action is not successful, the service returns an HTTP error response code along with detailed error information\.

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

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-detector-example"></a>

**Sample Request**

```
GET /detector/12abc34d567e8fa901bc2d34e56789f0 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180123T220712Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 220
Date: Tue, 23 Jan 2018 22:07:13 GMT
x-amzn-RequestId: c3cfdfa5-0089-11e8-a4e2-07af7075b461
X-Amzn-Trace-Id: sampled=0;root=1-5a67b211-9b4ca2adcf4a8bc402a66eac
X-Cache: Miss from cloudfront
Via: 1.1 fe951a27fbed2178f4268c584d282a1d.cloudfront.net (CloudFront)
X-Amz-Cf-Id: VcRcgzIE3MRFumWYKiXjXsoaY2GJSPSo7Q4eSDp7dNquhfxzrZgbgA==
Connection: Keep-alive
{  
   "status":"DISABLED",
   "createdAt":"2018-01-23T21:53:32.815Z",
   "updatedAt":"2018-01-23T21:53:32.815Z",
   "serviceRole":"arn:aws:iam::123456789012:role/aws-service-role/guardduty.amazonaws.com/AWSServiceRoleForAmazonGuardDuty"
}
```