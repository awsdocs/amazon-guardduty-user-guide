# GetInvitationsCount<a name="get-invitations-count"></a>

Returns the count of all Amazon GuardDuty membership invitations that were sent to the current member account, not including the currently accepted invitation\.

## Request Syntax<a name="get-invitations-count-request-syntax"></a>

```
GET https://<endpoint>/invitation/count
```

## Response Syntax<a name="get-invitations-count-response-syntax"></a>

```
{
    "invitationsCount": "integer"
}
```

## Response Elements<a name="get-invitations-count-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**invitationsCount**  
The number of all membership invitations sent to this GuardDuty member account, not including the currently accepted invitation\.  
Type: Integer

## Errors<a name="get-invitations-count-errors"></a>

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

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-invitations-count-example"></a>

**Sample Request**

```
GET /invitation/count HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T204945Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 22
Date: Thu, 25 Jan 2018 20:49:46 GMT
x-amzn-RequestId: 471e2f10-0211-11e8-ae9e-81995a5809d1
X-Amzn-Trace-Id: sampled=0;root=1-5a6a42ea-b7e4e135162fc10fffc6ed8b
X-Cache: Miss from cloudfront
Via: 1.1 452a6d5a60db801bab9900e11681a635.cloudfront.net (CloudFront)
X-Amz-Cf-Id: 2VlLvf233bVGY4yOB5rRATpTMVmyNDnOK5pgwA_OMugdypwnYMvpcQ==
Connection: Keep-alive
{  
   "invitationsCount":1
}
```