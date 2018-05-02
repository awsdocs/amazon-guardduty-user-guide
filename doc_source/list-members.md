# ListMembers<a name="list-members"></a>

Lists details about all member accounts for the current Amazon GuardDuty master account\.

## Request Syntax<a name="list-members-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/member
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string",
    "onlyAssociated": "boolean"
}
```

## Path Parameters<a name="list-members-path-parameters"></a>

**detectorID**  
The detector ID of the GuardDuty account whose members you want to list\.  
Required: Yes  
Type: String

## Request Parameters<a name="list-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
Indicates the maximum number of items that you want in the response\.  
Required: No  
Type: String  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListMembers` operation\. For subsequent calls to the operation, fill `nextToken` in the request with the value of `NextToken` from the previous response to continue listing data\.  
Required: No  
Type: String

**onlyAssociated**  
Specifies what member accounts the response includes based on their relationship status with the master account\. The default value is TRUE\. If `onlyAssociated` is set to TRUE, the response includes member accounts whose relationship status with the master is set to `ENABLED` or `DISABLED`\. If `onlyAssociated` is set to FALSE, the response includes all existing member accounts\.  
Required: No  
Type: Boolean  
Default: True

## Response Syntax<a name="list-members-response-syntax"></a>

```
{
    "members": [
        {
            "accountId": "string",
            "detectorId": "string",
            "email": "string",
            "masterId": "string",
            "relationshipStatus": "string",
            "invitedAt": "string",
            "updatedAt": "string"
        }
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-members-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**members**  
A list of details about the GuardDuty member accounts\.  
Type: Array    
**accountId**  
The AWS account ID\.  
Type: String  
**detectorId**  
The unique ID of the GuardDuty member account\.  
Type: String  
**email**  
The email address of the GuardDuty member account\.  
Type: String  
**masterId**  
The account ID of the master GuardDuty for a member account\.  
Type: String  
**relationshipStatus**  
The status of the relationship between the member account and its master account\. Valid values: `CREATED` \| `INVITED` \| `DISABLED` \| `ENABLED` \| `REMOVED` \| `RESIGNED` \| `EMAILVERIFICATIONINPROGRESS` \| `EMAILVERIFICATIONFAILED`  
Type: String  
**invitedAt**  
Time stamp at which the member account was invited to GuardDuty\.  
Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.  
**updatedAt**  
Time stamp at which this member account was updated\.  
Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.

**nextToken**  
The token that is required for pagination\. When a response is generated, if there is more data to be listed, this parameter is present in the response and contains the value to use for the `nextToken` parameter in a subsequent pagination request\. If there is no more data to be listed, this parameter is set to NULL\.  
Type: Integer

## Errors<a name="list-members-errors"></a>

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

The request is rejected\. The parameter `maxResults` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `maxResults` is out\-of\-bounds\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `onlyAssociated` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntryException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="list-members-example"></a>

**Sample Request**

```
GET /detector/26b092acdf3e60c625b69013f7488f7b/member HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T214335Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 256
Date: Fri, 09 Feb 2018 21:43:37 GMT
x-amzn-RequestId: 48c4d871-0de2-11e8-a0da-35504ea5b4f3
X-Amzn-Trace-Id: sampled=0;root=1-5a7e1608-de91dbb494298683e2ba0b97
X-Cache: Miss from cloudfront
Via: 1.1 a8a06e035420932f2808c2efee52f455.cloudfront.net (CloudFront)
X-Amz-Cf-Id: _tzbuMnoMN2zwkakGIqpbLE0Dd2sbIyiJ3dj2c3anx_Db7MNmrlNCQ==
Connection: Keep-alive
{  
   "members":[  
      {  
         "accountId":"123456789012",
         "detectorId":"12abc34d567e8fa901bc2d34e56789f0",
         "email":"guarddutymember@amazon.com",
         "relationshipStatus":"Enabled",
         "invitedAt":"2018-02-09T21:33:05.568Z",
         "masterId":"234567890123",
         "updatedAt":"2018-02-09T21:33:46.363Z"
      }
   ]
}
```