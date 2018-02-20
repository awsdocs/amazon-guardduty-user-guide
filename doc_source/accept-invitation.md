# AcceptInvitation<a name="accept-invitation"></a>

Accepts the invitation to be monitored by a master GuardDuty account\.

## Request Syntax<a name="accept-invitation-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/master
```

**Body:**

```
{
    "detectorId": string",
    "masterId": "string",
    "invitationId": "string"
}
```

## Path Parameters<a name="accept-invitation-path-parameters"></a>

**detectorID**  
The detector ID of the AWS account that is accepting an invitation to become a GuardDuty member account\.  
Type: String  
Required: Yes

## Request Parameters<a name="accept-invitation-request-parameters"></a>

The request accepts the following data in JSON format\.

**masterId**  
The account ID of the master GuardDuty account whose invitation you're accepting\.  
Type: String  
Required: Yes

**invitationId**  
The ID of the invitation that is sent to the AWS account by the GuardDuty master account\.  
Type: String  
Required: Yes

## Response Elements<a name="accept-invitation-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="accept-invitation-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. A required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. One or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `detectorId` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The current account cannot accept an invitation from the specified account ID because the latter is a member of another master account\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The current account cannot accept invitations because the account contains created, invited, or associated members\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The current account cannot accept invitations because it is already a member of a master account\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The current account has no pending invitation from the specified master account ID or is already a member of another master account\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The specified handshake role of the specified member account ID cannot be assumed by GuardDuty on behalf of the specified master account ID\.

HTTP Status Code: 400 

**LimitExceededException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="accept-invitation-example"></a>

**Sample Request**

```
POST /detector/a12abc34d567e8fa901bc2d34e56789f0/master HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 80
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T203032Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "masterId":"012345678901",
   "invitationId":"84b097800250d17d1872b34c4daadcf5"
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Thu, 25 Jan 2018 20:30:33 GMT
x-amzn-RequestId: 97dfbc58-020e-11e8-92b2-215719f46e03
X-Amzn-Trace-Id: sampled=0;root=1-5a6a3e69-ddfaf64f3fc7013f95e3c3f8
X-Cache: Miss from cloudfront
Via: 1.1 d98420743a69852491bbdea73f7680bd.cloudfront.net (CloudFront)
X-Amz-Cf-Id: mNPHSIIZh4O75j28b4jSZ6JaybkjuX3ek9Qu0EREyNYT19f-ZC9opg==
Connection: Keep-alive
```