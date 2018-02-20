# DeleteMembers<a name="delete-members"></a>

Deletes the Amazon GuardDuty member accounts that are specified by the account IDs\.

## Request Syntax<a name="delete-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/delete
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

## Path Parameters<a name="delete-members-path-parameters"></a>

**detectorID**  
The detector ID of the GuardDuty service whose member accounts you want to delete\.  
Type: String  
Required: Yes

## Request Parameters<a name="delete-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountIds**  
A list of account IDs of the GuardDuty member accounts that you want to delete\.  
Type: Array of strings  
Required: Yes    
**accountID**  
AWS account ID\.  
Type: String

## Response Syntax<a name="delete-members-response-syntax"></a>

```
{
    "unprocessedAccounts": [
        {
            "accountId": "string",
            "result": "string"
        }
    ]
}
```

## Response Elements<a name="delete-members-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The service returns the following data is returned in JSON format\.

**unprocessedAccounts**  
A list of account ID and email address pairs of the AWS accounts that could not be processed\.  
Type: Array of strings    
**accountID**  
The ID of the AWS account that could not be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="delete-members-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. The current account cannot delete the specified member account ID because it is still associated to it\.

HTTP Status Code: 200 

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

**NoSuchEntryException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="delete-members-example"></a>

**Sample Request**

```
POST /detector/26b092acdf3e60c625b69013f7488f7b/member/delete HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 32
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T220100Z
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
Content-Length: 26
Date: Fri, 09 Feb 2018 22:01:01 GMT
x-amzn-RequestId: b7409e55-0de4-11e8-aa1d-17f6b1e5e6f5
X-Amzn-Trace-Id: sampled=0;root=1-5a7e1a1d-8736f50418456d404294b219
X-Cache: Miss from cloudfront
Via: 1.1 b2532cb29a55e8fe8106a4a9a9241592.cloudfront.net (CloudFront)
X-Amz-Cf-Id: yZC2KsBzimqUgjOxPaamXSKWpXmMlFOIOSbEhNamaGRNwkXzaf50yQ==
Connection: Keep-alive
{  
   "unprocessedAccounts":[  

   ]
}
```