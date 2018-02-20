# GetMembers<a name="get-members"></a>

Returns the details on the Amazon GuardDuty member accounts that are specified by the account IDs\.

## Request Syntax<a name="get-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/get
```

**Body:**

```
{
    "accountIds": [
        {
            "accountId": "string"
        }
     ]
}
```

## Path Parameters<a name="get-members-path-parameters"></a>

**detectorID**  
The detector ID of the GuardDuty account on whose members you want to return the details\.  
Type: String  
Required: Yes

## Request Parameters<a name="get-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountIds**  
A list of account IDs for the GuardDuty member accounts on which you want to return the details\.  
Type: Array of strings  
Required: Yes    
**accountID**  
The AWS account ID\.  
Type: String

## Response Syntax<a name="get-members-response-syntax"></a>

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
    "unprocessedAccounts": [
        {
            "accountId": "string",
            "result": "string"
        }
    ]
}
```

## Response Elements<a name="get-members-response-parameters"></a>

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
The status of the relationship between the member account and its master account\. Valid values: `CREATED` | `INVITED` | `DISABLED` | `ENABLED` | `REMOVED` | `RESIGNED`  
Type: String  
**invitedAt**  
Time stamp at which the member account was invited to GuardDuty\.  
Type: String  
**updatedAt**  
Time stamp at which this member account was updated\.  
Type: String

**unprocessedAccounts**  
A list of account ID and email address pairs of the AWS accounts that could not be processed\.  
Type: Array of strings    
**accountID**  
The ID of the AWS account that could not be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="describe-members-errors"></a>

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

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-members-example"></a>

**Sample Request**

```
POST /detector/26b092acdf3e60c625b69013f7488f7b/member/get HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 32
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T213609Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "accountIds":[  
      "123456789012"
   ]
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 283
Date: Fri, 09 Feb 2018 21:36:10 GMT
x-amzn-RequestId: 3e768f7b-0de1-11e8-afbe-2bd59a045a01
X-Amzn-Trace-Id: sampled=0;root=1-5a7e144a-24c5171e766097b2c56c3822
X-Cache: Miss from cloudfront
Via: 1.1 27a783405519f49942e72a6ed75f783f.cloudfront.net (CloudFront)
X-Amz-Cf-Id: cz0twV2DdUinG-VzZD0bryhWIB8OcfoTBkPKbecD2TdkbvqWCvo7aw==
Connection: Keep-alive
{  
   "members":[  
      {  
         "accountId":"234567890123",
         "detectorId":"12abc34d567e8fa901bc2d34e56789f0",
         "email":"guarddutymember@amazon.com  ",
         "relationshipStatus":"Monitored",
         "invitedAt":"2018-02-09T21:33:05.568Z",
         "masterId":"123456789012",
         "updatedAt":"2018-02-09T21:33:46.363Z"
      }
   ],
   "unprocessedAccounts":[  

   ]
}
```