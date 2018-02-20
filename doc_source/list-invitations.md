# ListInvitations<a name="list-invitations"></a>

Lists all Amazon GuardDuty membership invitations that were sent to the current AWS account\.

## Request Syntax<a name="list-invitations-request-syntax"></a>

```
GET https://<endpoint>/invitation
```

**Body:**

```
{
    "maxResults" : "integer"
    "nextToken" : "string"
}
```

## Request Parameters<a name="list-invitations-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
Indicates the maximum number of items that you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListInvitations` operation\. For subsequent calls to the operation, fill `nextToken` in the request with the value of `NextToken` from the previous response to continue listing data\.  
Required: No  
Type: String

## Response Syntax<a name="list-invitations-response-syntax"></a>

```
{
    "invitations": [
        {
           "accountId": "string",
           "invitationId": "string",
           "invitedAt": "string",
           "relationshipStatus": "string"
        }
     ],
     "nextToken": "string"
}
```

## Response Elements<a name="list-invitations-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**invitations**  
A list of details about GuardDuty membership invitations that were sent to this AWS account\.  
Type: Array    
**accountId**  
The ID of the AWS account that sent the invitation\.  
Type: String  
**invitationId**  
The unique ID of the invitation\.  
Type: String  
**invitedAt**  
The time stamp at which the invitation was sent\.  
Type: String  
**relationshipStatus**  
The current relationship status between the inviter and invitee accounts\. Valid values: `CREATED` | `INVITED` | `DISABLED` | `ENABLED` | `REMOVED` | `RESIGNED`  
Type: String

**nextToken**  
When a response is generated, if there is more data to be listed, this parameter is present in the response and contains the value to use for the `nextToken` parameter in a subsequent pagination request\. If there is no more data to be listed, this parameter is set to NULL\.  
Type: String

## Errors<a name="list-invitations-errors"></a>

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

The request is rejected\. The parameter `maxResults` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `maxResults` is out\-of\-bounds\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="list-invitations-example"></a>

**Sample Request**

```
GET /invitation HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T201238Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 180
Date: Thu, 25 Jan 2018 20:12:39 GMT
x-amzn-RequestId: 176ef1d7-020c-11e8-8ed9-eb03a370f9db
X-Amzn-Trace-Id: sampled=0;root=1-5a6a3a37-ce08a19c90097c2711af6d20
X-Cache: Miss from cloudfront
Via: 1.1 8a4a49fefe26d51023ff83ac514d5779.cloudfront.net (CloudFront)
X-Amz-Cf-Id: 6lDytN8vgXTKCeKmTKW6n9uu-Q8auCCDJENKQ46nagklpnjkeIuFkA==
Connection: Keep-alive
{  
   "invitations":[  
      {  
         "accountId":"6012345678901",
         "invitationId":"2cb097774d0b74808af8fa270f1dc404",
         "invitedAt":"2018-01-25T20:07:24.438Z",
         "relationshipStatus":"Invited"
      }
   ],
   "empty":false
}
```